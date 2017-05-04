---
layout: post
title: More LED controllers
---

In the last post, we looked at *Fadecandy*, *RGB-123 Cape for BeagleBone* and *PixelPushers*. Since then, I've done a bit more research about other controllers:

## AllPixel 

(This seems to be kind of recent, but out of stock everywhere)

This is another small, [USB controller](http://maniacallabs.com/allpixel/). It controlls a single strand for most LED types, up to 700 LEDs per controller. The software side is handled by a [Python library](https://github.com/ManiacalLabs/BiblioPixel).

which supports a bunch of usecase. Seems to have a composable architecture, where it can drive physical LEDs or network controllers (where it uses a TCP protocol that's a bit different from OPC). Might be room for a thing translater?

The designers deliberately make this as an alternative to the Fadecandy, with objectives around driving longer strips and using wider range of LEDs. Further more, it uses some sort of serial protocol instead of full USB (I don't know what the difference is, really). Quite affordable actually.

## Octoscroller

(another output cape for BBB?) How does this compare to the RGB-123 one?

Look at some Aliexpress specials?

What is a PixLite? Seems a bit more DMX-y


