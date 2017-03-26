---
layout: page
title: About mount
---

[official doc](https: //github. com/tolitius/mount/blob/master/README. md)

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

