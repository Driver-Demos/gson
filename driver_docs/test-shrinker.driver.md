## Folders
- **[src](test-shrinker/src.driver.md)**: The `src` folder in the `gson` codebase contains the `main` and `test` directories, which are dedicated to Java files for demonstrating Gson's capabilities and integration tests for validating shrunken and obfuscated JARs, respectively.

## Files
- **[common.pro](test-shrinker/common.pro.driver.md)**: The `common.pro` file contains ProGuard and R8 rules specifically for integration tests in the `gson` codebase, ensuring certain classes and fields are preserved during code shrinking.
- **[pom.xml](test-shrinker/pom.xml.driver.md)**: The `pom.xml` file in the `gson/test-shrinker` directory configures a Maven project for testing code shrinking using ProGuard and R8, including dependencies, plugins, and build configurations.
- **[proguard.pro](test-shrinker/proguard.pro.driver.md)**: The `proguard.pro` file in the `gson` codebase specifies ProGuard rules to preserve field names for certain classes to ensure successful deserialization.
- **[r8.pro](test-shrinker/r8.pro.driver.md)**: The `r8.pro` file in the `gson` codebase specifies R8 configuration rules for optimizing and obfuscating Java classes, particularly focusing on preserving generic type parameters and specific class structures in "full mode".
- **[README.md](test-shrinker/README.md.driver.md)**: The `README.md` file in the `gson/test-shrinker` directory provides an overview of the Maven module that contains integration tests for evaluating Gson's behavior with code shrinking and obfuscation tools like ProGuard and R8.
