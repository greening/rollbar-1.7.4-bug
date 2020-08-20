# Bug in Rollbar 1.6.0 through 1.7.4

From version 1.6.0 to 1.7.4, Rollbar fails to log through log4j2 with this (typical) configuration. I include a demonstration with fat-jar system uno-jar, and a demonstration without uno-jar.

## Installing

To see this bug, first create file `secret.properties`, and add a Rollbar token thus:
```properties
rollbar.accessToken=<secret-rollbar-token>
```
Then run these commands:
```shell script
mvn clean install
java -jar target/rollbar-1.0-SNAPSHOT-unojar.jar
```
You can see that Rollbar works correctly in 1.5.2. If you edit `pom.xml` and change <rollbar.version> to 1.7.4,.then log4j2 will correctly log to console and rolling file, but will not log in Rollbar. The failure is present from Rollbar 1.6.0 onward.

## Running without uno-jar

You can also see Rollbar fail without unojar, by running this command:

```shell script
java -cp 'target/rollbar-1.0-SNAPSHOT.jar:target/lib/*' org.greening.Main
```
