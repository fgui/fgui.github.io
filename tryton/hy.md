---
layout: page
title: tryton-hy: hello
---

# writting tryton modules with hy

## why?

Lisp rules and tryton (written in python) is an open source erp with many modules on it.
Wouldn't it be could to extend it with a Lisp. Thanks hy we can.


## My experience so far...

Writting a few modules as a proof of concept. I am using these to learn hy and tryton at the same time.

## Installation

Install trytond the usual way but add hy via pip install at the end.

```bash
pip install git+https://github.com/hylang/hy.git
```


## Learnning Modules
Each module concentrates on a different concept.

### hello
Basic Module with a simple Model and a function field on the module.

[hello 4.4+](https://github.com/fgui/hy-tryton-hello)

[hello 4.0](https://github.com/fgui/hy-tryton-hello/tree/4.0)

xml files and __init__.py as usual (with python).
[hello.hy](https://github.com/fgui/hy-tryton-hello/blob/master/hello.hy) instead of hello.py

```hy
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

### hello-word
Extending hello to add a field

[hello-world](https://github.com/fgui/hy-tryton-hello_world)

```hy
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

### hello-history
Extending hello to support history

[hello-history](https://github.com/fgui/hy-tryton-hello_history)

### hello-active
Extending hello to support active

[hello-active](https://github.com/fgui/hy-tryton-hello_active)

### hello-company-prefix
Extenging hello to add a company field. Prefix field diferent for each company - multi-company

[hello-company-prefix post 4.4 with MultiValue](https://github.com/fgui/hy-tryton-hello_company_prefix)

[hello-company-prefix pre 4.4 with Prototype](https://github.com/fgui/hy-tryton-hello_company_prefix/tree/4.0)

### motto
Testing multi-company. The model instances are only visible for the users of the company.
The model has a field company which will be filter by using a rule.

[motto](https://github.com/fgui/hy-tryton-motto)