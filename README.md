# Payara-env

![Build](https://github.com/jeonghanlee/Payara-env/workflows/Build/badge.svg)
![Linter Run](https://github.com/jeonghanlee/Payara-env/workflows/Linter%20Run/badge.svg)

Even if the most latest version payara-server-5.2020.3, one needs `java 8` in order to build the Payara from its github repository.
With OpenJDK 11, one can see error message such as

```bash
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.8.0:compile (default-compile) on project asadmin-audit: Compilation failure
[ERROR] /home/jhlee/gitsrc/Payara-env/Payara-src/nucleus/payara-modules/asadmin-audit/src/main/java/fish/payara/audit/admin/SetAdminAuditServiceNotifierConfiguration.java:[168,67] incompatible types: org.jvnet.hk2.config.ConfigBeanProxy cannot be converted to fish.payara.nucleus.notification.configuration.Notifier
```

## Requirements

* Java 8 : Compiling the Payara 5.192
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
├── README.txt
└── .versions
```

## Run the Payra service

* systemd service

We can use all generic systemd service commands. One can start it by `systemctl start payara`.

```bash
Payara-env (master)$ systemctl start payara
Payara-env (master)$ systemctl status payara
● payara.service - payara Service
   Loaded: loaded (/etc/systemd/system/payara.service; enabled; vendor preset: enabled)
   Active: active (exited) since Mon 2020-07-20 13:54:36 PDT; 1min 48s ago
     Docs: https://docs.payara.fish/community/docs/5.192/README.html
  Process: 14130 ExecStart=/usr/bin/java -XX:+IgnoreUnrecognizedVMOptions -jar /opt/payara/glassfish/lib/client/appserver-cli.jar start-domain productio
 Main PID: 14130 (code=exited, status=0/SUCCESS)
    Tasks: 126 (limit: 4915)
   Memory: 1.6G
   CGroup: /system.slice/payara.service
           └─14147 /usr/lib/jvm/java-1.8.0-amazon-corretto/bin/java -cp /opt/payara/glassfish/modules/glassfish.jar -XX:+UnlockDiagnosticVMOptions -XX:M
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

## Errors and Warnings

Please see [docs/README.errors.md](docs/README.errors.md)
