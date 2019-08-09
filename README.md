# KT-33206
A sample project to reproduce [KT-33206](https://youtrack.jetbrains.com/issue/KT-33206).

The issue seems to be caused by incremental Kotlin annotation processor which can be enabled via `kapt.incremental.apt=true` flag in Gradle properties.
To reproduce, run `./gradlew :foo:kaptKotlin`
Failure stacktrace:

```
> Could not resolve all files for configuration ':foo:_classStructurekaptKotlin'.
   > Could not resolve com.squareup.wire:wire-runtime:3.0.0-rc01.
     Required by:
         project :foo
      > Cannot choose between the following variants of com.squareup.wire:wire-runtime:3.0.0-rc01:
          - jvm-api
          - jvm-runtime
          - metadata-api
        All of them match the consumer attributes:
          - Variant 'jvm-api' capability com.squareup.wire:wire-runtime:3.0.0-rc01:
              - Unmatched attributes:
                  - Found org.gradle.status 'release' but wasn't required.
                  - Found org.gradle.usage 'java-api-jars' but wasn't required.
                  - Found org.jetbrains.kotlin.platform.type 'jvm' but wasn't required.
          - Variant 'jvm-runtime' capability com.squareup.wire:wire-runtime:3.0.0-rc01:
              - Unmatched attributes:
                  - Found org.gradle.status 'release' but wasn't required.
                  - Found org.gradle.usage 'java-runtime-jars' but wasn't required.
                  - Found org.jetbrains.kotlin.platform.type 'jvm' but wasn't required.
          - Variant 'metadata-api' capability com.squareup.wire:wire-runtime:3.0.0-rc01:
              - Unmatched attributes:
                  - Found org.gradle.status 'release' but wasn't required.
                  - Found org.gradle.usage 'kotlin-api' but wasn't required.
                  - Found org.jetbrains.kotlin.platform.type 'common' but wasn't required.
```
