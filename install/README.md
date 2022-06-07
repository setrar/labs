# Install

Tutorial on how to setup a machine to use the ActiveMQ lab

## Prerequisites

This lab uses Microsoft Windows Machine

## :a: Package Managers

:round_pushpin: [ :chocolate_bar: Choco](https://chocolatey.org/install)

- [ ] In `Powershell Admin` run the command

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

:round_pushpin:  [ :superhero_man: SDKMan](https://sdkman.io/install)

- [ ] In `git bash`

```
 curl -s "https://get.sdkman.io" | bash 
```

## :b: Install tools

:tada: Using `sdk man`

:round_pushpin: Install Java

Omit Identifier to install default version 17.0.2-tem:

```
sdk install java 17.0.2-tem
```
 
 :round_pushpin: Install Maven
 
 ```
 sdk install maven
 ```
