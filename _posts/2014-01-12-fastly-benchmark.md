---
layout: post
title: Fastly Benchmark
---

I got tired of looking at third party benchmarks of Fastly using closed source tools. They were black boxes, so I couldn't justify the
numbers (good or bad) that they claimed. So, Simon and I knocked out the ultimate [mic-droppingly](http://0.media.collegehumor.cvcdn.com/56/95/7890f6112c0b7925960efaa915a58a56-dropmic3.gif) honest benchmarking we could.

Take a look at the Gist [here](https://gist.github.com/aspires/8189975), but the script is (intentionally) so short that I can paste it in:

```
#!/bin/bash

# Dependencies: ApacheBench, MTR

REQUESTS=100
CONCURRENCY=10
FASTLY='www.example.com.global.prod.fastly.net'
CURRENT='www.example.com'

for url in 'path/to/test' 'path/to/test2' 'path/to/test3'; do
  for host in $CURRENT $FASTLY; do
    ab -n $REQUESTS -c $CONCURRENCY "http://${host}/${url}" >> fastly.ab.log
    #echo "http://${host}/${url}"
  done
done

for host in $CURRENT $FASTLY; do
  mtr -c $REQUESTS -w -r $host >> fastly.mtr.log
done
```

That's it. No fancy whiz-bangery. No grandisose flash and flare. Just tried and true metrics tools that have been used in the industry for decades.

## So, what's going on?

The script uses two benchmarking tools:

- [ApacheBench](http://en.wikipedia.org/wiki/ApacheBench)
- [MTR](http://en.wikipedia.org/wiki/MTR_(software))

The user provides their existing domain, and the fastly generated service domain. __Note: the site and service need to be configured proper
ly for caching for the test to be realistic.__

From there, the script tests as many paths as the user desires with `ab`. The primary metric you want to look for here is the connection
times and the percentile results. These readouts are going to be a good approximation of TTFB for that object.

```
#Other apache heath stats

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       86   92   3.2     91      98
Processing:   531  239 155.0    860    1234
Waiting:      234  640 145.8    649     962
Total:        675  931 155.3    945    1325

Percentage of the requests served within a certain time (ms)
  50%    955
  66%   1029
  75%   1053
  80%   1058
  90%   1112
  95%   1197
  98%   1216
  99%   1325
 100%   1325 (longest request)

```

The second command, for MTR, tests 100 cycles of network connection for each host. The readout should give you about overall network
performance. The preformance you see here should correlate with the `ab` results, but it's a seperate approach to verifying latency
improvements.

```
HOST: ip-172-31-2-216                                 Loss%   Snt   Last   Avg  Best  Wrst StDev
  1. ec2-79-125-1-98.eu-west-1.compute.amazonaws.com  0.0%   100    0.8   1.2   0.6  27.8   3.2
  2. 178.236.0.220                                    0.0%   100    0.9   2.0   0.9  43.8   5.3
  3. 178.236.0.182                                    0.0%   100    1.6   1.6   1.2  18.0   1.8
  5. 178.236.3.52                                     0.0%   100   10.9  13.0  10.6  70.0   9.8
  6. 82.112.115.161                                   0.0%   100   11.6  11.5  11.1  12.8   0.2
  7. ae-13.r02.londen03.uk.bb.gin.ntt.net             0.0%   100   12.1  12.0  11.3  13.8   0.3
  8. te0-7-0-9.ccr21.lon02.atlas.cogentco.com         0.0%   100   12.4  12.0  11.3  13.8   0.5
  9. be2328.ccr21.lon01.atlas.cogentco.com            0.0%   100   11.5  11.8  11.5  13.9   0.4
 10. te2-1.ccr01.lon03.atlas.cogentco.com             0.0%   100   12.1  24.8  11.9 180.9  38.2
 11. ???                                             100.0   100    0.0   0.0   0.0   0.0   0.0
 12. 185.31.18.185                                    0.0%   100   14.9  12.5  11.0  15.4   1.8
```

# The rule going forward

We're not stoping here with benchmarking and evaluation options. We want more exaustive tools that go deeper into edge cases, and don't
require as much external configuration. Right now, you need to have `ab` and `mtr` on your machine, and you realistically need a 
few EC2 instances or other servers to test global performance. You need to have your Fastly service set up to cache properly,
otherwise the tests will all be cache misses. Also, the `ab` test sucks on mac; it errors out every other benchmark. This is 
too much work for such a simple script. It needs to be improved upon.

But, the core principles of a simple, open, reproducable test is something that will be around in the future. 
