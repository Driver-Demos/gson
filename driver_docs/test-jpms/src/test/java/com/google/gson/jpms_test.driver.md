## Folders
- **[opened](jpms_test/opened.driver.md)**: The `opened` folder in the `gson` codebase contains a test file, `ReflectionTest.java`, which ensures that Gson can handle serialization and deserialization of objects using reflection when the package is accessible to the Gson module.

## Files
- **[ExportedPackagesTest.java](jpms_test/ExportedPackagesTest.java.driver.md)**: The `ExportedPackagesTest.java` file contains unit tests to verify that Gson's `module-info.class` correctly exports its public API packages without opening them for reflection.
- **[ModuleTest.java](jpms_test/ModuleTest.java.driver.md)**: The `ModuleTest.java` file contains JUnit tests to verify the module setup of the test project and the module descriptor of Gson, ensuring it is correctly configured and adheres to expected dependencies and exports.
- **[ReflectionInaccessibleTest.java](jpms_test/ReflectionInaccessibleTest.java.driver.md)**: The `ReflectionInaccessibleTest.java` file contains tests to verify that Gson cannot use reflection on classes in a package that has not been opened to the Gson module, resulting in `JsonIOException` during serialization and deserialization.
