# Finoid Code Style

A library that enforces the Finoid's code style using Checkstyle for consistent
formatting across projects.

<div align="center">
  <img src=".github/assets/finoid-code-style.jpg" width="256">
</div>

## Installation

### IntelliJ IDEA

#### Configure Checkstyle Plugin

1. Clone this repository locally.
2. Install the Checkstyle-IDEA plugin:
    - Go to `File > Settings > Plugins`
    - Search for **CheckStyle-IDEA**
    - Install and restart IntelliJ
3. Configure the plugin:
    - Go to `File > Settings > Tools > Checkstyle`
    - Click `+` to add a configuration file
    - Select `src/main/resources/checkstyle.xml`
    - Name it (e.g., `Finoid Checkstyle`)
    - Set **Scan Scope** to `Only Java Sources (Including tests)`

### Maven

#### Add Checkstyle to Build

To enforce code style during build, add the following configuration:

```xml
<properties>
    <finoid-code-style>0.10.0</finoid-code-style>
    <checkstyle.version>10.24.0</checkstyle.version>
    <maven-checkstyle-plugin.version>3.6.0</maven-checkstyle-plugin.version>
</properties>

<build>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-checkstyle-plugin</artifactId>
        <version>${maven-checkstyle-plugin.version}</version>
        <dependencies>
            <dependency>
                <groupId>io.github.finoid</groupId>
                <artifactId>io.github.finoid</artifactId>
                <version>${finoid-code-style.version}</version>
            </dependency>
            <dependency>
                <groupId>com.puppycrawl.tools</groupId>
                <artifactId>checkstyle</artifactId>
                <version>${checkstyle.version}</version>
        </dependency>
        </dependencies>
        <configuration>
            <configLocation>checkstyle.xml</configLocation>
            <violationSeverity>warning</violationSeverity>
            <logViolationsToConsole>true</logViolationsToConsole>
            <sourceDirectories>
                <sourceDirectory>${project.build.sourceDirectory}</sourceDirectory>
                <sourceDirectory>${project.build.testSourceDirectory}</sourceDirectory>
            </sourceDirectories>
        </configuration>
        <executions>
            <execution>
                <goals>
                    <goal>check</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
</build>
```