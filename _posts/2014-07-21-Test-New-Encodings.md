---
layout: post
title: 'Test New Encodings With Fastly'
---

**Note:** This is another [cross post from the Fastly blog.](http://www.fastly.com/blog/test-new-encodings-with-fastly/)
It really showcases the flexibility that Varnish, and Fastly as a result, provides as a caching platform. [DocWilco](https://github.com/drwilco)
was a significant help in making sure that the VCL and overall logical processes here were sound. It wouldn't have
shipped without him.

----

At Fastly, we believe that the freedom to experiment is what makes the web great. We're excited by the cutting edge breakthroughs in file encodings that are happening almost every day, making the web
better and faster.

For example, Google has been developing the [WebP format](https://developers.google.com/speed/webp/?csw=1)
and Mozilla recently released version 2.0 of their [MozJPEG encoding](https://blog.mozilla.org/blog/2014/07/15/improving-jpeg-image-encoding/). Both have the potential to speed up global web performance, but each new encoding format [can have tradeoffs](http://www.cnet.com/news/facebook-tries-googles-webp-image-format-users-squawk/)
in your application (if you're testing either of these, make sure you keep this in mind).

### Fastly Lets You Experiment With New Encodings
Your CDN shouldn't hold you back from testing new file encodings and compression techniques. Our mission is to push web performance to new heights, so enabling experimentation is crucial. With Fastly, you can take a walk on the bleeding edge just like web giants such as [Facebook](http://thenextweb.com/insider/2014/07/15/mozilla-releases-mozjpeg-2-0-facebook-tests-backs-jpeg-encoder-60000-donation/).

If your users' browsers support these formats, and if you have these image
formats on your origin server, Fastly can serve the new encodings on the fly
with some VCL. Note that for every .jpeg, .jpg, and .png, you need to have the corresponding .webp.
For instance, if you have a `/foo/bar.jpeg` on your server, you also need to have a `/foo/bar.webp`.

```perl
sub vcl_recv {
  # Normalize Accept, we're only interested in webp right now.
  # And only normalize for URLs we care about.
  if (req.http.Accept && req.http.url ~ "(\.jpe?g|\.png)($|\?)") {
    # So we don't have to keep using the above regex multiple times.
    set req.http.X-Is-An-Image-URL = "yay";

    # first let's see if it's unacceptable
    if (req.http.Accept ~ "image/webp[^,];q=0(\.0?0?0?)?[^0-9]($|[,;])")
      unset req.http.Accept;
    }

    # It is acceptable, so if present set to only that
    if (req.http.Accept ~ "image/webp") {
      set req.http.Accept = "image/webp";
    } else {
      # not present, and we don't care about the rest
      unset req.http.Accept;
    }
  }
#FASTLY recv
}

sub vcl_miss {
  # If you have /foo/bar.jpeg, you should also have a /foo/bar.webp

  if (req.http.Accept ~ "image/webp" && req.http.X-Is-An-Image-URL) {
    set req.http.url = regsuball(req.http.url, "(\.jpe?g|\.png)($|\?)", ".webp\2");
  }
#FASTLY miss
}

sub vcl_fetch {
  if (req.http.X-Is-An-Image-URL) {
    if (!beresp.http.Vary ~ "(^|\s|,)Accept($|\s|,)") {
      if (beresp.http.Vary) {
        set beresp.http.Vary = beresp.http.Vary ", Accept";
      } else {
         set beresp.http.Vary = "Accept";
      }
    }
  }
#FASTLY fetch
}
```

This example assumes that you have your `.webp` files in the same directory as your
`.jpeg` and `.png` files, but you can rewrite your URLs as needed to fit your
deployment process.

### How Does This Work?
First of all, since `Vary` is being used, you need to normalize the `Accept` header
so that the header contains only two options. Without that, you risk lowering your hit rate
and increasing traffic to origin. For any image URLs, you want `Accept` to either be empty 
or to contain image/webp. That way, you're guaranteed to only have one copy of the `.jpeg`/`.png` file,
and one copy of the `.webp` file to serve all requests for that image.

After normalization in `vcl_recv`, the next step is changing the URL that you send to the
backend. This happens in `vcl_miss`, so that hash isn't changed, and a purge of the image
URL will purge both the `.jpeg`/`.png` and the `.webp` variants. Basically, if the client accepts
`.webp`, the `.jpeg`/`.jpg`/`.png` at the end is swapped with with `.webp`.

Finally, `Accept` is added to the `Vary` header in `vcl_fetch`, so that the `.webp` and the
original can coexist under the same URL, and the correct one will be served depending on the
value of `Accept`.

What's great is that this can be used for any file encoding, not just `.webp`. With
a few tweaks, you can support other encodings in the same way.

Have fun testing these new encodings! If you have any questions, don't hesitate
to contact us by emailing <a href="mailto:support@fastly.com">support@fastly.com</a>.
