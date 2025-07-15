# Purpose
The `PrintFormattingTest` class is a functional test suite designed to validate the JSON formatting capabilities of the Gson library, specifically focusing on whitespace handling and null value serialization. This class is part of the `com.google.gson.functional` package and utilizes the JUnit testing framework to execute its tests. The primary technical components include the `Gson` and `GsonBuilder` classes from the Gson library, which are used to serialize Java objects into JSON strings. The tests within this class ensure that JSON output can be generated without unnecessary whitespace and that null values can be handled according to different serialization configurations.

The class contains several test methods, each targeting specific aspects of JSON formatting. The [`testCompactFormattingLeavesNoWhiteSpace`](#PrintFormattingTesttestCompactFormattingLeavesNoWhiteSpace) method verifies that the JSON output of a list of objects does not contain any whitespace, ensuring compact formatting. The [`testJsonObjectWithNullValues`](#PrintFormattingTesttestJsonObjectWithNullValues) and [`testJsonObjectWithNullValuesSerialized`](#PrintFormattingTesttestJsonObjectWithNullValuesSerialized) methods test the behavior of JSON serialization with null values, with the latter method using a `GsonBuilder` configured to serialize nulls. These tests collectively ensure that the Gson library's formatting features work as expected, providing a reliable mechanism for JSON serialization in applications that require precise control over output formatting.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonObject`
- `com.google.gson.common.TestTypes.BagOfPrimitives`
- `com.google.gson.common.TestTypes.ClassWithTransientFields`
- `com.google.gson.common.TestTypes.Nested`
- `com.google.gson.common.TestTypes.PrimitiveArray`
- `java.util.ArrayList`
- `java.util.List`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### PrintFormattingTest<!-- {{#class:com.google.gson.functional.PrintFormattingTest}} -->
- **Modifiers**: `public`
- **Description**: The `PrintFormattingTest` class is a JUnit test class designed to perform functional tests on JSON print formatting using the Gson library. It includes tests to verify that JSON serialization can be done without whitespace, and to check the behavior of JSON serialization with null values, both with and without the `serializeNulls` option enabled. The class uses a `Gson` instance to serialize objects and includes utility methods to assert the absence of whitespace in JSON strings.
- **Fields**:
    - `gson`: `Gson` An instance of the Gson class used for JSON serialization in the tests.
- **Methods**:
    - [`com.google.gson.functional.PrintFormattingTest.setUp`](#PrintFormattingTestsetUp)
    - [`com.google.gson.functional.PrintFormattingTest.testCompactFormattingLeavesNoWhiteSpace`](#PrintFormattingTesttestCompactFormattingLeavesNoWhiteSpace)
    - [`com.google.gson.functional.PrintFormattingTest.testJsonObjectWithNullValues`](#PrintFormattingTesttestJsonObjectWithNullValues)
    - [`com.google.gson.functional.PrintFormattingTest.testJsonObjectWithNullValuesSerialized`](#PrintFormattingTesttestJsonObjectWithNullValuesSerialized)
    - [`com.google.gson.functional.PrintFormattingTest.assertContainsNoWhiteSpace`](#PrintFormattingTestassertContainsNoWhiteSpace)

**Methods**

---
#### PrintFormattingTest\.setUp<!-- {{#callable:com.google.gson.functional.PrintFormattingTest.setUp}} -->
The setUp method initializes the Gson object before each test is executed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with @Before, indicating it runs before each test method in the class.
    - A new instance of Gson is created and assigned to the gson field.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.functional.PrintFormattingTest`](#PrintFormattingTest)  (Base Class)


---
#### PrintFormattingTest\.testCompactFormattingLeavesNoWhiteSpace<!-- {{#callable:com.google.gson.functional.PrintFormattingTest.testCompactFormattingLeavesNoWhiteSpace}} -->
The method `testCompactFormattingLeavesNoWhiteSpace` verifies that the JSON serialization of a list of objects contains no whitespace.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a new `ArrayList` of `Object` type.
    - Add instances of `BagOfPrimitives`, `Nested`, `PrimitiveArray`, and `ClassWithTransientFields` to the list.
    - Convert the list to a JSON string using the `gson.toJson` method.
    - Call [`assertContainsNoWhiteSpace`](#PrintFormattingTestassertContainsNoWhiteSpace) to ensure the JSON string contains no whitespace.
- **Output**:
    - The method does not return a value; it performs an assertion to check for whitespace in the JSON string.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.PrintFormattingTest.assertContainsNoWhiteSpace`](#PrintFormattingTestassertContainsNoWhiteSpace)
- **See also**: [`com.google.gson.functional.PrintFormattingTest`](#PrintFormattingTest)  (Base Class)


---
#### PrintFormattingTest\.testJsonObjectWithNullValues<!-- {{#callable:com.google.gson.functional.PrintFormattingTest.testJsonObjectWithNullValues}} -->
The method `testJsonObjectWithNullValues` tests the behavior of Gson serialization when a JsonObject contains a null value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new JsonObject `obj` is created.
    - A property 'field1' with value 'value1' is added to `obj`.
    - A property 'field2' with a null value is added to `obj`.
    - The JsonObject `obj` is serialized to a JSON string using `gson.toJson()`.
    - The resulting JSON string is checked to ensure it contains 'field1'.
    - The resulting JSON string is checked to ensure it does not contain 'field2'.
- **Output**:
    - The method does not return any value; it performs assertions to validate the JSON serialization behavior.
- **Functions called**:
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrintFormattingTest`](#PrintFormattingTest)  (Base Class)


---
#### PrintFormattingTest\.testJsonObjectWithNullValuesSerialized<!-- {{#callable:com.google.gson.functional.PrintFormattingTest.testJsonObjectWithNullValuesSerialized}} -->
The method tests that a JSON object with null values is serialized correctly when using Gson with the serializeNulls option enabled.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created with the serializeNulls option enabled using GsonBuilder.
    - A JsonObject is instantiated and two properties are added: 'field1' with a non-null value and 'field2' with a null value.
    - The JsonObject is serialized into a JSON string using the Gson instance.
    - Assertions are made to verify that the JSON string contains both 'field1' and 'field2', ensuring that null values are serialized.
- **Output**:
    - The method does not return any value; it performs assertions to validate JSON serialization behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.serializeNulls`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeNulls)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrintFormattingTest`](#PrintFormattingTest)  (Base Class)


---
#### PrintFormattingTest\.assertContainsNoWhiteSpace<!-- {{#callable:com.google.gson.functional.PrintFormattingTest.assertContainsNoWhiteSpace}} -->
The method `assertContainsNoWhiteSpace` checks that a given string contains no whitespace characters.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `str`: The string to be checked for the absence of whitespace characters.
- **Control Flow**:
    - Convert the input string `str` into a character array using `toCharArray()`.
    - Iterate over each character `c` in the character array.
    - For each character `c`, assert that `Character.isWhitespace(c)` is false, meaning `c` is not a whitespace character.
- **Output**:
    - The method does not return a value; it throws an assertion error if any whitespace character is found in the string.
- **See also**: [`com.google.gson.functional.PrintFormattingTest`](#PrintFormattingTest)  (Base Class)



