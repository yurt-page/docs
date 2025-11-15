## Blog
See [yurt-blog](https://github.com/yurt-page/yurt-blog) engine.

Key features and ideas:
* RSS must be supported. Only it gives real freedom for readers. In fact only RSS will be enough to make life better for most peoples.
* The blog itself may be just an online RSS reader. I.e. you can read your own blog the same as any other.
* Multiple authors aren't necessary. We may have a very simple access list model.
* Friendly SEO is very wanted but not so important than everything else. I.e. not generate of pure HTML to be indexed. We may instead create some aggregator/proxy or maje our own "blog search" as Yandex.Blogs.
* Comments must be developed even better than posts: discussions are the main focus. Comments on habr.com are much valuable than post.
* But for some posts comments may be just disabled like in Telegram Channels. Such posts must have a different type like Note.
* So we must support different types of posts: articles (translatable and searchable), notes (not searchable), gists (not published in feed but searchable) etc.
* Stats must be as good as possible (countries, unique readers, read time etc.) but in the same time we must value users privacy (do not use or leak third party data). Otherwise, users may start to use Google Analytics or other even worst spying systems. But some websites like e-commerce for marketing still needs more stats. We are fine to create own tracking system (at least we are not evil yet).
* Cross posting is very important. We must allow publishing to Twitter, FB, anything else.
* We must also be friendly for cross posting and support OData.
* Subscribe via email will be very nice. XMPP/Web/Telegram push.
* To minimize space and optimize speed we may store posts directly in RSS but each post separately. We are free to extend RSS with our elements like comments.
* Support for git/markdown static generators. We may create a plugin for Jekyl/Hugo.
* Maybe we can add a versioning and send only diffs on editing.
* Very basic WYSIWYG editor and use Markdown. But on saving convert MD to HTML/RSS.
* For an API we may try to use AtomPub or even use raw WebDAV PUT.
* We must gzip post content on client before sending. Thus, we'll save resources on router.
* Spam Protection is the hardest thing to do. PoW Captcha may help https://git.sequentialread.com/forest/pow-captcha. Maybe reuse the Hashcash for email



### Another interesting solutions
Basically any static site generator may be used like [Hugo](https://gohugo.io/) and [it's alternatives](https://www.google.com/search?q=hugo+alternatives).
But they all are written in Go/Ruby/PHP and it's hard to put them on a router.
Hugo in Go, [Grav CMS](https://learn.getgrav.org/17/basics/what-is-grav): in PHP,
[Ghost](https://github.com/TryGhost/Ghost) and
[11ty](https://github.com/11ty/eleventy/) in NodeJS.
The https://www.htmly.com/ in PHP

Shell script based site generators:
* Luke Smith blog scripts https://github.com/LukeSmithxyz/lb
* suckless.org static generator https://git.codemadness.org/saait/file/README.html
* https://codeberg.org/vimuser/untitled uses pandoc templates. Used by libreboot.org
* https://blot.im/ allows to create a blog from DropBox. Sources https://github.com/davidmerfield/blot
* https://turtlapp.com/  collaborative notebook
* https://github.com/luevano/luevano.xyz Python based static enerator

WebDAV based blog engines:
* https://github.com/katomaso/webdave


* [indieforums](https://www.indieforums.net/threads/024f3f45f725dba0.html)
* https://searchmysite.net/ search by indie blogs

## Compression
My entire blog for ten years in Wordpress when exported to RSS (XMl) is only about 3mb. So it may be served even from a 4mb router if remove Luci from it and compress the rss and then uncompress into memory (/tmp) and serve.
Basically the squashfs on the OpenWrt use the LZMA compression so the additional compression may be not needed.

We can serve the pre-compressed file directly with `Content-Encoding: gzip` and save a network bandwith.
Browsers supports only deflate, gzip, brotli, and Chrome now also supports zstd. The RSS is usually consumed by RSS readers that may support only deflate and gzip. Two Yurts may use any compression which they like e.g LZMA but this is a last resort.

* deflate compression uses a 32k window without a dictionary. Fast and effective.
* gzip is a deflate with a checksum. This is a de-facto standard default encryption. OpenWrt have the gzip command out of the box.
* lzma gives a best compression, but extreemely slow on compression and decompression. The OpenWrt uses it for SquashFS but there is no xz command out of the box. One of my ideas was to bring the lzma compressor from the SquashFS to user space command.
* brotli has a dictionary for web assets (HTML, JS and CSS) and has slow compression but fast enough decompression. It may be too heavy to install on routers. The format is really bad by itself: no concatenation, no magic header. Most advantages comes from the good dictionary.
* zstd has a good compression speed and it can be a replacement for gzip as a default. You can use a dictionary to improve. With a maximum level it almost like xz but with a better decompression speed.

Here is a comparission of compression ratio of the rss.xml and size of all separate posts gzipped:

| file        | bytes   | ratio |
|-------------|---------|-------|
| rss.xml     | 3104010 |       |
| rss.xml.gz  | 665879  | 21%   |
| rss.xml.zst | 463984  | 14%   |
| rss.xml.xz  | 450184  | 14%   |
| rss.xml.br  | 437314  | 14%   |
| post.*.gz   | 911604  | 29%   |

Just gzip makes the rss five times smaller. With Brotli it can be seven times smaller.
But gzipped files can be processed on OpenWrt backend more easily.

As a trick we can use gzip or any other compression on a browser side.
When a user posting an article to a blog a JS library compress the post before sending to OpenWrt backend.
A backend may need to decompress it to validate but if you are posting to own blog then the step can be skipped.
Even if you need to decompress on a backend to validate that would be less expensive job than validate and compress.
This also saves a bandwidth (not so important if you post once a week).
One day (but in far feature) browsers will start to support compressed requests:
* https://stackoverflow.com/questions/424917/why-cant-browser-send-gzip-request
* https://support.google.com/chrome/thread/182178237/sending-compressed-request-from-browser-to-api-server
* https://stackoverflow.com/questions/7555902/is-it-possible-to-use-content-encoding-gzip-in-a-http-post-request


The JS libraries by itself may be bigger than the zstd or brotli installed on a backend.
But they can be served from CDN.

If we split RSS to separate posts then we can serve each post separately and render it to HTML by JS.
This will save a space and simplify.
Additionally for RSS readers we can return only last posts concatenated.

When splitting posts and compress them separately then compression ratio is worse but still remains good enough i.e. 29%.

Files compressed with gzip can be simply concatenated and decompressed as one file.
The problem is that browsers don't support this https://issues.chromium.org/issues/40990701
Browsers seems to use the [inflateInit2](https://github.com/madler/zlib/blob/develop/zlib.h#L837) function:

    Unlike the gunzip utility and gzread() (see
    below), inflate() will *not* automatically decode concatenated gzip members.
    inflate() will return Z_STREAM_END at the end of the gzip member.  The state
    would need to be reset to continue decoding a subsequent gzip member.  This
    *must* be done if there is more data after a gzip member, in order for the
    decompression to be compliant with the gzip standard (RFC 1952).

This must be easy to fix but difficult to marge into mainline. Anyway this work needs to be done as a side project.

Good news is that the concatenation works for raw deflate and zstd.
The gzip utility doesn't support creation of raw deflate (both GNU gzip, BusyBox gzip and even pigz).

I created the [deflate](https://github.com/stokito/deflate) tool for tests.
But we may use the gzip and then extract the raw deflate by removing header and tail checksum:

```sh
echo "hello" | gzip > hello.txt.gz
cat hello.txt.gz | tail --bytes=+11 | head --bytes=-8 > hello.txt.deflate
```

As an alternative, we may deflate with a JS library [pako](https://github.com/nodeca/pako) (15kb minified).
Same is possible with zstd.

So as a conclusion the better option would be to use an RSS split to posts, minified and compressed with deflate in a browser with the pako.js library.
This will give a good tradeoff between interoperability, size and complexity. 

## Comment spam protection
* https://blog.lopp.net/protect-contact-forms-from-spam-with-proof-of-work/ Hashcash
