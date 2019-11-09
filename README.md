[![APACHE v2 License](https://img.shields.io/badge/license-apachev2-blue.svg?style=flat)](LICENSE-2.0.txt) 
[![Latest Release](https://img.shields.io/maven-central/v/com.github.bbottema/jetbrains-runtime-annotations.svg?style=flat)](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.github.bbottema%22%20AND%20a%3A%22jetbrains-runtime-annotations%22)
[![Javadocs](http://www.javadoc.io/badge/com.github.bbottema/jetbrains-runtime-annotations.svg)](https://javadoc.io/doc/com.github.bbottema/jetbrains-runtime-annotations)

# jetbrains-runtime-nullability-annotations
The well-known Jetbrains nullability annotations, but with RUNTIME retention

```
<dependency>
  <groupId>com.github.bbottema</groupId>
  <artifactId>jetbrains-runtime-annotations</artifactId>
  <version>1.0.0</version>
  <scope>provided</scope>
</dependency>
```

## Why
There are currently no nullability annotations available that are available for reflection in runtime. The community used to have the `javax.annotation.Nullable` from FindBugs' and later SpotBugs' [JSR305](https://stackoverflow.com/questions/2289694/what-is-the-status-of-jsr-305) implementation, but as that uses the same packages as the JDK, with Java's modularization, this can [cause the split-package](https://github.com/google/guava/issues/2960) problem.

Modern IDE's natively handle these annotations and common static analyses (like the Maven SpotBugs plugin) understand these annotations, but are limited to a specific set of known common packages or certain Java class names. The [Jetbrains annotations](https://search.maven.org/search?q=g:org.jetbrains%20AND%20a:annotations&core=gav), and possible the [Eclipse annotations](https://search.maven.org/search?q=g:org.eclipse.jdt%20AND%20a:org.eclipse.jdt.annotation&core=gav), are the most neutral and light-weight libraries available that are supported this way. Google's [Checker Qual](https://search.maven.org/search?q=g:org.checkerframework%20AND%20a:checker-qual&core=gav) brings a lot of baggage and the others are focussed on Android or are very old.

That leaves us with the Jetbrains annotations, but they are limited to CLASS retention and its developers [have no plans to change this](https://intellij-support.jetbrains.com/hc/en-us/community/posts/206984375-Runtime-retention-of-Nullable-for-dependency-injection). They in fact suggest to recompile them with RUNTIME retention.

## How
This library simply copies the source code for the Jetbrains nullability annotations (only @NotNull and @Nullable) and changes the retention from CLASS to RUNTIME
