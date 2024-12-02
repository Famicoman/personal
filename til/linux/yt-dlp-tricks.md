# yt-dlp Tricks

We want to download some videos via the terminal!

## Installation

It is important we use a newish version of `yt-dlp`:

```
$  python3 -m pip install -U "yt-dlp[default,curl-cffi]"
```

## Downloading embedded Vimeo videos

```
$ yt-dlp https://amigavideo.net/toasterpaint-video-toaster-2-0-essentials/
```

With a timeout of 300 seconds (for slow loading pages):

```
yt-dlp --socket-timeout 300 https://amigavideo.net/category/productionedition/ravevideoproductions/
```