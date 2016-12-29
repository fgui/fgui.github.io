# About clojure.test


clojure.test is the official unit test framework for clojure. Here are some notes to complement the official docs.

[official documentation](https://clojure.github.io/clojure/clojure.test-api.html)


## lein

How to auto run the tests in your project

```clojure
;; include plugin in your project.clj
  :plugins [[lein-auto "0.1.2"]]
```

```bash
lein auto test
```


```clojure
;; typical require content for testing
(:require [clojure.test :refer [is testing deftest]])`


(deftest example-test [])
```

## emacs cider

```
C-c M-j cider-jack-in 
C-c C-x cider-refresh
C-c C-k cider-load-buffer
C-c C-t C-p cider-run-project-tests
```

#assertions for throwables


There are 2 special assertions for Throwables. 

`is` behave differently base on the first symbol of the list being given. 
That means that `throw?` and `throw-with-msg?` are not functions or macros or special forms but just symbols being processed by the is macro.
This may confuse some IDEs that expect this symbols to be functions or macros or special forms. 
