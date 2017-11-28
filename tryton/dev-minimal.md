---
layout: page
title: minimal setup development tryton
---

# Getting started with Tryton development.
## Minimal setup
install trytond (server) and tryton (client) without extra modules.
assuming postgres already installed.

### requirements trytond (server)

https://github.com/tryton/trytond/blob/develop/doc/topics/install.rst

create a virtual environment and install:

```
  pip install Werkzeug
  pip install relatorio
  pip install wsgi
  pip install wrapt
  pip install Genshi
  pip install polib
  pip install datautil
  pip install python-sql
  pip install psycopg2
  pip install lxml
```

### requirements tryton (client)

https://github.com/tryton/tryton/blob/develop/doc/installation.rst

no virtualenv due to gtk library difficult to install/use under virtualenv.

create a folder for your workspace and clone server and client repositoris

hg clone https://hg.tryton.org/trytond
hg clone https://hg.tryton.org/tryton

or use git/github mirrors

git clone git@github.com:tryton/trytond.git
git clone git@github.com:tryton/tryton.git


### setup trytond

create a minimal trytond.conf inside trytond to use posgresql (instead of sqllite)

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

test it

start server (from trytond)
```
./bin/trytond -v -c trytond.conf
```

start client (from tryton) (from outside the virtual env)
```
./bin/tryton
```

create a module under /trytond/modules

install the module
```
./bin/trytond-admin -c trytond.conf -d minimal-tryton -u hello
```

### documentation
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
