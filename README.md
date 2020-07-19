# Payara-env

Even if the most latest version payara-server-5.2020.3, one needs `java 8` in order to build the Payara from its github repository.
With OpenJDK 11, one can see error message such as

```bash
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.8.0:compile (default-compile) on project asadmin-audit: Compilation failure
[ERROR] /home/jhlee/gitsrc/Payara-env/Payara-src/nucleus/payara-modules/asadmin-audit/src/main/java/fish/payara/audit/admin/SetAdminAuditServiceNotifierConfiguration.java:[168,67] incompatible types: org.jvnet.hk2.config.ConfigBeanProxy cannot be converted to fish.payara.nucleus.notification.configuration.Notifier
```

## Requirements

* JAVA 8

Amazon provides LTS OpenJDK at <https://aws.amazon.com/corretto>. It works well with Debian 10 without any issues.
In this repo, we use the corretto-8 version at <https://github.com/corretto/corretto-8/releases/tag/8.262.10.1>.

```bash
$ wget -c https://corretto.aws/downloads/resources/8.262.10.1/java-1.8.0-amazon-corretto-jdk_8.262.10-1_amd64.deb
$ sudo apt install ./java-1.8.0-amazon-corretto-jdk_8.262.10-1_amd64.deb
$ sudo update-alternative --config java
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                                  Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-amazon-corretto/bin/java          11100008  auto mode
  1            /usr/lib/jvm/java-1.8.0-amazon-corretto/jre/bin/java   10800262  manual mode
  2            /usr/lib/jvm/java-11-amazon-corretto/bin/java          11100008  manual mode
  3            /usr/lib/jvm/java-11-openjdk-amd64/bin/java            1111      manual mode

Press <enter> to keep the current choice[*], or type selection number: 1
```

## Build

```bash
make init
make build
```

