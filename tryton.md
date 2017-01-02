# tryton


## official webs

[tryton.org](http://www.tryton.org/)

[tryton spain](http://www.tryton-erp.es/)


[documentation core trytond](http://doc.tryton.org/4.2/trytond/doc/index.html)

[documentation client](http://doc.tryton.org/4.2/tryton/doc/index.html)

[documentation core modules](http://doc.tryton.org/4.2/modules/index.html)

## Model layer

* sub-class [ModelSQL](http://hg.tryton.org/trytond/file/tip/trytond/model/modelsql.py) and/or [ModelView](http://hg.tryton.org/trytond/file/tip/trytond/model/modelview.py) (sub-classing [Model](http://hg.tryton.org/trytond/file/tip/trytond/model/model.py))
* add [Fields](http://hg.tryton.org/trytond/file/tip/trytond/model/fields) as class attributes
* give it a ```__name__```
* register it in the *Pool*, normally done in ```__init__.py```_
* works similar to [active record](https://en.wikipedia.org/wiki/Active_record_pattern)
  - object instance tied to a single row of database
  - 
