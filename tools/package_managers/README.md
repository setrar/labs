# :gear: Install


## :a: Package Managers

:round_pushpin: [ :chocolate_bar: Choco](https://chocolatey.org/install)

:desktop_computer: In `Powershell` Admin terminal, run the command

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

:round_pushpin:  [ :superhero_man: SDKMan](https://sdkman.io/install)

- [ ] In `git bash`

```
 curl -s "https://get.sdkman.io" | bash 
```

## :b: Install Development Tools

:desktop_computer: Using `choco` in `Powershell` admin terminal

:round_pushpin: Install `git bash`to get :shell: `shell`  access and `git` to control the source code.

```
choco install git
```

:round_pushpin: Install MySQL Workbench
 
```
choco install mysql.workbench
```


:desktop_computer: Using `sdk man` in `git bash` terminal

:round_pushpin: Install Java Compiler

Omit Identifier to install default version 17.0.2-tem:

```
sdk install java 17.0.2-tem
```

```
sdk install java 11.0.15-tem
```

```
sdk use java 11.0.15-tem
```


 :round_pushpin: Install Maven software project management
 
 ```
 sdk install maven
 ```
 
 
