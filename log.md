
# Log information

```bash
Payara-src/appserver/packager/docker/target/docker.zip


[INFO] --- glassfishbuild-maven-plugin:3.2.20.payara-p1:exec (create-glassfish-domain) @ payara ---
[INFO] executable: /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/stage/payara5/bin/asadmin
[INFO] commandLineArgs: --user admin create-domain --template=/home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/stage/payara5/glassfish/common/templates/gf/appserver-domain.jar --nopassword --savelogin=true --checkports=false --adminport 4848 --instanceport 8080 --keytooloptions CN=localhost domain1
[INFO] [exec] Using port 4848 for Admin.
[INFO] [exec] Using port 8080 for HTTP Instance.
[INFO] [exec] Using default port 7676 for JMS.
[INFO] [exec] Using default port 3700 for IIOP.
[INFO] [exec] Using default port 8181 for HTTP_SSL.
[INFO] [exec] Using default port 3820 for IIOP_SSL.
[INFO] [exec] Using default port 3920 for IIOP_MUTUALAUTH.
[INFO] [exec] Using default port 8686 for JMX_ADMIN.
[INFO] [exec] Using default port 6666 for OSGI_SHELL.
[INFO] [exec] Using default port 9009 for JAVA_DEBUGGER.
[INFO] [exec] Distinguished Name of the self-signed X.509 Server Certificate is:
[INFO] [exec] [CN=localhost,OU=Payara,O=Payara Foundation,L=Great Malvern,ST=Worcestershire,C=UK]
[INFO] [exec] Distinguished Name of the self-signed X.509 Server Certificate is:
[INFO] [exec] [CN=localhost-instance,OU=Payara,O=Payara Foundation,L=Great Malvern,ST=Worcestershire,C=UK]
[INFO] [exec] Domain domain1 created.
[INFO] [exec] Domain domain1 admin port is 4848.
[INFO] [exec] Domain domain1 allows admin login as user "admin" with no password.
[INFO] [exec] Login information relevant to admin user name [admin]
[INFO] [exec] for this domain [domain1] stored at
[INFO] [exec] [/home/jhlee/.gfclient/pass] successfully.
[INFO] [exec] Make sure that this file remains protected.
[INFO] [exec] Information stored in this file will be used by
[INFO] [exec] administration commands to manage this domain.
[INFO] [exec] Command create-domain executed successfully.
[INFO]
[INFO] --- glassfishbuild-maven-plugin:3.2.20.payara-p1:exec (create-production-domain) @ payara ---
[INFO] executable: /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/stage/payara5/bin/asadmin
[INFO] commandLineArgs: --user admin create-domain --template=/home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/stage/payara5/glassfish/common/templates/gf/production-domain.jar --nopassword --savelogin=true --checkports=false --adminport 4848 --instanceport 8080 --keytooloptions CN=localhost production
[INFO] [exec] Using port 4848 for Admin.
[INFO] [exec] Using port 8080 for HTTP Instance.
[INFO] [exec] Using default port 7676 for JMS.
[INFO] [exec] Using default port 3700 for IIOP.
[INFO] [exec] Using default port 8181 for HTTP_SSL.
[INFO] [exec] Using default port 3820 for IIOP_SSL.
[INFO] [exec] Using default port 3920 for IIOP_MUTUALAUTH.
[INFO] [exec] Using default port 8686 for JMX_ADMIN.
[INFO] [exec] Using default port 6666 for OSGI_SHELL.
[INFO] [exec] Using default port 9009 for JAVA_DEBUGGER.
[INFO] [exec] Distinguished Name of the self-signed X.509 Server Certificate is:
[INFO] [exec] [CN=localhost,OU=Payara,O=Payara Foundation,L=Great Malvern,ST=Worcestershire,C=UK]
[INFO] [exec] Distinguished Name of the self-signed X.509 Server Certificate is:
[INFO] [exec] [CN=localhost-instance,OU=Payara,O=Payara Foundation,L=Great Malvern,ST=Worcestershire,C=UK]
[INFO] [exec] Domain production created.
[INFO] [exec] Domain production admin port is 4848.
[INFO] [exec] Domain production allows admin login as user "admin" with no password.
[INFO] [exec] Admin login information for host [localhost] and port [4848]
[INFO] [exec] is being overwritten with credentials provided because the
[INFO] [exec] --savelogin option was used during the create-domain command.
[INFO] [exec] Login information relevant to admin user name [admin]
[INFO] [exec] for this domain [production] stored at
[INFO] [exec] [/home/jhlee/.gfclient/pass] successfully.
[INFO] [exec] Make sure that this file remains protected.
[INFO] [exec] Information stored in this file will be used by
[INFO] [exec] administration commands to manage this domain.
[INFO] [exec] Command create-domain executed successfully.
[INFO]
[INFO] --- maven-antrun-plugin:1.8:run (foo) @ payara ---
[INFO] Executing tasks

main:
     [echo] Building payara (final name payara)
     [echo] Running from /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara
     [echo] Output dir is /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/classes
     [echo] Parent is org.glassfish.main.distributions:distributions:pom:5.192
     [copy] Copying 1 file to /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/classes/META-INF
[INFO] Executed tasks
[INFO]
[INFO] --- glassfishbuild-maven-plugin:3.2.20.payara-p1:zip (default-zip) @ payara ---
[INFO] duplicate: preserve
[INFO] file set : /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/stage (excludes: [], includes: [**/bin/*, **/bin/*.bat, **/lib/nadmin*])
[INFO] file set : /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/stage (excludes: [**/bin/*, **/bin/*.bat, **/lib/nadmin*], includes: [])
[INFO] [zip] Building zip: /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/payara.zip
[INFO]
[INFO] --- maven-install-plugin:3.0.0-M1:install (default-install) @ payara ---
[INFO] Installing /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/target/payara.zip to /home/jhlee/.m2/repository/fish/payara/distributions/payara/5.192/payara-5.192.zip
[INFO] Installing /home/jhlee/gitsrc/Payara-env/Payara-src/appserver/distributions/payara/pom.xml to /home/jhlee/.m2/repository/fish/payara/distributions/payara/5.192/payara-5.192.pom
```
