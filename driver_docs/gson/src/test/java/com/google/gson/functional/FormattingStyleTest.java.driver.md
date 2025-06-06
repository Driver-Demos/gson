# Purpose
The provided Java source code file is a set of functional tests for the `FormattingStyle` feature in the Gson library, which is a popular Java library for converting Java objects to JSON and vice versa. The tests are designed to verify the correct behavior of different JSON formatting styles, specifically focusing on the pretty and compact formatting options. The file uses JUnit4 as the testing framework and includes various test cases to ensure that JSON output adheres to specified formatting styles, such as different newline and indentation configurations. The tests also validate the ability to switch between compact and pretty styles using the `withX` methods provided by the `FormattingStyle` class.

The code is structured to cover a broad range of formatting scenarios, including default formatting, various combinations of newline and indent styles, and the conversion between compact and pretty styles. It also includes validation tests to ensure that only valid newline and indent characters are accepted. The use of `assertThat` from the Truth library and `assertThrows` from JUnit ensures that the tests are both expressive and robust. The file does not define public APIs or external interfaces but rather serves as an internal validation tool to ensure the reliability and correctness of the `FormattingStyle` feature within the Gson library.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.FormattingStyle`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.reflect.TypeToken`
- `java.util.Arrays`
- `java.util.LinkedHashMap`
- `java.util.List`
- `java.util.Map`
- `org.junit.Test`
- `org.junit.runner.RunWith`
- `org.junit.runners.JUnit4`


# Classes

---
### FormattingStyleTest<!-- {{#class:com.google.gson.functional.FormattingStyleTest}} -->
- **Modifiers**: `public`
- **Description**: The `FormattingStyleTest` class is a JUnit test class designed to validate the functionality of different JSON formatting styles using the Gson library. It tests various combinations of newline and indent styles, ensuring that JSON strings are correctly formatted and parsed according to the specified `FormattingStyle`. The class includes tests for default, compact, and pretty formatting styles, as well as conversions between compact and pretty styles. It also includes validation tests to ensure that only valid newline and indent characters are used.
- **Fields**:
    - `TEST_NEWLINES`: `String[]` An array of strings representing various newline characters to be tested.
    - `TEST_INDENTS`: `String[]` An array of strings representing various indent styles to be tested.
- **Methods**:
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
    - [`com.google.gson.functional.FormattingStyleTest.buildExpected`](#FormattingStyleTestbuildExpected)
    - [`com.google.gson.functional.FormattingStyleTest.testDefault`](#FormattingStyleTesttestDefault)
    - [`com.google.gson.functional.FormattingStyleTest.testVariousCombinationsParse`](#FormattingStyleTesttestVariousCombinationsParse)
    - [`com.google.gson.functional.FormattingStyleTest.toJson`](#FormattingStyleTesttoJson)
    - [`com.google.gson.functional.FormattingStyleTest.testFormatCompact`](#FormattingStyleTesttestFormatCompact)
    - [`com.google.gson.functional.FormattingStyleTest.testFormatPretty`](#FormattingStyleTesttestFormatPretty)
    - [`com.google.gson.functional.FormattingStyleTest.testFormatPrettySingleLine`](#FormattingStyleTesttestFormatPrettySingleLine)
    - [`com.google.gson.functional.FormattingStyleTest.testFormat`](#FormattingStyleTesttestFormat)
    - [`com.google.gson.functional.FormattingStyleTest.testCompactToPretty`](#FormattingStyleTesttestCompactToPretty)
    - [`com.google.gson.functional.FormattingStyleTest.testPrettyToCompact`](#FormattingStyleTesttestPrettyToCompact)
    - [`com.google.gson.functional.FormattingStyleTest.testStyleValidations`](#FormattingStyleTesttestStyleValidations)

**Methods**

---
#### FormattingStyleTest\.createInput<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.createInput}} -->
The `createInput` method initializes and returns a map with a single key-value pair, where the key is a string and the value is a list of integers.
- **Modifiers**: `private`, `static`
- **Inputs**: None
- **Control Flow**:
    - A new `LinkedHashMap` is instantiated and assigned to the variable `map`.
    - A key-value pair is added to the map, with the key being the string "a" and the value being a list containing the integers 1 and 2.
    - The map is returned as the output of the method.
- **Output**:
    - A `Map<String, List<Integer>>` containing a single entry with key "a" and value `[1, 2]`.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.buildExpected<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.buildExpected}} -->
The `buildExpected` method constructs a JSON-like string template with customizable newline, indentation, and spacing after separators.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `newline`: A string representing the newline character(s) to be used in the output.
    - `indent`: A string representing the indentation to be used in the output.
    - `spaceAfterSeparators`: A boolean indicating whether to include a space after separators like colons and commas.
- **Control Flow**:
    - Initialize a string `expected` with a template containing placeholders for newline, indent, colon space, and comma space.
    - Determine the `commaSpace` string based on the `spaceAfterSeparators` flag and whether `newline` is empty.
    - Replace placeholders in the `expected` string with the actual `newline`, `indent`, and calculated spaces.
    - Return the modified `expected` string.
- **Output**:
    - A string representing the formatted JSON-like structure with specified newline, indentation, and spacing.
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testDefault<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testDefault}} -->
The `testDefault` method tests the default pretty-printing JSON serialization of a specific input map using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created with pretty-printing enabled using `GsonBuilder`.
    - The [`createInput`](#FormattingStyleTestcreateInput) method is called to generate a map with a single entry, which is then serialized to a JSON string using the [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` object.
    - The resulting JSON string is compared to an expected JSON string generated by the [`buildExpected`](#FormattingStyleTestbuildExpected) method with specific formatting parameters (newline, indent, and space after separators).
    - An assertion is made to ensure that the serialized JSON matches the expected JSON format.
- **Output**:
    - The method does not return any value; it performs an assertion to validate JSON formatting.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setPrettyPrinting`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetPrettyPrinting)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
    - [`com.google.gson.functional.FormattingStyleTest.buildExpected`](#FormattingStyleTestbuildExpected)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testVariousCombinationsParse<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testVariousCombinationsParse}} -->
The `testVariousCombinationsParse` method tests the parsing of JSON strings with various combinations of newline and indent styles using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a JSON string `jsonStringMix` with mixed newline and indent styles.
    - Define a `TypeToken` for a `Map<String, List<Integer>>` to specify the expected type of parsed JSON.
    - Iterate over all combinations of newline and indent styles defined in `TEST_NEWLINES` and `TEST_INDENTS`.
    - For each combination, create a `FormattingStyle` with the current newline and indent, and configure a `Gson` instance with this style.
    - Build an expected JSON string using [`buildExpected`](#FormattingStyleTestbuildExpected) with the current newline and indent.
    - Parse the expected JSON string using `gson.fromJson` and assert that the parsed result matches the expected input created by `createInput()`.
    - Parse the mixed JSON string `jsonStringMix` using `gson.fromJson` and assert that the parsed result matches the expected input created by `createInput()`.
- **Output**:
    - The method does not return a value; it performs assertions to verify that JSON parsing works correctly with various formatting styles.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.withNewline`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithNewline)
    - [`com.google.gson.FormattingStyle.withIndent`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithIndent)
    - [`com.google.gson.GsonBuilder.setFormattingStyle`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetFormattingStyle)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.functional.FormattingStyleTest.buildExpected`](#FormattingStyleTestbuildExpected)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.toJson<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.toJson}} -->
The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method converts an object into its JSON representation using a specified formatting style.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `obj`: The object to be converted into JSON format.
    - `style`: The `FormattingStyle` to be applied to the JSON output, which dictates how the JSON is formatted (e.g., pretty or compact).
- **Control Flow**:
    - A `GsonBuilder` instance is created and configured with the specified `FormattingStyle`.
    - The `GsonBuilder` is used to create a `Gson` instance.
    - The [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method of the `Gson` instance is called with the input object to convert it into a JSON string.
- **Output**:
    - A JSON string representation of the input object, formatted according to the specified `FormattingStyle`.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setFormattingStyle`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetFormattingStyle)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testFormatCompact<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testFormatCompact}} -->
The `testFormatCompact` method tests the JSON formatting of a map using the COMPACT formatting style and verifies the output against expected results.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Call [`toJson`](#FormattingStyleTesttoJson) with `createInput()` and `FormattingStyle.COMPACT` to generate a JSON string.
    - Call [`buildExpected`](#FormattingStyleTestbuildExpected) with empty strings and `false` to generate the expected JSON string.
    - Use `assertThat` to check if the generated JSON matches the expected JSON.
    - Perform a sanity check by asserting the generated JSON equals the hardcoded string `{"a":[1,2]}`.
- **Output**:
    - The method does not return any value; it performs assertions to validate JSON formatting.
- **Functions called**:
    - [`com.google.gson.functional.FormattingStyleTest.toJson`](#FormattingStyleTesttoJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
    - [`com.google.gson.functional.FormattingStyleTest.buildExpected`](#FormattingStyleTestbuildExpected)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testFormatPretty<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testFormatPretty}} -->
The `testFormatPretty` method tests the JSON pretty-printing functionality by comparing the output of a JSON conversion to an expected formatted string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Invoke the [`toJson`](#FormattingStyleTesttoJson) method with `createInput()` and `FormattingStyle.PRETTY` to generate a pretty-printed JSON string.
    - Call [`buildExpected`](#FormattingStyleTestbuildExpected) with newline, indent, and spaceAfterSeparators parameters to create the expected JSON string.
    - Use `assertThat` to verify that the generated JSON string matches the expected JSON string.
    - Perform a sanity check by asserting that the generated JSON string matches a hardcoded pretty-printed JSON string.
- **Output**:
    - The method does not return any value; it performs assertions to validate JSON formatting.
- **Functions called**:
    - [`com.google.gson.functional.FormattingStyleTest.toJson`](#FormattingStyleTesttoJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
    - [`com.google.gson.functional.FormattingStyleTest.buildExpected`](#FormattingStyleTestbuildExpected)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testFormatPrettySingleLine<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testFormatPrettySingleLine}} -->
The `testFormatPrettySingleLine` method tests the JSON formatting functionality using a compact style with spaces after separators.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `FormattingStyle` object is created with the `COMPACT` style and configured to have spaces after separators.
    - The [`toJson`](#FormattingStyleTesttoJson) method is called with the input data and the specified formatting style to generate a JSON string.
    - The generated JSON string is compared to an expected JSON string using the [`buildExpected`](#FormattingStyleTestbuildExpected) method with specific parameters.
    - An assertion checks that the generated JSON matches the expected JSON string.
    - A sanity check assertion verifies that the generated JSON is equal to a hardcoded JSON string `{"a": [1, 2]}`.
- **Output**:
    - The method does not return any value; it performs assertions to validate JSON formatting.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.withSpaceAfterSeparators`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithSpaceAfterSeparators)
    - [`com.google.gson.functional.FormattingStyleTest.toJson`](#FormattingStyleTesttoJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
    - [`com.google.gson.functional.FormattingStyleTest.buildExpected`](#FormattingStyleTestbuildExpected)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testFormat<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testFormat}} -->
The `testFormat` method tests various combinations of newline, indent, and space after separators in JSON formatting to ensure the output matches the expected format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Iterates over each string in `TEST_NEWLINES` array to use as a newline character.
    - For each newline, iterates over each string in `TEST_INDENTS` array to use as an indent.
    - For each combination of newline and indent, iterates over a boolean array to determine if a space should be added after separators.
    - Creates a `FormattingStyle` object with the current newline, indent, and space after separators settings.
    - Converts a predefined input object to JSON using the current `FormattingStyle`.
    - Builds the expected JSON string using the same newline, indent, and space after separators settings.
    - Asserts that the generated JSON string matches the expected JSON string.
- **Output**:
    - The method does not return a value; it performs assertions to validate JSON formatting.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.withNewline`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithNewline)
    - [`com.google.gson.FormattingStyle.withIndent`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithIndent)
    - [`com.google.gson.FormattingStyle.withSpaceAfterSeparators`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithSpaceAfterSeparators)
    - [`com.google.gson.functional.FormattingStyleTest.toJson`](#FormattingStyleTesttoJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
    - [`com.google.gson.functional.FormattingStyleTest.buildExpected`](#FormattingStyleTestbuildExpected)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testCompactToPretty<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testCompactToPretty}} -->
The `testCompactToPretty` method verifies that a JSON object formatted using a modified COMPACT style matches the output of the PRETTY style.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `FormattingStyle` object is created by modifying the `COMPACT` style to include a newline character, an indent of two spaces, and spaces after separators.
    - The [`toJson`](#FormattingStyleTesttoJson) method is called with the input object and the modified `FormattingStyle`, producing a JSON string.
    - The [`toJson`](#FormattingStyleTesttoJson) method is called again with the input object and the `PRETTY` style, producing another JSON string.
    - An assertion checks that the JSON string from the modified `COMPACT` style is equal to the JSON string from the `PRETTY` style.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the formatting conversion.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.withNewline`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithNewline)
    - [`com.google.gson.FormattingStyle.withIndent`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithIndent)
    - [`com.google.gson.FormattingStyle.withSpaceAfterSeparators`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithSpaceAfterSeparators)
    - [`com.google.gson.functional.FormattingStyleTest.toJson`](#FormattingStyleTesttoJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testPrettyToCompact<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testPrettyToCompact}} -->
The `testPrettyToCompact` method verifies that a JSON object formatted using a modified 'PRETTY' style matches the same object formatted using the 'COMPACT' style.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `FormattingStyle` object is created by modifying the `PRETTY` style to have no newline, no indent, and no space after separators.
    - The [`toJson`](#FormattingStyleTesttoJson) method is called with the [`createInput`](#FormattingStyleTestcreateInput) object and the modified `FormattingStyle`, producing a JSON string.
    - The [`toJson`](#FormattingStyleTesttoJson) method is called again with the [`createInput`](#FormattingStyleTestcreateInput) object and the `COMPACT` style, producing another JSON string.
    - An assertion checks that the two JSON strings are equal, ensuring the modified `PRETTY` style produces the same output as the `COMPACT` style.
- **Output**:
    - The method does not return any value; it performs an assertion to validate JSON formatting.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.withNewline`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithNewline)
    - [`com.google.gson.FormattingStyle.withIndent`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithIndent)
    - [`com.google.gson.FormattingStyle.withSpaceAfterSeparators`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithSpaceAfterSeparators)
    - [`com.google.gson.functional.FormattingStyleTest.toJson`](#FormattingStyleTesttoJson)
    - [`com.google.gson.functional.FormattingStyleTest.createInput`](#FormattingStyleTestcreateInput)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)


---
#### FormattingStyleTest\.testStyleValidations<!-- {{#callable:com.google.gson.functional.FormattingStyleTest.testStyleValidations}} -->
The `testStyleValidations` method tests the validation logic of the `FormattingStyle` class to ensure that only valid newline and indent characters are accepted.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to verify that an `IllegalArgumentException` is thrown when invalid newline characters (`\u2028`, `NL`) are passed to `FormattingStyle.PRETTY.withNewline`.
    - It checks that the exception message is 'Only combinations of \n and \r are allowed in newline.' for invalid newline inputs.
    - The method also uses `assertThrows` to verify that an `IllegalArgumentException` is thrown when an invalid indent character (`\f`) is passed to `FormattingStyle.PRETTY.withIndent`.
    - It checks that the exception message is 'Only combinations of spaces and tabs are allowed in indent.' for the invalid indent input.
- **Output**:
    - The method does not return any value; it is a test method that asserts the correct exceptions and messages are produced for invalid inputs.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.withNewline`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithNewline)
    - [`com.google.gson.FormattingStyle.withIndent`](../../../../../../main/java/com/google/gson/FormattingStyle.java.driver.md#FormattingStylewithIndent)
- **See also**: [`com.google.gson.functional.FormattingStyleTest`](#FormattingStyleTest)  (Base Class)



