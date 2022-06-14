# Guess My Java Version

A utility to perform a best effort selection of the Java version needed by the build tool to build a Java project. [Moderne](https://public.moderne.io) offers a large public dataset of type attributed abstract syntax trees (ASTs) produced from OSS code. These ASTs are built daily. In order to produce an AST, the Java version that the project's build tool must run with must be known in advance.

Unfortunately, neither Gradle or Maven require any explicit signal about the Java version they require, so this must be inferred from the project using a variety of heuristics.

## Known heuristics

| Heuristic | Notes |
|--------------|-------------------|
| Gradle `sourceCompatibility` | See [Java Plugin reference](https://docs.gradle.org/current/userguide/java_plugin.html#sec:java-extension) |
| Maven `maven.compiler.source` | See [blog](https://www.baeldung.com/maven-java-version#compiler) |
| Use of libraries requiring a minimum Java 11 version | Caffeine 3.+. This would likely involve looking for direct dependencies, since otherwise chicken and egg problem. |
| References to base docker images | e.g. openjdk:11-jdk-slim |
| CircleCI Java version | See [openjdk](https://circleci.com/developer/images/image/cimg/openjdk). Also check docs for what implied default version is |
| TravisCI Java version | See [Building a Java project](https://docs.travis-ci.com/user/languages/java/) |
| GitHub actions Java version | See [GitHub actions docs](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven#using-the-maven-starter-workflow) |
| Any reference to Jigsaw | The presence of a `module-info.java` or a declared dependency on a module |
