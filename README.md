# jetbrains-runtime-nullability-annotations
The well-known Jetbrains nullability annotations, but with RUNTIME retention

## Why
There are currently no nullability annotations available that are available for reflection in runtime. The community used to have the `javax.annotation.Nullable` from FindBugs' and later SpotBugs' [JSR305](https://stackoverflow.com/questions/2289694/what-is-the-status-of-jsr-305) implementation, but as that uses the same packages as the JDK, with Java's modularization, this can [cause the split-package](https://github.com/google/guava/issues/2960) problem.

Modern IDE's natively handle these annotations and common static analyses (like the Maven SpotBugs plugin) understand these annotations, but are limited to a specific set of known common packages or certain Java class names. The [Jetbrains annotations](https://search.maven.org/search?q=g:org.jetbrains%20AND%20a:annotations&core=gav), and possible the [Eclipse annotations](https://search.maven.org/search?q=g:org.eclipse.jdt%20AND%20a:org.eclipse.jdt.annotation&core=gav), are the most neutral and light-weight libraries available that are supported this way. Google's [Checker Qual](https://search.maven.org/search?q=g:org.checkerframework%20AND%20a:checker-qual&core=gav) brings a lot of baggage and the others are focussed on Android or are very old.

That leaves us with the Jetbrains annotations, but they are limited to CLASS retention and its developers [have no plans to change this](https://intellij-support.jetbrains.com/hc/en-us/community/posts/206984375-Runtime-retention-of-Nullable-for-dependency-injection). They in fact suggest to recompile them with RUNTIME retention.

## How
This library simply copies the source code for the Jetbrains nullability annotations and changes the retention from CLASS to RUNTIME
