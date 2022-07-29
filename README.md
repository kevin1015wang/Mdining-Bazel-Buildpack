# heroku-buildpack-bazel

Heroku buildpack for [Bazel](http://www.bazel.io). You can find the original [buildback by Google here](https://github.com/google/heroku-buildpack-bazel).

This fork has been tested against `Scala` and `Java` in production, and furthermore has support for poly-repo like build patterns. The `BAZEL_BUILD_PATH` environment variable allows you to specify any build target, so you can deploy the same repository to containers with different settings and run different applications accordingly.


## Requirements

1. `WORKSPACE` file in git-root. See the documentation on [Bazel WORKSPACE](http://www.bazel.io/docs/tutorial/workspace.html).
2. `BAZEL_BUILD_PATH` config variable containing the build-path of the `{java, scala}_binary` you want to run.


## Default Procfile
The default `Procfile` is:
```Procfile
  web: .jdk/bin/java -jar app.jar
  worker: .jdk/bin/java -jar app.jar
```

This does not need to be included in your app. However, if you need custom JVM flags, simply include your custom `Procfile` with your application. Modify the line above with the flags you want.

## Use this buildpack

```shell
heroku config:set BAZEL_BUILD_PATH=//path/to/your:bin
heroku buildpacks:set https://github.com/ThriveFinancial/heroku-buildpack-bazel
```
