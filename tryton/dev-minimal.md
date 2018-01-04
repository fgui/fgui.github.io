---
layout: page
title: tryton: basic setup
---

# Getting started with Tryton development.
## Minimal setup

This is installing from 0 'by hand'. Most consulting companies have some kind of method (via invoke or other)
that installs from a series of setup files with install modules, patches etc.
As far as I can tell there is no a standard script to do this in the tryton
community.

Install trytond (server) and tryton (client) with/without extra modules.
Assuming postgres already installed.


### Requirements trytond (server)

https://github.com/tryton/trytond/blob/develop/doc/topics/install.rst

create a *virtual environment* and install:

```
  pip install Werkzeug
  pip install relatorio
  ;; pip install wsgi
  pip install wrapt
  pip install Genshi
  pip install polib
  pip install datautil
  pip install python-sql
  pip install psycopg2
  pip install lxml
  pip install bcrypt
  ;; for all the modules
  pip install ldap3
  pip install python-stdnum
  pip install simpleeval
  pip install stripe
  ?pip install coda
  pip install febelfin-coda
  pip install zeep
  pip install PyPDF2

```

### requirements tryton (client)

https://github.com/tryton/tryton/blob/develop/doc/installation.rst

no virtualenv due to gtk library difficult to install/use under virtualenv.

create a folder for your workspace and clone server and client repositoris

### with modules via hgnested

hg nclone http://hg.tryton.org/trytond


### minimal install (no modules)
```
hg clone https://hg.tryton.org/trytond
```

### install client
```
hg clone https://hg.tryton.org/tryton
```

### or use git/github mirrors

```
git clone git@github.com:tryton/trytond.git
git clone git@github.com:tryton/tryton.git
```

### setup trytond

create a minimal trytond.conf inside trytond folder to use posgresql (instead of sqllite)

```
[database]
uri=postgresql:///
```

https://github.com/tryton/trytond/blob/develop/doc/topics/setup_database.rst

create db postgres and initialize it
```
createdb minimal-tryton (from trytond)

./bin/trytond-admin -v -c trytond.conf  -d minimal-tryton  -u ir res
```

### Start server and client

start server (from trytond)
```
./bin/trytond -v -c trytond.conf
```

start client (from tryton) (from outside the virtual env)
```
./bin/tryton
```

#### Create a module under /trytond/modules

install the module
```
./bin/trytond-admin -c trytond.conf -d minimal-tryton -u hello
```

### Documentation
make the docs (pdf) for trytond and tryton

requirements:

```
pip install sphinx
sudo apt-get install latexmk
```

build pdf:

```
cd doc
make latex
cd _build/latex
make all-pdf
```
