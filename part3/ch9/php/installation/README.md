


## :gear: Install

- [ ] To install `php` in Powershell

```
choco install php
```

- [ ] To enable SSL, open  `/c/tools/php81/php.ini` and add the below line

```
extension=C:\tools\php81\ext\php_openssl.dll
```

- [ ] On windows, open `C:\Program Files\Git\bin\bash.exe` in the search bar to avoid the `STDIN not a tty` issue


- [ ] In your home directory, run the command to install `Composer`
```
 wget https://raw.githubusercontent.com/composer/getcomposer.org/76a7060ccb93902cd7576b67264ad91c8a2700e2/web/installer -O - -q | php -- --quiet 
``` 

- [ ] Put the composer binary on your PATH

```
mkdir ${HOME}/bin && mv composer.phar ${HOME}/bin/composer 
```

# References

- [ ] [Composer installation error - output is not a tty, input is not a tty](https://stackoverflow.com/questions/33622087/composer-installation-error-output-is-not-a-tty-input-is-not-a-tty)
