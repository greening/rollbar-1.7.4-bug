# Bug in Rollbar 1.6.0 through 1.7.4

From version 1.6.0 to 1.7.4, Rollbar fails to work correctly with either one-jar or uno-jar (popular fat jar approaches).



To see this bug, first edit file src/main/resources/log4j2.properties, and add a Rollbar token to line 24 thus:
```properties
appender.rollbar.accessToken=<rollbar-token>
```
Then run these commands:
```shell script
mvn clean install
java -jar target/rollbar-1.0-SNAPSHOT-unojar.jar
```
You can see that Rollbar works correctly in 1.5.2. If you edit pom.xml and change <rollbar.version> to 1.7.4 thus:
```xml
<rollbar.version>1.7.4</rollbar.version>
```
...then log4j2 will correctly log to console and rolling file, but will not log in Rollbar. The failure is present from Rollbar 1.6.0 onward.
