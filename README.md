# Heroku GWT Example

This is a sample GWT application that is set up to run on Heroku. It's based on the [GWT Maven Archetype](http://mojo.codehaus.org/gwt-maven-plugin/user-guide/archetype.html) and uses [webapp-runner](https://github.com/jsimone/webapp-runner) to launch the application in a lightweight Tomcat container.

You can clone and deploy it to Heroku as is, but I would recommend adding a whole bunch of your own awesome code to it first.

## Building

Requirements:

- JDK 17 or newer (tested up to JDK 25)
- Maven 3.x

Build the WAR (this also downloads `webapp-runner.jar` into `target/dependency`):

    mvn clean package

To also run the GWT integration tests (`GwtTest*`, run headless with HtmlUnit by `gwt:test`), go through the `verify` phase:

    mvn clean verify

On JDK 17+ the GWT test JVM needs `--add-opens java.base/java.lang=ALL-UNNAMED`; this is already set via the `gwt.extraJvmArgs` property in `pom.xml`. If you override that property on the command line, keep the flag.

## Running locally

After building, start the app the same way the `Procfile` does on Heroku:

    java -jar target/dependency/webapp-runner.jar --port 8080 target/herokuGWTMavenSample-1.0-SNAPSHOT

Then open <http://localhost:8080/>.

## Deploying to Heroku

Heroku runs `mvn` to build, then launches the app using the `Procfile`. `system.properties` pins the Java runtime to 17.
