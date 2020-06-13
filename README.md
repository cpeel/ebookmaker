# EbookMaker


EbookMaker is the tool used for format conversion at Project Gutenberg.
It builds EPUB2 and Kindle files from HTML.
Also it builds HTML4, EPUB2, Kindle, and PDF files from reST sources.


## Prerequisites

* Python2 >= 2.7 or Python3 >= 3.6
* HTMLTidy (http://binaries.html-tidy.org/),
* Kindlegen (https://www.amazon.com/gp/feature.html/?docId=1000765211) or Calibre (https://calibre-ebook.com/)
* TexLive (to build from TeX), and
* groff (not sure when this is needed).

For cover generation

* Cairo https://www.cairographics.org/download/
* Noto Sans and Noto Sans CJK:
    * CentOS or RedHat: `yum install google-noto-sans-cjk-fonts; yum install google-noto-sans-fonts`
    * Ubuntu: `apt-get install fonts-noto-cjk fonts-noto`

Tested with Python 3.6

## Install

(master branch, editable install)
`pipenv install ebookmaker`

Use the ebookmaker.conf file to pass a path to your kindlegen, tex, and groff programs 
if they're not in your PATH. Edit the ebookmaker.conf and copy it to /etc/ebookmaker.conf to 
reset the paths.
Copy ebookmaker.conf to ~/.ebookmaker to override settings in /etc/ebookmaker.conf or to set default 
command line options.

## Sample invocation

(From the directory where you ran `pipenv install`)

`pipenv shell`
`ebookmaker -v -v --make=epub.images --output-dir=/Documents/pg /Documents/library/58669/58669-h/58669-h.htm`

or

`pipenv run ebookmaker -v -v --make=epub.images --output-dir=/Documents/pg /Documents/library/58669/58669-h/58669-h.htm`



## new to pipenv?

Install pipenv  (might be `pip install --user pipenv`, depending on your default python)

`$ pip3 install --user pipenv`

The default install location is `${HOME}/.local/bin`, so add this to your login shell's ${PATH} if needed.

Change directories to where you want to have your ebookmaker environment. Then, to initialize a python 3 virtual environment, do

`$ pipenv --three`

Whenever you want to enter this environment, move to this directory and do:

`$ pipenv shell`
 
Install the gutenberg modules:

`$ pipenv install ebookmaker`

Check your install:

`$ ebookmaker --version`
`EbookMaker 0.9.0`

Since you're in the shell, you can navigate to a book's directory and convert it:

`$ ebookmaker -v -v --make=epub.images --ebook 10001 --title "The Luck of the Kid" --author "Ridgwell Cullum" luck-kid.html`

## Update

`$ cd ebookmaker` to whever you ran `$ pipenv install ebookmaker`

then:

`$ pipenv update ebookmaker`

## Test

Install, as above.

`$ cd ebookmaker` to whever you ran `$ pip install ebookmaker`

then:

`$ git checkout master`

`$ pipenv install -e .`

`$ python setup.py test`

Travis-CI will run tests on branches committed in the gutenbergtools org

## Installing on Windows

To install on Windows, first install Python from
[python.org](https://www.python.org/downloads/windows/).

Next, install Microsoft Visual Studio Build Tools. Go to
[Microsoft Visual Studio Downloads](https://visualstudio.microsoft.com/downloads/),
scroll down and expand *Tools for Visual Studio 2019*, and download *Build Tools
for Visual Studio 2019*. This will download and start the Visual Studio
Installer. In the installer, select the **C++ build tools** workload and start
the install.

After that completes, install ebookmaker by starting a command line window and
running:

```
pip3 install --user ebookmaker
```

To run ebookmaker:

```
python "%APPDATA%\Python\Python38\Scripts\ebookmaker" --version
```

You will need to download and install HTML Tidy and KingleGen (links at the top
of this file) as well. They need to be on your path so ebookmaker can find them.

If you want to create book covers, you will need to install the GTK+ Toolkit.
Download and install the
[Gtk+ Runtime Environment](http://gladewin32.sourceforge.net/). It will install
to a path such as `c:\GTK+`. Add the `bin` subdirectory (eg: `c:\GTK+\bin`) to
your path as well.

### Using ebookmaker on Windows

If you are using a folder or file name that contains, the pathnames must be
enclosed in `"`, like `--output-dir="C:\your foldername"`. If pathname is
quoted, it **must not** end with trailing `\` or an error will be raised.

### Use with Guiguts

You might find it useful to create a batch file for use with Guiguts.
Example `run_ebookmaker.bat`:

```
python "%APPDATA%\Python\Python38\Scripts\ebookmaker" --version -v --make=epub.images --make=kindle.images --output-dir=%1 --title=%2 %3
```

If running the batch file from within Guiguts, you should use `$d.` rather
than `$d` (i.e. a dot after $d so quoted pathname will end in `\."` rather
than `\"`) when passing it as a value for the output-dir argument.
The corresponding "external program" setup within Guiguts would look like:

```
c:\path\to\run_ebookmaker.bat $d. $f $d$f$e
```
