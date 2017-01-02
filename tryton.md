# tryton


## official webs

[tryton.org](http://www.tryton.org/)

[tryton spain](http://www.tryton-erp.es/)


[documentation core trytond](http://doc.tryton.org/4.2/trytond/doc/index.html)

[documentation client](http://doc.tryton.org/4.2/tryton/doc/index.html)

[documentation core modules](http://doc.tryton.org/4.2/modules/index.html)

## Model layer

* extends [ModelSQL](http://hg.tryton.org/trytond/file/tip/trytond/model/modelsql.py) and/or [ModelView](http://hg.tryton.org/trytond/file/tip/trytond/model/modelview.py) (sub-classing [Model](http://hg.tryton.org/trytond/file/tip/trytond/model/model.py))
* add [Fields](http://hg.tryton.org/trytond/file/tip/trytond/model/fields) as class attributes
* give it a ```__name__```
* register it in the *Pool*, normally done in ```__init__.py```_
* works similar to [active record](https://en.wikipedia.org/wiki/Active_record_pattern)
  - object instance tied to a single row of database
  - define ddl with class fields

## Fields

* [documentatino](http://doc.tryton.org/4.2/trytond/doc/ref/models/fields.html#ref-models-fields)



## Reading code

### [trytond/model/fields/Integer.py](http://hg.tryton.org/trytond/file/tip/trytond/model/fields/integer.py) 


``` python
class Integer(Field):
    '''
    Define an integer field (``int``).
    '''
    _type = 'integer'

    def sql_type(self):
        db_type = backend.name()
        if db_type == 'postgresql':
            return SQLType('INT4', 'INT4')
        elif db_type == 'mysql':
            return SQLType('SIGNED INTEGER', 'BIGINT')
        else:
            return SQLType('INTEGER', 'INTEGER')

    def sql_format(self, value):
        db_type = backend.name()
        if (db_type == 'sqlite'
                and value is not None
                and not isinstance(value, (Query, Expression))):
            value = int(value)
        return super(Integer, self).sql_format(value)


SQLType = namedtuple('SQLType', 'base type')

* extends [Field](http://hg.tryton.org/trytond/file/tip/trytond/model/fields/field.py)
* sql_type return type used in database storage it depends on the backend name.
* sql_format -> Convert the value to use as parameter of SQL queries.


