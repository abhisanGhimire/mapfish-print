Please read the documentation available here: <https://mapfish.github.io/mapfish-print/>

For professional support, users should sign a support contract with a professional services
company, and use their appropriate channel.

# Prerequisites

Building mapfish-print requires make and Docker.

# Build

Execute the following command():

```{.sourceCode .}
> make build
```

This will build three artifacts: print-servlet-xxx.war, print-lib.jar, print-standalone.jar

The build also builds the documentation in the docs/build/site folder. To deploy the documentation it should
simply be copied to the gh-pages branch and then committed GitHub will automatically build the updated site
at: <https://mapfish.github.io/mapfish-print/>

If you only want to build the docs simply run:

```{.sourceCode .}
> ./gradlew docs:build
```

or run build in the docs directory.

<div class="admonition note">

The test (part of the build) requires the 'Liberation Sans' font, which can be downloaded
[here](https://www.fontsquirrel.com/fonts/Liberation-Sans).

</div>

# Auto-releoad mode

To be able to quickly test modifications in the print you should:
- Copy the file `docker-compose.override.sample.yaml` to `docker-compose.override.yaml`.
- Run `docker compose up -d`,
The print will be available on port `8080` and on code modification will be built and trigger a restart.

# Create new stabilisation branch

- Update *CHANGELOG.md*
- In the `builds.gradle` file , set the version to `x.y.0`.
- Create a new branch name x.y from master.
- Create a new label names 'backport x.y' in the right color (github: Issues->Labels->New Label).
- Create a tag 'release/x.y.0'.
- On the master branch: Update the `SECURITY.md` file, add a policy for the new and old version.
- On the master branch update the `.github/workflows/rebuild.yaml` file by adding the new branch name.
- On the master branch update the `.github/workflows/audit.yaml` file by adding the new branch name.
- On the master branch set in the `build.gradle` file the new `x.y+1.0-SNAPSHOT` version.

# Run from commandline

The following command will run the mapfish printer. The arguments must be supplied to the -PprintArgs="..."
parameter.

To list all the commandline options then execute (the current direstory is ./core):

```{.sourceCode .}
> ./gradlew print -PprintArgs="-help"
```

```{.sourceCode .}
> ./gradlew print -PprintArgs="-config ../examples/src/test/resources/examples/simple/config.yaml -spec ../examples/src/test/resources/examples/simple/requestData.json -output ./output.pdf"
```

If you want to run in debug mode you can do the following:

```{.sourceCode .}
> ./gradlew print --debug-jvm -PprintArgs="-config ../examples/src/test/resources/examples/simple/config.yaml -spec ../examples/src/test/resources/examples/simple/requestData.json -output ./output.pdf"
```

For the examples that use geoserver you shoul run it in the composition, then build and start the composition:

```
make build
cp docker-compose.override.sample.yaml docker-compose.override.yaml
make acceptance-tests-up
```

Run the example:

```
docker-compose exec builder gradle print -PprintArgs="-config /src/examples/src/test/resources/examples/simple/config.yaml -spec /src/examples/src/test/resources/examples/simple/requestData.json -output /src/examples/output.pdf"
```

# To use in Eclipse

Create Eclipse project metadata:

```{.sourceCode .}
> ./gradlew eclipse
```

Import project into Eclipse

# Run in Eclipse

- Create new Java Run Configuration
- Main class is org.mapfish.print.cli.Main
- Program arguments: -config samples/config.yaml -spec samples/spec.json -output \$HOME/print.pdf

# Contributor License Agreement

Before accepting a contribution, we ask that you provide us a Contributor License Agreement. If you are making
your contribution as part of work for your employer, please follow the guidelines on submitting a [Corporate
Contributor License Agreement](https://github.com/mapfish/mapfish-print/wiki/C2C_Corporate-CLA_v1-0.pdf). If
you are making your contribution as an individual, you can submit a digital [Individual Contributor License
Agreement](http://goo.gl/forms/QO9UELxM9m).

# Credits

![image](https://www.yourkit.com/images/yklogo.png)

> target
>
> : <https://www.yourkit.com/java/profiler/index.jsp>
>
> Thanks to [YourKit](https://www.yourkit.com/java/profiler/index.jsp) for letting us use their Java profiler!

# Published artifacts

[Docker](https://hub.docker.com/r/camptocamp/mapfish_print)

[War and jar from version 3.23](https://github.com/orgs/mapfish/packages)

[War and jar before version 3.23](https://mvnrepository.com/artifact/org.mapfish.print)

[Releases, including various assets](https://github.com/mapfish/mapfish-print/releases)
