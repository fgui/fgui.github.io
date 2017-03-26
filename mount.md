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
(defstate x :start :anything :stop (println x))

start
```clojure 
(mount.core/start)
(mount.core/stop)
```
