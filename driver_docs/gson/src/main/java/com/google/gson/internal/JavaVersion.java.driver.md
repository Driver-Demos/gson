# Purpose
The provided Java source code file defines a utility class named [`JavaVersion`](#JavaVersionJavaVersion) within the `com.google.gson.internal` package. This class is designed to determine and provide information about the major version of the Java Runtime Environment (JRE) that the application is currently running on. The class includes methods to parse the Java version string, which can vary in format between legacy versions (e.g., "1.8") and newer versions (e.g., "9.0.4"). The class provides two public static methods: `getMajorJavaVersion()`, which returns the major version number as an integer, and `isJava9OrLater()`, which returns a boolean indicating whether the application is running on Java 9 or a later version. These methods facilitate compatibility checks and conditional logic based on the Java version.

The [`JavaVersion`](#JavaVersionJavaVersion) class is a utility class with a narrow focus, specifically targeting the extraction and interpretation of the Java version from the system properties. It does not define a broad API or external interfaces but rather serves as an internal component likely used by other parts of the Gson library to ensure compatibility with different Java versions. The class is marked as `final`, indicating it is not intended to be subclassed, and it has a private constructor to prevent instantiation, reinforcing its role as a utility class. The code includes robust parsing logic to handle various version string formats and defaults to a minimum supported version if parsing fails, ensuring resilience across different Java environments.
# Imports and Dependencies

---
- `com.google.gson.internal`


# Classes

---
### JavaVersion<!-- {{#class:com.google.gson.internal.JavaVersion}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JavaVersion` class is a utility designed to determine and provide the major version of the Java Runtime Environment (JRE) that the current application is running on. It parses the Java version string obtained from the system properties, handling both legacy and newer version formats, and provides methods to retrieve the major version number and to check if the application is running on Java 9 or later. This class is final and cannot be instantiated, ensuring its utility nature.
- **Fields**:
    - `majorJavaVersion`: `int` A static final integer that holds the major Java version determined at class loading time.
- **Methods**:
    - [`com.google.gson.internal.JavaVersion.determineMajorJavaVersion`](#JavaVersiondetermineMajorJavaVersion)
    - [`com.google.gson.internal.JavaVersion.parseMajorJavaVersion`](#JavaVersionparseMajorJavaVersion)
    - [`com.google.gson.internal.JavaVersion.parseDotted`](#JavaVersionparseDotted)
    - [`com.google.gson.internal.JavaVersion.extractBeginningInt`](#JavaVersionextractBeginningInt)
    - [`com.google.gson.internal.JavaVersion.getMajorJavaVersion`](#JavaVersiongetMajorJavaVersion)
    - [`com.google.gson.internal.JavaVersion.isJava9OrLater`](#JavaVersionisJava9OrLater)
    - [`com.google.gson.internal.JavaVersion.JavaVersion`](#JavaVersionJavaVersion)

**Methods**

---
#### JavaVersion\.determineMajorJavaVersion<!-- {{#callable:com.google.gson.internal.JavaVersion.determineMajorJavaVersion}} -->
The method `determineMajorJavaVersion` retrieves the current Java version from system properties and parses it to determine the major version number.
- **Modifiers**: `private`, `static`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the Java version string from the system property `java.version`.
    - Call the [`parseMajorJavaVersion`](#JavaVersionparseMajorJavaVersion) method with the retrieved Java version string to parse and determine the major version number.
    - Return the major version number obtained from [`parseMajorJavaVersion`](#JavaVersionparseMajorJavaVersion).
- **Output**:
    - The method returns an integer representing the major version number of the current Java runtime environment.
- **Functions called**:
    - [`com.google.gson.internal.JavaVersion.parseMajorJavaVersion`](#JavaVersionparseMajorJavaVersion)
- **See also**: [`com.google.gson.internal.JavaVersion`](#JavaVersion)  (Base Class)


---
#### JavaVersion\.parseMajorJavaVersion<!-- {{#callable:com.google.gson.internal.JavaVersion.parseMajorJavaVersion}} -->
The `parseMajorJavaVersion` method determines the major Java version from a given version string, defaulting to 6 if parsing fails.
- **Modifiers**: `static`
- **Inputs**:
    - `javaVersion`: A string representing the Java version, which may follow different versioning conventions.
- **Control Flow**:
    - Call [`parseDotted`](#JavaVersionparseDotted) with `javaVersion` to attempt parsing the major version from a dotted version string.
    - If [`parseDotted`](#JavaVersionparseDotted) returns -1, indicating failure, call [`extractBeginningInt`](#JavaVersionextractBeginningInt) to attempt extracting the major version from the beginning of the string.
    - If [`extractBeginningInt`](#JavaVersionextractBeginningInt) also returns -1, return 6 as the default major version.
    - Return the parsed major version if successful.
- **Output**:
    - The method returns an integer representing the major Java version, or 6 if parsing fails.
- **Functions called**:
    - [`com.google.gson.internal.JavaVersion.parseDotted`](#JavaVersionparseDotted)
    - [`com.google.gson.internal.JavaVersion.extractBeginningInt`](#JavaVersionextractBeginningInt)
- **See also**: [`com.google.gson.internal.JavaVersion`](#JavaVersion)  (Base Class)


---
#### JavaVersion\.parseDotted<!-- {{#callable:com.google.gson.internal.JavaVersion.parseDotted}} -->
The `parseDotted` method parses a Java version string to determine the major version number.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `javaVersion`: A string representing the Java version, which may be in formats like '1.8' or '9.0.4'.
- **Control Flow**:
    - The method attempts to split the input `javaVersion` string into parts using '.' or '_' as delimiters, limiting to a maximum of three parts.
    - It parses the first part of the split string into an integer `firstVer`.
    - If `firstVer` equals 1 and there is more than one part, it returns the integer value of the second part, which represents the major version in legacy Java versioning (e.g., '1.8').
    - If `firstVer` is not 1, it returns `firstVer` as the major version number for newer Java versioning (e.g., '9').
    - If a `NumberFormatException` occurs during parsing, it catches the exception and returns -1.
- **Output**:
    - The method returns an integer representing the major Java version number, or -1 if parsing fails.
- **See also**: [`com.google.gson.internal.JavaVersion`](#JavaVersion)  (Base Class)


---
#### JavaVersion\.extractBeginningInt<!-- {{#callable:com.google.gson.internal.JavaVersion.extractBeginningInt}} -->
The `extractBeginningInt` method extracts and returns the integer value from the beginning of a given Java version string.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `javaVersion`: A string representing the Java version from which the beginning integer is to be extracted.
- **Control Flow**:
    - Initialize a StringBuilder `num` to accumulate numeric characters.
    - Iterate over each character `c` in the `javaVersion` string.
    - Check if the character `c` is a digit using `Character.isDigit(c)`.
    - If `c` is a digit, append it to `num`; otherwise, break the loop.
    - Convert the accumulated numeric string in `num` to an integer using `Integer.parseInt(num.toString())`.
    - Return the parsed integer.
    - If a `NumberFormatException` occurs during parsing, return -1.
- **Output**:
    - The method returns the integer value extracted from the beginning of the input string, or -1 if no valid integer can be extracted.
- **Functions called**:
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.length`](Streams.java.driver.md#CurrentWritelength)
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.charAt`](Streams.java.driver.md#CurrentWritecharAt)
    - [`com.google.gson.internal.ConstructorConstructor.toString`](ConstructorConstructor.java.driver.md#ConstructorConstructortoString)
- **See also**: [`com.google.gson.internal.JavaVersion`](#JavaVersion)  (Base Class)


---
#### JavaVersion\.getMajorJavaVersion<!-- {{#callable:com.google.gson.internal.JavaVersion.getMajorJavaVersion}} -->
The `getMajorJavaVersion` method returns the major Java version of the current JVM.
- **Modifiers**: `public`, `static`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the static variable `majorJavaVersion`.
- **Output**:
    - The method returns an integer representing the major Java version.
- **See also**: [`com.google.gson.internal.JavaVersion`](#JavaVersion)  (Base Class)


---
#### JavaVersion\.isJava9OrLater<!-- {{#callable:com.google.gson.internal.JavaVersion.isJava9OrLater}} -->
The `isJava9OrLater` method checks if the current Java runtime environment is version 9 or later.
- **Modifiers**: `public`, `static`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the result of the comparison between `majorJavaVersion` and the integer 9.
- **Output**:
    - A boolean value indicating whether the Java version is 9 or later.
- **See also**: [`com.google.gson.internal.JavaVersion`](#JavaVersion)  (Base Class)


---
#### JavaVersion\.JavaVersion<!-- {{#callable:com.google.gson.internal.JavaVersion.JavaVersion}} -->
The `JavaVersion` constructor is a private method that prevents instantiation of the `JavaVersion` utility class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as private, which means it cannot be accessed from outside the class.
    - This effectively prevents any instantiation of the `JavaVersion` class, enforcing its utility nature.
- **Output**:
    - There is no output as this is a constructor method with no return value.
- **See also**: [`com.google.gson.internal.JavaVersion`](#JavaVersion)  (Base Class)



