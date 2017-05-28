

# In Terminal

```bash
export PATH=/opt/local/bin:/opt/local/sbin:$PATH
sudo port selfupdate
sudo port install pkgconfig
export PATH=/opt/pkgconfig/bin:$PATH
sudo port install gtk2 +x11
export PKG_CONFIG_PATH=/opt/local/lib/pkgconfig

#R CMD INSTALL ~/Downloads/RGtk2_2.20.31.tar.gz ## nope
#R CMD INSTALL ~/Downloads/cairoDevice_2.24.tar.gz ## nope
```

## Building Building `GTK` () on macOS  via `jhbuild`

The following process is adapted from [this wiki](https://wiki.gnome.org/Projects/GTK%2B/OSX/Building)

Download the following shell script (executable via the `sh` terminal command) and save it in your "home" directory ("`~/`" or "`/Users/#<USERNAME>#/`" - replace "`#<USERNAME>#`" with your username on you machine):  https://git.gnome.org/browse/gtk-osx/plain/gtk-osx-build-setup.sh

Then run the following command sequence in Terminal.app (or your favorite alternative shell application  (e.g., iTerm)). Note that this process takes quite a while, so be prepared to let it run a while (i.e., if you are on a laptop, make sure your machine is plugged in to a power source and that you don't need to close or logout any time soon (at least 30 minutes, based on the time it is taking me to run the sequence while writing this). Also, make sure that your current working directory is the same as where you saved the shell script above

```bash
sudo sh gtk-osx-build-setup.sh
## enter user password when prompted ##

## I added the next command based on a prompt message resulting from the previous command ##

export PATH=/Users/#<USERNAME># ## again, replace "#<USERNAME>#" with your username ##
	/.local/bin:$PATH

##
jhbuild bootstrap ## takes a while ## ## returns an error that "intltool meta-bootstrap" was not installed ##
jhbuild build meta-gtk-osx-bootstrap meta-gtk-osx-core ## returns same error as above ##
jhbuild bootstrap ## returns same error as above ##
```

## To also add correct PATH to `~/.bash_profile` & `~/.bashrc`:

### For `~/.bash_profile`

1. Open the two files in TextEdit (or whatever you prefer)

```bash
open -a TextEdit ~/.bash_profile
open -a TextEdit ~/.bashrc
```

2. Add the following line to each of the opened documents (as before, replace "#<USERNAME>#"> with your username on your machine):

"
export PATH=/Users/#<USERNAME>#
	/.local/bin:$PATH
"

Save and close each file. To make those changes official, you'll need to `source` your `~./bashrc` file and restart the terminal application:

```bash
source ~/.bashrc
```


# In `R` (`v3.4.0`):

```r
Sys.setenv(PATH=paste0("/opt/pkgconfig/bin:",Sys.getenv("PATH")))
Sys.setenv(PATH=paste0("/Users/#<USERNAME>#
	/.local/bin:",Sys.getenv("PATH")))
Sys.setenv(PKG_CONFIG_PATH="/opt/local/lib/pkgconfig")
```

Try installing `RGtk2` package in `R`:

```r
install.packages("RGtk2", type="source") ## nope
install.packages("cairoDevice", type="source") ## nope


Sys.getenv("PKG_CONFIG_PATH")
Sys.setenv(PKG_CONFIG_PATH="/Library/Frameworks/GTK+.framework/Versions/2.24.X11/Resources/lib/pkgconfig")
install.packages("RGtk2", type="source") ## nope
```

Uninstall `R` (`v3.4.0`) completely:

```bash
sudo rm -rf /Library/Frameworks/R.framework/Applications/R.app
sudo rm -rf /usr/bin/R /usr/bin/Rscript
```

I gave up at this point at reinstalled the previous version of `R` (`v3.3.0`).
