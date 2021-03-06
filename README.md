KindlePDFViewer
===============

This is a document viewer application, created for usage on the Kindle e-ink reader.
It is currently restricted to 4bpp inverse grayscale displays. For PDF files
it is using the muPDF library (see http://mupdf.com/), for DjVu files djvulibre library
and for ebooks (fb2, mobi, ePub, etc) crengine. It can also read JPEG images using
libjpeg library. The user interface is scripted using Lua (see http://www.lua.org/).

The application is licensed under the GPLv3 (see COPYING file).


Building
========

Follow these steps:

* fetch thirdparty sources
	* manually fetch all the thirdparty sources:
		* init and update submodule koreader-base
		* within koreader-base:
			* install muPDF sources into subfolder "mupdf"
			* install muPDF third-party sources (see muPDF homepage) into a new
			  subfolder "mupdf/thirdparty"
			* install libDjvuLibre sources into subfolder "djvulibre"
			* install CREngine sources into subfolder "kpvcrlib/crengine"
			* install LuaJit sources into subfolder "luajit-2.0"
			* install popen_noshell sources into subfolder "popen-noshell"
			* install libk2pdfopt sources into subfolder "libk2pdfopt"

	* automatically fetch thirdparty sources with Makefile:
		* make sure you have patch, wget, unzip, git and svn installed
		* run `make fetchthirdparty`.

* adapt Makefile to your needs

* run `make thirdparty`. This will build MuPDF (plus the libraries it depends
  on), libDjvuLibre, CREngine, libk2pdfopt and Lua.

* run `make`. This will build the koreader-base application


Running
=======

In real eink devices
---------------------
The user interface is scripted in Lua. See "reader.lua".
It uses the Linux feature to run scripts by using a corresponding line at its
start.

So you might just call that script. Note that the script and the koreader-base
binary currently must be in the same directory.

You would then just call reader.lua, giving the document file path, or any
directory path, as its first argument. Run reader.lua without arguments to see
usage notes.  The reader.lua script can also show a file chooser: it will do
this when you call it with a directory (instead of a file) as first argument.


In emulator
-----------
You need to first compile koreader-base in emulation mode.
  * If you have built kindlepdfviewer in real mode before, you need to
    clean it up:

```
make clean && make cleanthirdparty
```

  * Then compile with emulation mode flag:

```
EMULATE_READER=1 make
```

  * You may want to see README.md in koreader-base for more information.


Next run `make bootstrapemu` to setup basic runtime environment needed by
emulation mode. A new emu directory will be created.


Last, run the emulator with following command:
```
cd emu && reader.lua -d ./
```
