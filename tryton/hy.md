---
layout: page
title: hylang tryton
---

# writting tryton modules with hy

## why?

Lisp rules and tryton (written in python) is an open source erp with many modules on it.
Wouldn't it be could to extend it with a Lisp. Thanks hy we can.


## My experience so far...

A hello and hello-world module as a proof of concept.

## Installation

Install trytond the usual way but add hy via pip install at the end.

```
pip install git+https://github.com/hylang/hy.git
```

## Writing hello
xml files and __init__.py as usual (with python).
[hello.hy](https://github.com/fgui/hy-tryton-hello/blob/master/hello.hy) instead of hello.py

``` hy
(import [trytond.model [ModelSQL ModelView fields]])
(def --all-- ["Hello"])

(defclass Hello [ModelSQL ModelView]
  "Hello World"
  [--name-- "hello"
   name (.Char fields "Name" :required True)
   greeting (.Function fields (.Char fields "Greeting") "get_greeting")]

  (defn get-greeting [self name]
    (.format "Hello {}" self.name)))
```

## Writing hello-word
[hello.hy](https://github.com/fgui/hy-tryton-hello_world/blob/master/hello.hy) instead of hello.py

``` hy
(import [trytond.pool [PoolMeta]])
(import [trytond.model [fields]])
(def --all-- ["Hello"])

(defclass Hello []
  "Hello World with surname"
  [--name-- "hello"
   --metaclass-- PoolMeta
   surname (.Char fields "Surname")]

  (defn get-greeting [self name]
    (setv su (super Hello self)
          res (.get_greeting su name))
    (if self.surname
      (+ res " " self.surname)
      res)))
```