# Sentry Missing JPMS capability example

This example demonstrates the missing JPMS capability of Sentry SDK.

## How to reproduce

```shell
./gradlew build
```

The build will fail with the following error:

```
> Task :app:compileJava FAILED
/Users/..../sentry-jpms/app/src/main/java/module-info.java:5: error: module not found: sentry
    requires sentry;
             ^
1 error

FAILURE: Build failed with an exception.
```

The issue is already filed at https://github.com/getsentry/sentry-java/issues/945

## Expected behavior

The build should succeed.

## Rationale

The Sentry SDK JAR file misses either the `module-info.class` file or an `Automatic-Module-Name` entry in the `MANIFEST.MF` file. This is the bare minimum to make a JAR file a JPMS capable module.

## Workaround

A workaround would be to remove the `module-info.java` file from this project. This will make the project compile and run successfully. However, this sacrifices the use of JPMS in the project all together.

## Further reading

- https://openjdk.org/projects/jigsaw/spec/
- https://en.wikipedia.org/wiki/Java_Platform_Module_System
- https://www.baeldung.com/java-modularity
