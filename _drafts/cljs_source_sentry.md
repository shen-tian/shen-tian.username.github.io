---
layout: post
title: ClojureScript Sourcemaps on Sentry
---

## Problem

[Sentry][sentry] is an error tracking tool, which is used to collect
errors/exceptions your program encounters in the wild. In particular, it
is useful for collecting errors from JS web apps.

[sentry]: https://sentry.io

It supports source maps, thus able to pinpoint the error down to a line
in your source file, even while running the prod build, which is often
minimized.

This is particularly useful when the source is in a different language
than JS itself. For a ClojureScript project

## Steps

Compiler settings:

```clj
{:id           "min"
 :source-paths ["src"]
 :compiler     {:main          your-app.core
                :output-to     "resources/public/js/compiled/app.js"
                :output-dir    "resources/public/js/compiled"
                :optimizations :advanced
                :source-map    "resources/public/js/compiled/app.js.map"}}
```

- `:output-dir` will contain the source (both yours, but also dependencies).
this is what we want to send to Sentry;
- `:source-map` is the sourcemap file itself.

Create the release on Sentry and Upload the source

```bash
sentry-cli releases \
    new \
    $RELEASE_NAME

sentry-cli releases \
    files \
    $RELEASE_NAME \
    upload-sourcemaps \
    --url-prefix $DEPLOY_URL/js/compiled \
    --ext cljs \
    --ext clj \
    --ext cljc \
    --ext js \
    --ext map \
    resources/public/js/compiled
```

Delete the source!

Deploy your app
