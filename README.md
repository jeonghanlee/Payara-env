# Payara-env

![Build](https://github.com/jeonghanlee/Payara-env/workflows/Build/badge.svg)
![Linter Run](https://github.com/jeonghanlee/Payara-env/workflows/Linter%20Run/badge.svg)

This is the Payara 5.192 configuration environment with CentOS 8 and Debian 10. It may works with other versions (more latest one), which is not tested.

## Requirements

* Java 8  : Compiling the Payara 5.192
* Java 11 : Running the Payara 5.192
* Maven 3

Please check all necessary JAVA environment at <https://github.com/jeonghanlee/java-env>

## Build

There is no running payara or glassfish service in a system. Please check it `systemctl status payara` or its relevant tools.

```bash
Payara-env (master)$ make vars
Payara-env (master)$ make init
Payara-env (master)$ make build
```

## Installation

```bash
Payara-env (master)$ make install

Payara-env (master)$ make exist
tree -aL 1 /opt/payara/5.192
/opt/payara/5.192
├── bin
├── glassfish
├── h2db
├── javadb
├── META-INF
├── mq
├── prefs
├── README.txt
└── .versions
```

## Reinstallation

If one would like to reinstall everything from scratch, please run `make reinstall`. It does `make uninstall` and `make install`.
Thus, old payara installation will be replaced with the new one completely. All web application will be removed.

```bash
Payara-env (master)$ make reinstall
```

## Run the Payra service

* systemd service

We can use all generic systemd service commands. One can start it by `systemctl start payara`.

```bash
Payara-env (master)$ systemctl start payara
Payara-env (master)$ systemctl status payara
● payara.service - payara Service
   Loaded: loaded (/etc/systemd/system/payara.service; enabled; vendor preset: enabled)
   Active: active (exited) since Wed 2020-09-23 14:58:58 PDT; 32min ago
     Docs: https://docs.payara.fish/community/docs/5.192/README.html
  Process: 934 ExecStart=/opt/java-env/JDK11/bin/java -XX:+IgnoreUnrecognizedVMOptions -jar /opt/payara/5.192/glassfish/lib/client/appserver-cli.jar start-domain production (code=exi
 Main PID: 934 (code=exited, status=0/SUCCESS)
    Tasks: 131 (limit: 4915)
   Memory: 1.0G
   CGroup: /system.slice/payara.service
           └─1411 /opt/java-env/JDK11/bin/java -cp /opt/payara/5.192/glassfish/modules/glassfish.jar -XX:+UnlockDiagnosticVMOptions --add-opens=jdk.management/com.sun.management.inte
           .....
```

* Web site

<http://localhost:4848/>

|![Payara Server](docs/payara_server.png)|
| :---: |
|**Figure 1** Payara Server Web Screenshot.|

## Rules

```bash
make sd_start          : systemctl start payara
make sd_status         : systemctl status payara
make sd_stop           : systemctl stop payara
make sd_restart        : systemctrl restart payara
make uninstall         : Uninstall and remove the payara
make install.maven     : Install and set it up the local MAVEN version in .maven path
make clean.maven       : Remove the local MAVEN
make compile           : Compile Payara
make compile.post      : Update configurations, and add MariaDB JTBC connector
make build.pre         : Clean up .m2/repository/glassfish and others
```

## Production

This payara environment only run the production domain through systemd service. Thus, `systemctl start payara` means `asadmin start-domain production`. Thus, the default payara `jvm_options` memory options are large such as

```bash
# Original Configuration
JAVA_HEAPSIZE="2g"
MAX_METASPACE_SIZE="2g"
```

However, this is too much for my personal computer, so I reduce them to

```bash
NEW_JAVA_HEAPSIZE="1g"
MAX_METASPACE_SIZE="512m"
```

Therefore, if one would like to deploy it within a production environment, please add the relevant memory size in `configure/CONFIG_SITE.local`.
In addtion, the default MASTER and ADMIN passwords are not good, so, please use the secure passowrds for them also. Here is the example `CONFIG_SITE.local` file as follows:

```bash
# Revert the original PayaraConfiguration
JAVA_HEAPSIZE="2g"
NEW_JAVA_HEAPSIZE="2g"
MAX_METASPACE_SIZE="2g"

MASTER_PASSWORD:=thisissecurepassword
ADMIN_PASSWORD:=thisissecurepassword
```

Note that `_PASSWORD` varialbes within several places in `Makefile` environment through variables and shell environment. Please make sure special characters can be handled by them together properly.

## Errors and Warnings

Please see [docs/README.errors.md](docs/README.errors.md)
