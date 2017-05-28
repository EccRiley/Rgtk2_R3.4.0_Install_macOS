# Dealing with `GTK2` \& `RGtk2` Installation \& Setup on `Mac OS X`/`macOS` Systems^[Primary source: http://marcoghislanzoni.com/blog/2014/08/29/solved-installing-rattle-r-3-1-mac-os-x-10-9/]

Note that this document is written with instructional purposes in mind for my research team, so some commentary may be less relevant to finding the solution than it is to explaining the various commands and processes for those less comfortable with the command line. BUT: Please (please, please) comment/correct inaccuracies in my explanations, as I am still relatively new to programming overall and definitely want to avoid spreading misinformation.

```bash
export PATH=/opt/local/bin:/opt/local/sbin:$PATH ## adds "`/opt/local/bin`" & "`opt/local/sbin`" to your "`$PATH`" variable, which tells the terminal where to look for executable files (FYI: For future reference, individual entries (i.e., paths to executables) in the `$PATH` variable are separated by "`:`") ##


## When prompted for a password after running any of the commands below, enter the *password* (not username) that you use to login to the machine you are currently using ##
## The reason you're prompted for your password is because of the "`sudo`" argument at the beginning of some of the below commands, which tells the terminal to execute those command "as `root`" (i.e., as an administrator) ##

sudo port selfupdate ## updates the _`macports`_ library ##
sudo port upgrade outdated ## (1) you will likely see a warning message after running the previous command telling you to run this command, which updates all of the packages/programs installed via the `macports` library after having updated your local `macports` library (i.e., after having run the previous command) ##
## Fair warning: The latter command can take a while, depending on the number of programs installed on your maching via the `macports` library, but it is generally a good idea to run this regardless, as updates to these packages/programs are not automatically patched to end-users (i.e., you will never get a notification on you computer about available updates to these packages in the way that you would for, say, `macOS` system software updates or updates to applications installed via the Mac App Store) ##

sudo port install pkgconfig ## install the `pkgconfig` program via the `macports` library ##

export PATH=/opt/pkgconfig/bin:$PATH ## add the `pkgconfig` executable's path to your $PATH variable ##

sudo port install gtk2 +x11 ## install the `gtk2` & `x11` programs via the `macports` library ##
export PKG_CONFIG_PATH=/opt/local/lib/pkgconfig ## add the `$PKG_CONFIG_PATH` variable, which should now lead to the `pkgconfig`, `gtk2`, & `x11` executables to your user `profile` the `pkgconfig` path
```

## STOP !!

1. Visit the following link and click on the download link for the "Package Source" file (the one that ends with ".tar.gz"): https://cran.r-project.org/web/packages/RGtk2/
2. Do the same at this link: http://cran.r-project.org/web/packages/cairoDevice
3. Adjust the file paths in the next couple of commands to the correct file location of the downloaded source files.
4. Run the following two commands in the `Terminal` app

(_Note: the following two commands are actually `R` commands executed from the `Terminal` app - pretty cool, huh?!_ :) )

```bash
R CMD INSTALL ~/Downloads/RGtk2_xx.yy.z.tar.gz
R CMD INSTALL ~/Downloads/cairoDevice_xx.yy.z.tar.gz
```

Now open `R` and run the following

```{r}
Sys.setenv(PATH=paste0("/opt/pkgconfig/bin:",Sys.getenv("PATH")))
Sys.setenv(PKG_CONFIG_PATH="/opt/local/lib/pkgconfig")

install.packages("RGtk2", type="source")
install.packages("cairoDevice", type="source")
```
