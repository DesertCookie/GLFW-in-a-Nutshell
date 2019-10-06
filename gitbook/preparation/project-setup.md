---
description: Getting a project set up to start development
---

# Project Setup

## Java

Wrappers available for Java:

| Wrapper | Author | GitHub | Source | Documentation |
| :--- | :--- | :--- | :--- | :--- |
| jGLFW | badlogic | \[github.com\]\(\([https://github.com/badlogic/jglfw](https://github.com/badlogic/jglfw)\)\) | [gitbub.com](https://github.com/badlogic/jglfw/tree/master/jglfw/src/com/badlogic/jglfw) | - |
| LWJGL-GLFW | LWJGL | [github.com](https://github.com/LWJGL/lwjgl3) | [github.com](https://github.com/LWJGL/lwjgl3/tree/master/modules/lwjgl/glfw) | [lwjgl.org](https://javadoc.lwjgl.org/org/lwjgl/glfw/package-summary.html) |

_In this guide, LWJGL-GLFW will be used. There are no plans to add a how-to for jGLFW. LWJGL-GLFW requires the LWJGL core, and since_ [_STB_](https://github.com/nothings/stb) _will be used in this guide, we will also add LWJGL-STB._

### Maven

This assumes, you have already created a Maven project and have some familiarity with Maven's `pom.xml` file.

Depending on your operating system, add the following to your `pom.xml`:

```markup
    <properties>
      <lwjgl.version>3.2.3</lwjgl.version>
      <lwjgl.natives>natives-windows-x86</lwjgl.natives>
   </properties>

   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>org.lwjgl</groupId>
            <artifactId>lwjgl-bom</artifactId>
            <version>${lwjgl.version}</version>
            <scope>import</scope>
            <type>pom</type>
         </dependency>
      </dependencies>
   </dependencyManagement>

   <dependencies>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-glfw</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-stb</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-glfw</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-stb</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
   </dependencies>
```

```markup
    <properties>
      <lwjgl.version>3.2.3</lwjgl.version>
      <lwjgl.natives>natives-linux</lwjgl.natives>
   </properties>

   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>org.lwjgl</groupId>
            <artifactId>lwjgl-bom</artifactId>
            <version>${lwjgl.version}</version>
            <scope>import</scope>
            <type>pom</type>
         </dependency>
      </dependencies>
   </dependencyManagement>

   <dependencies>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-glfw</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-stb</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-glfw</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-stb</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
   </dependencies>
```

```markup
    <properties>
      <lwjgl.version>3.2.3</lwjgl.version>
      <lwjgl.natives>natives-macos</lwjgl.natives>
   </properties>

   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>org.lwjgl</groupId>
            <artifactId>lwjgl-bom</artifactId>
            <version>${lwjgl.version}</version>
            <scope>import</scope>
            <type>pom</type>
         </dependency>
      </dependencies>
   </dependencyManagement>

   <dependencies>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-glfw</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-stb</artifactId>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-glfw</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
      <dependency>
         <groupId>org.lwjgl</groupId>
         <artifactId>lwjgl-stb</artifactId>
         <classifier>${lwjgl.natives}</classifier>
      </dependency>
   </dependencies>
```

If you require a more complex dependency setup, for example supporting multiple operating systems, head to [lwjgl.org](https://lwjgl.org/customize) and easily build a `pom.xml` specific to your needs.

### Gradle

This assumes, you have already created a Gradle project and have some familiarity with Gradle's `build.gralde` file.

Depending on your operating system, add the following to your `build.gradle`:

```groovy
    project.ext.lwjglVersion = "3.2.3"
    project.ext.lwjglNatives = "natives-windows-x86"

    repositories {
       mavenCentral()
    }

    dependencies {
       implementation platform("org.lwjgl:lwjgl-bom:$lwjglVersion")

       implementation "org.lwjgl:lwjgl"
       implementation "org.lwjgl:lwjgl-glfw"
       implementation "org.lwjgl:lwjgl-stb"
       runtimeOnly "org.lwjgl:lwjgl::$lwjglNatives"
       runtimeOnly "org.lwjgl:lwjgl-glfw::$lwjglNatives"
       runtimeOnly "org.lwjgl:lwjgl-stb::$lwjglNatives"
    }
```

```groovy
    project.ext.lwjglVersion = "3.2.3"
    project.ext.lwjglNatives = "natives-linux"

    repositories {
       mavenCentral()
    }

    dependencies {
       implementation platform("org.lwjgl:lwjgl-bom:$lwjglVersion")

       implementation "org.lwjgl:lwjgl"
       implementation "org.lwjgl:lwjgl-glfw"
       implementation "org.lwjgl:lwjgl-stb"
       runtimeOnly "org.lwjgl:lwjgl::$lwjglNatives"
       runtimeOnly "org.lwjgl:lwjgl-glfw::$lwjglNatives"
       runtimeOnly "org.lwjgl:lwjgl-stb::$lwjglNatives"
    }
```

```groovy
    project.ext.lwjglVersion = "3.2.3"
    project.ext.lwjglNatives = "natives-macos"

    repositories {
       mavenCentral()
    }

    dependencies {
       implementation platform("org.lwjgl:lwjgl-bom:$lwjglVersion")

       implementation "org.lwjgl:lwjgl"
       implementation "org.lwjgl:lwjgl-glfw"
       implementation "org.lwjgl:lwjgl-stb"
       runtimeOnly "org.lwjgl:lwjgl::$lwjglNatives"
       runtimeOnly "org.lwjgl:lwjgl-glfw::$lwjglNatives"
       runtimeOnly "org.lwjgl:lwjgl-stb::$lwjglNatives"
    }
```

If you require a more complex dependency setup, for example supporting multiple operating systems, head to [lwjgl.org](https://lwjgl.org/customize) and easily build a `gradle.properties` specific to your needs.

### IntelliJ IDEA / Eclipse

This assumes, you have already created an IntelliJ IDEA or Eclipse project and are somewhat familiar with your IDE of choice.

1. Open [lwjgl.org](https://lwjgl.org/customize) and select `Release`.
2. Adjust the following settings:  

     Options: `Include source`, `Include JavaDoc`  

     Natives: _choose depending on your needs_  

     Presets: `None` \(_to deselect everything_\)  

     Contents: `LWJGL core`, `GLFW`, `stb`

3. Hit `DOWNLOAD ZIP` and extract the downloaded archive into a folder in your project root \(e.g. `lib`\).
