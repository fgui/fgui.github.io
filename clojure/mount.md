---
layout: page
title: About mount
---

## Docs

[official doc](https://github.com/tolitius/mount/blob/master/README.md)

[github pagem](https://github.com/tolitius)

## Code

dependencies project.clj
```clojure
[mount "0.1.11"]
```

require
```clojure 
[mount.core :refer [defstate]]
```

state
```clojure
(defstate conn :start (create-conn) :stop (diconnec conn))
```

use state from another ns
```clojure
(:require [a-ns :refer [conn])
```

start
```clojure 
(mount.core/start)
(mount.core/stop)
```

swap state
```clojure
(mount/start-with {#'app.db/conn test-conn'})
```

## Posts about component and mount

From creator (Anatoly Polinsky - tolitius) of mount: 
[No Ceremony](https://www.dotkam.com/2016/11/21/no-ceremony/)

From (Dmitri Sotnikov - yoghos) (Luminus)
[Contrasting Component and Mount](http://yogthos.net/posts/2016-01-19-ContrastingComponentAndMount.html)
