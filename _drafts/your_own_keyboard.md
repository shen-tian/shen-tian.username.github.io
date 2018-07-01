---
layout: post
title: Adventures in customised keyboards
published: true
---
About 18 months ago, I went down a rabbit hole, which, long story short, ended with me wanting to build my own computer keyboard. I've since completed the said keyboard and been using it whenever I've been at my work desk.

As with most obsessive hobbies, things get weird and wonderful in the land of DIY keyboards. I'll try to document some desgin decisions I ended up making here.

My objectives:

- Have a keyboard that's efficient, comfortable (and fun) to work on while at my desk;
- Doesn't make it harder for me to use normal keyboards (mostly Macs or ThinkPads);
- Not important: anyone being able to use my keyboard.

To cut the tension. I ended up with a Preonic keyboard. It is small but not tiny, and the keymap aims to reproduce the left-side of standard keyboards, while allowing for better access to right hand symbols.

## Non staggered keyboards

Most keyboards have the typewritter stagger, which allowed levers inside mechanical typewriters to not interfere with each other. Needless to say, this is a bit of an anarchronism, but opinions vary on how much of a problem this introduces. There's a couple of contemporary keyboard designs that does away with this. This includes the [ErgoDox][ergodox], [Atreus][atreus], and various [Ortholinear Keyboards][olkb].

[ergodox]: https://www.ergodox.io/
[atreus]: https://atreus.technomancy.us/
[olkb]: https://olkb.com/

The Preonic I ended up with is from OLKB. I found the adaptation to the non-stagger fairly easy, except for one area: re-learning which fingers I use to press the `X` and `C` keys. Turns out that like many people, I've been using my index finger for `C` and middle finger for `X`. This adaptation does mean I occationally mistype these keys on a normal keyboard, but doesn't present a major issue.

Overall, I'm not convinced that having aligned columns is better or worse than the standard keyboard layout. It's simply slightly different. It's conceptually (and physically) neat, but I don't believe the typewriter stagger presents any actual problems. Ultimatley, how we use our hands is not that symmetrical: almost everyone favours one hand over the other, after all. The stagger is just one of those arbitary asymmetries.

## Full size, TKL, 60%, or 40%

A "full size" keyboard has just over 100 keys. We can often get by on fewer keys:

- The numberpad mostly duplicates keys that's elsewhere on the keyboard already. Unless you are doing a lot of number entry, there's not a lot of loss of functionality when you lose it to go to a **T**en **K**ey**L**ess layout. A fraction of commercial keyboards are in this class.

- Some operating systems don't make a lot of us of the document navigation keys (Page Up, Insert etc.) and functions keys (F1, F2, ...). In particular, macOS does not lean on these heavily, as reflected in these keys being either absent or behind a function layer on most Apple keyboards. Losing these keys takes us down to a 60% keyboard (typically having around 60 keys).

- Some keyboards go more spartan, but removing the number row and a couple of other keys. These are typically classified as 40% keyboards. Keyboards this spartan are only really found in DIY land.

Overall, I settled on the 60% Preonic. I like that it's close to being the largest keyboard you can use without requiring you to significantly reposition your hands to reach any of the keys. Compared to 40% keyboards, it's really handy to not have to retrain yourself to find the number row (and all the symbols on it) on a function layer.

## Modifiers and the spacebar

Now we are getting into the interesting stuff. Modifier keys are those that don't do anything by themselves, but when combined with other keys, modify their functionaities. We use the `Shift` modifier to capitalise a letter, and `Control` modifier to turn the `C` key into the "Copy" command. You probably got the following modifiers on your keyboard: `Shift`, `Control`, `Alt` and the Windows or Mac Command key. Most laptop keyboards have a `Fn` modifier too.

A smaller keyboard has fewer single function keys, and thus require more modifier usage. In particular, standard keyboard layouts have between 13 and 14 key columns in the alphanumeric section: 

![14 Column keyboard](https://rahulpnath.com/images/touch_typing.gif)

Your middle and ring fingers get one column each. The index fingers split the middle four columns, at two each. The left pinkie cover the left two, and the right pinkie cover the right **four**. This is especially noteworthy to programmers, as you often use the symbols on the right most side.

A very important optimisation is, therefore, to reduce a keyboard down to 12 columns, and the right pinkie workload down to 2 columns. This is the biggest difference between 40/60% keyboards and standard layouts.

This is accomplished through an additional modifier key. You've got to find new homes for these "right-pinkie" orphans: `[]{}-=_+|'"`. I stashed most of them under `UIOPJKL;` keys, accessed by the new modifer.

The new modifier (`Raise` in Preonic firmware) sits after the `Ctrl Meta Super` trio, just before the shortened spacebar. Since most of the keys I'd want to combine the modifier sits on the right size, it's especially nice to have this under the left thumb.

## Bottom corners are for palms



## Hand mobility and flexibility

Then, there's something in there about which keys are easier to press, and which ones aren't. Can use the OLKB diagram as starting point.

There's something in there about the greater mobility you get when you are using thumb for a modifier: pivot from there. Whereas pinky modifiers do limit where you go. Thus, kind of works for shift if you use oposite hands. Otherwise a bit limited to how you work keys.

## Interesting notes:

 - Right hand is where the complicated stuff happens, as the Qwerty keyboard is quite optimised toward the left.
 - Corners are for palming.
 - Why?
