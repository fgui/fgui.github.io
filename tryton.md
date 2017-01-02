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
* register it in the *Pool*, normally done in ```__init__.py```
* works similar to [active record](https://en.wikipedia.org/wiki/Active_record_pattern)
  - object instance tied to a single row of database
  - define ddl with class fields

## Fields

* [documentation](http://doc.tryton.org/4.2/trytond/doc/ref/models/fields.html#ref-models-fields)



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
```

* extends [Field](http://hg.tryton.org/trytond/file/tip/trytond/model/fields/field.py)
* sql_type return type used in database storage it depends on the backend name.
* sql_format -> Convert the value to use as parameter of SQL queries.

## Bootstrapping

## [Werkzeug](http://werkzeug.pocoo.org/) The Python [WSGI](https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface) Utility Library

``` ./trytond/bin/trytond -c config.conf  ```

[trytond init](http://hg.tryton.org/trytond/file/tip/bin/trytond)

``` python
import sys
import os
import glob

from werkzeug.serving import run_simple

DIR = os.path.abspath(os.path.normpath(os.path.join(__file__,
    '..', '..', 'trytond')))
if os.path.isdir(DIR):
    sys.path.insert(0, os.path.dirname(DIR))

import trytond.commandline as commandline
from trytond.config import config, split_netloc

parser = commandline.get_parser_daemon()
options = parser.parse_args()
commandline.config_log(options)
config.update_etc(options.configfile)

# Import trytond things after it is configured
from trytond.application import app
from trytond.pool import Pool
from trytond.modules import get_module_list, get_module_info

with commandline.pidfile(options):
    for name in options.database_names:
        Pool(name).init()
    hostname, port = split_netloc(config.get('web', 'listen'))
    static_files = {
        '/': config.get('web', 'root'),
        }
    certificate = config.get('ssl', 'certificate')
    privatekey = config.get('ssl', 'privatekey')
    if certificate or privatekey:
        ssl_context = (certificate, privatekey)
    else:
        ssl_context = None
    extra_files = options.configfile
    for module in get_module_list():
        info = get_module_info(module)
        path = os.path.join(info['directory'], 'view', '*.xml')
        extra_files.extend(glob.glob(path))
    run_simple(hostname, port, app,
        threaded=True,
        extra_files=extra_files,
        static_files=static_files,
        ssl_context=ssl_context,
        use_reloader=options.dev)

```
