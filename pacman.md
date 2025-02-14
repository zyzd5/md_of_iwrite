* `S`, --`sync`
    * `c`, --`clean`: Remove packages that no longer installed
    * `i`, --`info`: Display information on a given package, -`ii` to displaypackages that depend on this package
    * `s`, --`search` 'regexp' :
    * `u`, --`sysupgrade`: upgrade all package, `-Suu` for downgrade package to lower version, `-Su foo` to upgrade `foo` package 
    * `y`, --`refresh`: download a fresh copy from the server, typically be used -`yu`, -`yy` will force a refresh of all package, even if they were up-to-date

* -`Q`, --`query`
    * `i`, --`info`: Display information on a given package
    * `s`, --`search` 'regexp' :

* -`R`, --`remove`           
    * `n`, --`nosave`: when removing a package, by default, pacman will save the config-file to .pacsave file, passing a `-n` to ignore file_backup
    * `s`, --`recursive`: Remove target package and its dependencies
    * `u`, --`unneeded`: Removes targets that are not required by any other packages

* -`D`, --`database`: will learn it
