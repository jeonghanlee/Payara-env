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

## Errors

### Maven Building Error

Irregularly, I've faced the following error. it may be related with the system resources. One can try to redo with more memeory resouces, `make build.pre`, which needs more downloading time, use the local maven `make install.maven`, or all of them. It may be related with a running payara service. Please stop the servie during building procedures.

```bash
[INFO] Security Related Implementation for GlassFish 5.192  SKIPPED
[INFO] GlassFish Tests related modules 5.192 .............. SKIPPED
[INFO] btrace jar files 5.192 ............................. SKIPPED
[INFO] GlassFish Flashlight Client 5.192 .................. SKIPPED
[INFO] Flashlight 5.192 ................................... SKIPPED
[INFO] Payara Project 5.192 ............................... SKIPPED
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  04:31 min
[INFO] Finished at: 2020-07-29T23:13:40-07:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.glassfish.build:glassfishbuild-maven-plugin:3.2.20.payara-p1:exec (create-glassfish-domain) on project payara: Execution create-glassfish-domain of goal org.glassfish.build:glassfishbuild-maven-plugin:3.2.20.payara-p1:exec failed: null returned: 1 -> [Help 1]
[ERROR]
```

### Java 8 Error

Once the https is enabled, one see the following error in server.log.
Ironically, we have to run the Payara 5.192 with JAVA 11, even if we only can compile it with JAVA 8.

```bash
[2020-09-22T21:26:49.778-0700] [Payara 5.192] [WARNING] [] [org.glassfish.grizzly.filterchain.DefaultFilterChain] [tid: _ThreadID=50 _ThreadName=http-thread-pool::http-listener-2(4)] [timeMillis: 1600835209778] [levelValue: 900] [[
  GRIZZLY0013: Exception during FilterChain execution
java.lang.NoClassDefFoundError: Could not initialize class sun.security.ssl.SSLEngineImpl
  at sun.security.ssl.SSLContextImpl$AbstractTLSContext.createSSLEngineImpl(SSLContextImpl.java:610)
  at sun.security.ssl.SSLContextImpl.engineCreateSSLEngine(SSLContextImpl.java:202)
  at javax.net.ssl.SSLContext.createSSLEngine(SSLContext.java:377)
  at org.glassfish.grizzly.ssl.SSLEngineConfigurator.createSSLEngine(SSLEngineConfigurator.java:190)
  at org.glassfish.grizzly.ssl.SSLEngineConfigurator.createSSLEngine(SSLEngineConfigurator.java:162)
  at org.glassfish.grizzly.ssl.SSLBaseFilter$SSLTransportFilterWrapper.handleRead(SSLBaseFilter.java:1111)
  at org.glassfish.grizzly.filterchain.ExecutorResolver$9.execute(ExecutorResolver.java:95)
  at org.glassfish.grizzly.filterchain.DefaultFilterChain.executeFilter(DefaultFilterChain.java:260)
  at org.glassfish.grizzly.filterchain.DefaultFilterChain.executeChainPart(DefaultFilterChain.java:177)
  at org.glassfish.grizzly.filterchain.DefaultFilterChain.execute(DefaultFilterChain.java:109)
  at org.glassfish.grizzly.filterchain.DefaultFilterChain.process(DefaultFilterChain.java:88)
  at org.glassfish.grizzly.ProcessorExecutor.execute(ProcessorExecutor.java:53)
  at org.glassfish.grizzly.nio.transport.TCPNIOTransport.fireIOEvent(TCPNIOTransport.java:524)
  at org.glassfish.grizzly.strategies.AbstractIOStrategy.fireIOEvent(AbstractIOStrategy.java:89)
  at org.glassfish.grizzly.strategies.WorkerThreadIOStrategy.run0(WorkerThreadIOStrategy.java:94)
  at org.glassfish.grizzly.strategies.WorkerThreadIOStrategy.access$100(WorkerThreadIOStrategy.java:33)
  at org.glassfish.grizzly.strategies.WorkerThreadIOStrategy$WorkerThreadRunnable.run(WorkerThreadIOStrategy.java:114)
  at org.glassfish.grizzly.threadpool.AbstractThreadPool$Worker.doWork(AbstractThreadPool.java:569)
  at org.glassfish.grizzly.threadpool.AbstractThreadPool$Worker.run(AbstractThreadPool.java:549)
  at java.lang.Thread.run(Thread.java:748)
```
