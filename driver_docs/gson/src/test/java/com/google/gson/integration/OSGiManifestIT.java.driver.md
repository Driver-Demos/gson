# Purpose
The provided Java source code file is an integration test class named `OSGiManifestIT`, which is part of the `com.google.gson.integration` package. This class is designed to perform assertions on the generated OSGi manifest attributes of the Gson library. The primary purpose of this file is to ensure that the manifest file within the final JAR of the Gson library is correctly configured with the expected attributes, such as `Bundle-SymbolicName`, `Bundle-Name`, `Bundle-License`, and `Bundle-Version`. The tests also verify the import and export package declarations, ensuring that dependencies are correctly specified and that there are no unnecessary imports, particularly of Gson's own packages. The class is structured to be run as part of a Maven build process, specifically using the `mvn clean verify` command, to ensure that the tests are executed against the final JAR rather than an intermediate build.

The technical components of this file include several private methods that assist in parsing and validating the manifest attributes, such as [`findManifest`](#OSGiManifestITfindManifest), [`splitPackages`](#OSGiManifestITsplitPackages), [`shortenVersionNumber`](#OSGiManifestITshortenVersionNumber), and [`increaseVersionNumber`](#OSGiManifestITincreaseVersionNumber). These methods are used to locate the manifest file, split package strings, and manipulate version numbers for comparison purposes. The class uses JUnit annotations like `@Before` and `@Test` to set up the test environment and define individual test cases. The integration test is crucial for maintaining the integrity of the OSGi manifest, ensuring that the Gson library is packaged correctly for OSGi environments, which is essential for modular Java applications.
# Imports and Dependencies

---
- `com.google.gson.integration`
- `com.google.common.truth.Truth.assertThat`
- `com.google.common.truth.Truth.assertWithMessage`
- `org.junit.Assert.fail`
- `com.google.common.base.Splitter`
- `com.google.gson.internal.GsonBuildConfig`
- `java.io.IOException`
- `java.io.InputStream`
- `java.net.URL`
- `java.util.ArrayList`
- `java.util.Collections`
- `java.util.List`
- `java.util.jar.Attributes`
- `java.util.jar.Manifest`
- `java.util.stream.Collectors`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### OSGiManifestIT<!-- {{#class:com.google.gson.integration.OSGiManifestIT}} -->
- **Modifiers**: `public`
- **Description**: The `OSGiManifestIT` class is an integration test designed to perform assertions on the generated OSGi manifest attributes for the Gson library. It ensures that the manifest is correctly loaded from the final Gson JAR and verifies various attributes such as bundle information, imports, exports, and required capabilities. The class includes methods to find and parse manifest files, split package strings, and manipulate version numbers. It is intended to be run with Maven's Failsafe Plugin, specifically with the `mvn clean verify` command, to ensure the tests are executed against the final JAR and not an intermediate or IDE-generated version.
- **Fields**:
    - `GSON_VERSION`: `String` Holds the version of Gson as defined in the GsonBuildConfig.
    - `manifestAttributes`: `Attributes` Stores the main attributes of the manifest file for the Gson bundle.
- **Methods**:
    - [`com.google.gson.integration.OSGiManifestIT.getGsonManifestAttributes`](#OSGiManifestITgetGsonManifestAttributes)
    - [`com.google.gson.integration.OSGiManifestIT.getAttribute`](#OSGiManifestITgetAttribute)
    - [`com.google.gson.integration.OSGiManifestIT.testBundleInformation`](#OSGiManifestITtestBundleInformation)
    - [`com.google.gson.integration.OSGiManifestIT.testImports`](#OSGiManifestITtestImports)
    - [`com.google.gson.integration.OSGiManifestIT.testExports`](#OSGiManifestITtestExports)
    - [`com.google.gson.integration.OSGiManifestIT.testRequireCapability`](#OSGiManifestITtestRequireCapability)
    - [`com.google.gson.integration.OSGiManifestIT.findManifest`](#OSGiManifestITfindManifest)
    - [`com.google.gson.integration.OSGiManifestIT.splitPackages`](#OSGiManifestITsplitPackages)
    - [`com.google.gson.integration.OSGiManifestIT.shortenVersionNumber`](#OSGiManifestITshortenVersionNumber)
    - [`com.google.gson.integration.OSGiManifestIT.increaseVersionNumber`](#OSGiManifestITincreaseVersionNumber)

**Methods**

---
#### OSGiManifestIT\.getGsonManifestAttributes<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.getGsonManifestAttributes}} -->
The `getGsonManifestAttributes` method initializes the `manifestAttributes` field by loading and verifying the manifest data from the Gson JAR file.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Invoke [`findManifest`](#OSGiManifestITfindManifest) with the argument 'com.google.gson' to retrieve the manifest data for the Gson package.
    - Verify that the manifest data URL ends with '.jar!/META-INF/MANIFEST.MF' to ensure it is loaded from the final Gson JAR file.
    - Assign the main attributes of the manifest to the `manifestAttributes` field.
- **Output**:
    - The method does not return any value; it initializes the `manifestAttributes` field.
- **Functions called**:
    - [`com.google.gson.integration.OSGiManifestIT.findManifest`](#OSGiManifestITfindManifest)
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.getAttribute<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.getAttribute}} -->
The `getAttribute` method retrieves the value of a specified attribute from the manifest attributes.
- **Modifiers**: `private`
- **Inputs**:
    - `name`: The name of the attribute whose value is to be retrieved from the manifest attributes.
- **Control Flow**:
    - The method calls `getValue` on the `manifestAttributes` object, passing the `name` parameter to retrieve the corresponding attribute value.
- **Output**:
    - The method returns a `String` representing the value of the specified attribute from the manifest attributes.
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.testBundleInformation<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.testBundleInformation}} -->
The `testBundleInformation` method verifies that specific OSGi manifest attributes for the Gson library match expected values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to check that the 'Bundle-SymbolicName' attribute equals 'com.google.gson'.
    - It asserts that the 'Bundle-Name' attribute equals 'Gson'.
    - It checks that the 'Bundle-License' attribute matches the expected Apache 2.0 license string with a link.
    - It verifies that the 'Bundle-Version' attribute matches the expected version, replacing '-SNAPSHOT' with '.SNAPSHOT' in the GSON_VERSION.
- **Output**:
    - The method does not return any value; it performs assertions to validate manifest attributes.
- **Functions called**:
    - [`com.google.gson.integration.OSGiManifestIT.getAttribute`](#OSGiManifestITgetAttribute)
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.testImports<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.testImports}} -->
The `testImports` method verifies the correctness of the OSGi manifest's import package attributes for a project, ensuring specific dependencies are optional and that no Gson packages are imported.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the 'Bundle-Version' attribute from the manifest of 'com.google.errorprone.annotations' and shorten it to 'major.minor' format using [`shortenVersionNumber`](#OSGiManifestITshortenVersionNumber).
    - Calculate the next major version of the error-prone version using [`increaseVersionNumber`](#OSGiManifestITincreaseVersionNumber).
    - Construct a version range string for error-prone annotations using the current and next major version.
    - Retrieve the 'Import-Package' attribute from the manifest and split it into a list of package imports using [`splitPackages`](#OSGiManifestITsplitPackages).
    - Check if any of the imports start with 'java.' and fail the test if true, indicating the test must be run from the command line.
    - Assert that the imports list contains exactly the specified optional dependencies for 'sun.misc' and 'com.google.errorprone.annotations' with the constructed version range.
    - Iterate over the imports list and assert that none of the imported packages contain 'com.google.gson'.
- **Output**:
    - The method does not return any value; it performs assertions to validate the import package attributes in the manifest.
- **Functions called**:
    - [`com.google.gson.integration.OSGiManifestIT.shortenVersionNumber`](#OSGiManifestITshortenVersionNumber)
    - [`com.google.gson.integration.OSGiManifestIT.findManifest`](#OSGiManifestITfindManifest)
    - [`com.google.gson.integration.OSGiManifestIT.increaseVersionNumber`](#OSGiManifestITincreaseVersionNumber)
    - [`com.google.gson.integration.OSGiManifestIT.splitPackages`](#OSGiManifestITsplitPackages)
    - [`com.google.gson.integration.OSGiManifestIT.getAttribute`](#OSGiManifestITgetAttribute)
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.testExports<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.testExports}} -->
The `testExports` method verifies that the exported packages in the OSGi manifest match the expected list of packages with their respective version numbers.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the current Gson version, removing any '-SNAPSHOT' suffix.
    - Get the list of exported packages from the manifest's 'Export-Package' attribute using the [`splitPackages`](#OSGiManifestITsplitPackages) method.
    - Assert that the list of exported packages matches the expected list, which includes specific packages and their version numbers.
- **Output**:
    - The method does not return any value; it performs assertions to validate the exported packages.
- **Functions called**:
    - [`com.google.gson.integration.OSGiManifestIT.splitPackages`](#OSGiManifestITsplitPackages)
    - [`com.google.gson.integration.OSGiManifestIT.getAttribute`](#OSGiManifestITgetAttribute)
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.testRequireCapability<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.testRequireCapability}} -->
The `testRequireCapability` method verifies that the OSGi manifest attributes specify the required Java version and do not include deprecated attributes.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A string `expectedJavaVersion` is initialized to "1.8" to represent the minimum required Java version.
    - The method asserts that the `Require-Capability` attribute in the manifest matches the expected format for the specified Java version.
    - The method asserts that the `Bundle-RequiredExecutionEnvironment` attribute is not present in the manifest, indicating that deprecated attributes are not used.
- **Output**:
    - The method does not return any value; it performs assertions to validate manifest attributes.
- **Functions called**:
    - [`com.google.gson.integration.OSGiManifestIT.getAttribute`](#OSGiManifestITgetAttribute)
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.findManifest<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.findManifest}} -->
The `findManifest` method searches for and returns the manifest data of a specified OSGi bundle by its symbolic name.
- **Modifiers**: `private`
- **Inputs**:
    - `bundleName`: The symbolic name of the OSGi bundle whose manifest is to be found.
- **Control Flow**:
    - Retrieve all resources with the name 'META-INF/MANIFEST.MF' using the class loader.
    - Iterate over each URL resource found.
    - For each resource, open an input stream and create a Manifest object from it.
    - Check if the 'Bundle-SymbolicName' attribute of the manifest matches the provided bundleName.
    - If a match is found, return a new ManifestData object containing the URL and the manifest.
    - If no matching manifest is found after checking all resources, fail the test with an error message and return null.
- **Output**:
    - Returns a ManifestData object containing the URL and manifest of the specified bundle if found, otherwise fails the test and returns null.
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.splitPackages<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.splitPackages}} -->
The `splitPackages` method splits a string of package names separated by commas into a list of individual package names, while ignoring commas within quoted sections.
- **Modifiers**: `private`
- **Inputs**:
    - `packagesString`: A string containing package names separated by commas, with potential quoted sections that may contain commas.
- **Control Flow**:
    - Initialize an empty list `splitPackages` to store the resulting package names.
    - Initialize `nextSplitStart` to 0 to track the start index of the next package name.
    - Initialize `isInQuotes` to false to track whether the current character is within quotes.
    - Iterate over each character in `packagesString`.
    - If the character is a double quote ('"'), toggle the `isInQuotes` flag.
    - If the character is a comma (',') and `isInQuotes` is false, add the substring from `nextSplitStart` to the current index to `splitPackages`, and update `nextSplitStart` to the index after the comma.
    - After the loop, add the final substring from `nextSplitStart` to the end of `packagesString` to `splitPackages`.
- **Output**:
    - A list of strings, each representing an individual package name extracted from the input string.
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.shortenVersionNumber<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.shortenVersionNumber}} -->
The `shortenVersionNumber` method truncates a version string to a specified number of components.
- **Modifiers**: `private`
- **Inputs**:
    - `versionString`: A string representing the version number, e.g., "1.2.3".
    - `keepPosition`: An integer indicating the number of version components to retain, starting from the left (0 = major, 1 = minor, etc.).
- **Control Flow**:
    - The method uses the `Splitter` class to split the `versionString` by the '.' character into a stream of version components.
    - It limits the stream to `keepPosition + 1` components, effectively truncating the version string to the desired length.
    - The truncated components are then joined back together into a single string using '.' as the separator.
    - The resulting shortened version string is returned.
- **Output**:
    - A string representing the shortened version number, containing only the specified number of components from the original version string.
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)


---
#### OSGiManifestIT\.increaseVersionNumber<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.increaseVersionNumber}} -->
The `increaseVersionNumber` method increments a specified part of a version number string and removes any lower version parts.
- **Modifiers**: `private`
- **Inputs**:
    - `versionString`: A string representing the version number, formatted as dot-separated integers (e.g., "1.2.3").
    - `position`: An integer indicating the position of the version part to increase, where 0 is the major version, 1 is the minor version, etc.
- **Control Flow**:
    - Initialize an empty list `splitVersion` to store integer parts of the version.
    - Split the `versionString` by '.' and convert each part to an integer, adding it to `splitVersion`.
    - Trim `splitVersion` to only include elements up to the specified `position`.
    - Increment the version part at the specified `position` by 1.
    - Convert the modified `splitVersion` back to a string by joining the elements with '.' and return it.
- **Output**:
    - A string representing the updated version number, with the specified part incremented and lower parts removed.
- **See also**: [`com.google.gson.integration.OSGiManifestIT`](#OSGiManifestIT)  (Base Class)



---
### ManifestData<!-- {{#class:com.google.gson.integration.OSGiManifestIT.ManifestData}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ManifestData` class is a simple data holder used to encapsulate a URL and its associated `Manifest` object, providing a convenient way to manage and pass around these two related pieces of information within the `OSGiManifestIT` integration test class.
- **Fields**:
    - `url`: `URL` A `URL` object representing the location of the manifest file.
    - `manifest`: `Manifest` A `Manifest` object representing the manifest data associated with the URL.
- **Methods**:
    - [`com.google.gson.integration.OSGiManifestIT.ManifestData.ManifestData`](#ManifestDataManifestData)

**Methods**

---
#### ManifestData\.ManifestData<!-- {{#callable:com.google.gson.integration.OSGiManifestIT.ManifestData.ManifestData}} -->
The `ManifestData` constructor initializes an instance with a given URL and Manifest object.
- **Modifiers**: `public`
- **Inputs**:
    - `url`: A `URL` object representing the location of the manifest file.
    - `manifest`: A `Manifest` object containing the manifest data.
- **Control Flow**:
    - Assigns the provided `url` to the instance variable `this.url`.
    - Assigns the provided `manifest` to the instance variable `this.manifest`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `ManifestData` class.
- **See also**: [`com.google.gson.integration.OSGiManifestIT.ManifestData`](#OSGiManifestIT.ManifestData)  (Base Class)



