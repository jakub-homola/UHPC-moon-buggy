# Creating a New Easyconfig From Scratch

Create easyconfig for `moon-buggy` software. The manual procedure is listed below.

Software:     `moon-buggy`

Homepage:     [https://github.com/seehuhn/moon-buggy](https://github.com/seehuhn/moon-buggy)

**Description**
Moon-buggy is a simple character graphics game, where you drive some kind of car across the moon's surface. Unfortunately there are dangerous craters there. Fortunately your car can jump over them!

## Manual Installation (Skip this step)

```console
$ wget https://code.it4i.cz/jar091/moon-buggy/-/archive/master/moon-buggy-master.tar.gz
$ tar xvf moon-buggy-master.tar.gz
$ cd moon-buggy-master
$ ./autogen.sh
$ ./configure --prefix=$HOME/game/moon-buggy-build
$ make
$ ls
acinclude.m4    buggy.h       config.h.in    copying.h  error.c      highscore.o  keyboard.c  main.o       meteor.o      moon-buggy.info  pager.o    README      terminal.c        title.eps     xmalloc.o
aclocal.m4      buggy.o       config.log     cursor.c   error.o      hpath.c      keyboard.o  Makefile     missing       moon-buggy.lsm   persona.c  realname.c  terminal.o        title.o       xstrdup.c
ANNOUNCE        car.img       config.status  cursor.o   game.c       hpath.o      laser.c     Makefile.am  mode.c        moon-buggy.png   persona.o  realname.o  test-score-modes  TODO          xstrdup.o
AUTHORS         ChangeLog     config.sub     darray.h   game.o       img.sed      laser.o     Makefile.in  mode.o        moon-buggy.texi  queue.c    signal.c    texinfo.tex       vclock.c
autogen.sh      checklist     configure      date.c     ground.c     INSTALL      level.c     manpage.in   moon-buggy    moon-buggy.xpm   queue.o    signal.o    text2c.sed        vclock.o
autom4te.cache  config.guess  configure.ac   date.o     ground.o     install-sh   level.o     mdate-sh     moon-buggy.6  NEWS             random.c   stamp-h1    THANKS            version.texi
buggy.c         config.h      COPYING        depcomp    highscore.c  instcmds     main.c      meteor.c     moon-buggy.h  pager.c          random.o   stamp-vti   title.c           xmalloc.c
$ ./moon-buggy
```

## Create Easyconfog From Template

* **Task**: *create easyconfig for `moon-buggy` (use template)* (Download template.eb)

```console
$ wget https://code.it4i.cz/jar091/moon-buggy/-/raw/master/easybuild/template.eb
$ cp template.eb moon-buggy-1.0.eb
```

* **Task**: *EASYBLOCK* ... choose easyblock (Analyse manual instalation - only step CONFIGURE AND MAKE -> choose easyblock `ConfigureMake`)

```python
easyblock = 'ConfigureMake'
```

* **Task**: *NAME* ... defined name of the software

```python
name = 'moon-buggy'
```

* **Task**: *VERSION* ... defined versions of the software

```python
version = "1.0"
```

* **Task**: *VERSIONSUFFIX* ... add your login

```python
versionsuffix = "-loginXXX"
```

* **Task**: *HOMEPAGE* ... homepage url

```python
homepage = 'https://github.com/seehuhn/moon-buggy'
```

* **Task**: *DESCRIPTION* ... basic software information

```python
description = """Moon-buggy is a simple character graphics game, where you drive some
kind of car across the moon's surface.  Unfortunately there are
dangerous craters there.  Fortunately your car can jump over them!"""
```

* **Task**: *TOOLCHAIN* ... choose toolchain

```python
toolchain = {'name': 'GCC', '14.3.0': ''}
```

* **Task**: *SOURCE_URLS* ... source urls

```python
source_urls = ['https://code.it4i.cz/jar091/moon-buggy/-/archive/%(version)s/']
```

* **Task**: *SOURCES* ... package name definition

```python
sources = ['%(name)s-%(version)s.tar.gz']
```

* **Task**: *PRECONFIGOPTS* ... autogen.sh

```python
preconfigopts = "./autogen.sh && "
```

* **Task**: *BUILDDEPENDENCY*

```python
('Autoconf', '2.69')
```

* **Task**: *DEPENDENCY*

```python
 ('ncurses', '6.1'),
```

* **Task**: *SANITY_CHECK_PATH* ... you must check exists binary file

```python
sanity_check_paths = {
    'files': ['bin/moon-buggy', 'com/moon-buggy/mbscore'],
    'dirs': ['bin', 'com', 'share'],
}
```

* **Task**: *MODULECLASS* ... choose class

```python
moduleclass = 'tools'
```

* **Task**: *install `moon-buggy` from easyconfig*

```console
$ eb moon-buggy-1.0.eb -r
== temporary log file in case of crash /tmp/eb-ctAvZY/easybuild-GQkRPM.log
== resolving dependencies ...
== processing EasyBuild easyconfig /home/loginXXX/game/moon-buggy-1.0.eb
== building and installing moon-buggy/1.0-loginXXX...
== fetching files...
...
...
== COMPLETED: Installation ended successfully
== Results of the build can be found in the log file(s) /home/loginXXX/.local/easybuild/software/moon-buggy/1.0-loginXXX/easybuild/easybuild-moon-buggy-1.0-20181016.094918.log
== Build succeeded for 1 out of 1
== Temporary log file(s) /tmp/eb-ctAvZY/easybuild-GQkRPM.log* have been removed.
== Temporary directory /tmp/eb-ctAvZY has been removed.
```

* **Task**: *load module and run `moon-buggy`*

```console
$ ml moon-buggy/1.0-loginXXX
$ moon-buggy
```
