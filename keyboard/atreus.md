---
layout: page
title: Atreus keyboard Firmware AltGr
---
## Firmware changes to qwerty to add AltGr

https://github.com/fgui/tmk_keyboard/blob/atreus/keyboard/atreus/keymap_qwerty_altgr.c

Main reason to be able to use Colemak with languages that require AltGr+Letter combinations.

Changes from original qwerty layout.

Tab -> AltGr (Right Alt)
fn+Tab -> Tab


I wanted to be able to DEL when editing text outside emacs without moving L2 some times:
fn+space -> delete


Note: When uploading the changes I got confuse reading the docs. To find out the /dev/xxxxx you must turn on and off bootloading not disconnect the keyboard.
