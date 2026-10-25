# 📦 Apache Maven: Commands & Guide

![Maven](https://img.shields.io/badge/Apache_Maven-C71A36?logo=apachemaven&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white)
![Type](https://img.shields.io/badge/type-cheat%20sheet-informational)

My study notes and reference guide for **Apache Maven**, the build automation and dependency management tool for Java projects.

📄 **Full guide:** [`Apache_Maven_Commands_and_Guide.pdf`](Apache_Maven_Commands_and_Guide.pdf) (also available as [`.docx`](Apache_Maven_Commands_and_Guide.docx))

## What is Maven?

Maven builds Java projects using **convention over configuration**. One file, `pom.xml` (the *Project Object Model*), describes the project, its dependencies and plugins. Maven then compiles, tests, packages and deploys it in a standard, repeatable way.

## Key concepts

| Concept | Summary |
|---------|---------|
| **POM (`pom.xml`)** | Central config: coordinates (`groupId:artifactId:version`), dependencies, plugins, build settings |
| **Dependency management** | Declares libraries in the POM; Maven downloads them (and their transitive dependencies) from Maven Central |
| **Standard layout** | `src/main/java`, `src/main/resources`, `src/test/java`, `target/` |
| **Build lifecycle** | `validate → compile → test → package → verify → install → deploy` |
| **Plugins** | Surefire (tests), Assembly (distributions), Javadoc, Shade, Compiler, … |
| **Repositories** | Local (`~/.m2/repository`) and remote (Maven Central or an internal Nexus/Artifactory) |
| **Multi-module** | A parent POM aggregates and configures several modules |

## Most-used commands

```bash
mvn -v                         # Maven & Java versions
mvn archetype:generate         # create a new project from a template
mvn clean                      # delete target/
mvn compile                    # compile main sources
mvn test                       # run unit tests (Surefire)
mvn package                    # build JAR/WAR into target/
mvn install                    # install artifact into the local ~/.m2 repo
mvn deploy                     # publish artifact to a remote repository
mvn clean install -DskipTests  # full build without tests
mvn dependency:tree            # show the dependency graph
mvn versions:display-dependency-updates   # find outdated dependencies
mvn -pl module-a -am install   # build one module and what it depends on
```

## Minimal `pom.xml`

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.release>17</maven.compiler.release>
  </properties>
  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter</artifactId>
      <version>5.10.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```

## Maven in CI/CD

Maven fits naturally into Jenkins and GitHub Actions pipelines. `mvn -B clean verify` gives a non-interactive build with tests, and `mvn deploy` publishes artifacts to Nexus or Artifactory.
