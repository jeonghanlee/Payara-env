# Errors


## Maven Building Error

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

## Java 8 Error

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


## Java Prefs Warnings

Payara service is running with `payara` user within systemd, so it doesn't have permissions to access `/etc/.java/.systemPrefs/`. Thus, we added the extrac java option `-Djava.util.prefs.userRoot=/opt/payara/5.192/prefs` to Payara java_options within `domain.xml` file to remove the following messages within `server.log`. 

```bash
2020-09-23T14:18:18.954-0700] [Payara 5.192] [WARNING] [] [java.util.prefs] [tid: _ThreadID=464 _ThreadName=Timer-1] [timeMillis: 1600895898954] [levelValue: 900] [[
  Could not lock User prefs.  Unix error code 2.]]

[2020-09-23T14:18:18.955-0700] [Payara 5.192] [WARNING] [] [java.util.prefs] [tid: _ThreadID=464 _ThreadName=Timer-1] [timeMillis: 1600895898955] [levelValue: 900] [[
  Couldn't flush user prefs: java.util.prefs.BackingStoreException: Couldn't get file lock.]]
```
