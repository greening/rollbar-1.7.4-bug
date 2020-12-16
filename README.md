# Bug in Rollbar 1.6.0 through 1.7.5

From version 1.6.0 to 1.7.5, Rollbar fails to log through log4j2 with this (typical) configuration.

## Install and demonstrate bug

To see this bug, first create file `secret.properties`, and add a Rollbar token thus:
```properties
rollbar.accessToken=<secret-rollbar-token>
```
Then run these commands:
```shell script
mvn clean install
java -cp 'target/rollbar-1.0-SNAPSHOT.jar:target/lib/*' org.greening.Main
```
You can see that it does not log "Donald Trump was elected US President" as an error to Rollbar, but log4j2 logs correctly logs "Donald Trump was elected US President" as an error to console and rolling file. The failure is present from Rollbar 1.6.0 onward.

## See Rollbar 1.5.2 succeed

Change the version of Rollbar 1.5.2 in the pom.xml `<rollbar.version>1.5.2</rollbar.version>`. Then run these commands:
```shell script
mvn clean install
java -cp 'target/rollbar-1.0-SNAPSHOT.jar:target/lib/*' org.greening.Main
```
It now works.

## Running with uno-jar

We use uno-jar fat jar system, and so at first I thought it might be that. You can also see Rollbar fail with unojar, by running this command, but uno-jar is really not necessary to see this bug.

```shell script
java -jar target/rollbar-1.0-SNAPSHOT-unojar.jar
```
