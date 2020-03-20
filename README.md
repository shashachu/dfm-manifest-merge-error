# dfm-manifest-merge-error
Sample app demonstrating the manifest merge error when using product flavors and dynamic feature modules when enabling `android.uniquePackageNames`. This results in runtime crashes when using AGP 3.6.1 unless you enable `android.generateRJava`.

Building a flavor that does not override applicationId fails at the manifest merge step. Building a flavor that does override applicationId succeeds.

# Repro:
```
$ ./gradlew :app:processProductionDebugManifest

> Task :app:processProductionDebugManifest FAILED
/Users/shasha/code/dfm-manifest-merge-error/app/src/main/AndroidManifest.xml Error:
        Package name 'com.test' used in: AndroidManifest.xml, :dynamicfeature.
/Users/shasha/code/dfm-manifest-merge-error/app/src/main/AndroidManifest.xml Error:
        Validation failed, exiting

See http://g.co/androidstudio/manifest-merger for more information about the manifest merger.


FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:processProductionDebugManifest'.
> Manifest merger failed with multiple errors, see logs

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 909ms
15 actionable tasks: 15 executed
```

```
$ ./gradlew :app:processAlphaDebugManifest

BUILD SUCCESSFUL in 831ms
15 actionable tasks: 15 executed
```