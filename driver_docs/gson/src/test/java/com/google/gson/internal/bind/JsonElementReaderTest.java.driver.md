# Purpose
The `JsonElementReaderTest` class is a comprehensive suite of unit tests designed to validate the functionality of the `JsonTreeReader` class, which is part of the Google Gson library. This test class is focused on ensuring that the `JsonTreeReader` can accurately parse and handle various JSON structures and data types, including numbers, strings, booleans, nulls, arrays, and objects. The tests cover both lenient and strict parsing modes, particularly in handling special floating-point values like NaN and infinities, which are not typically allowed in JSON. The class also tests the reader's ability to handle nested structures, skip values, and manage incorrect data types gracefully by throwing appropriate exceptions.

The test methods utilize the `JsonParser` to convert JSON strings into `JsonElement` objects, which are then read by the `JsonTreeReader`. Assertions are made using the `Truth` library to verify that the reader's output matches expected values or behaviors. The tests also ensure that the reader correctly identifies and throws exceptions for malformed JSON or when operations are attempted on closed readers. This test suite is crucial for maintaining the robustness and reliability of the `JsonTreeReader` class, ensuring it adheres to expected behaviors when integrated into applications that rely on JSON parsing and manipulation.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonParser`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.Strictness`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.IOException`
- `org.junit.Test`


# Classes

---
### JsonElementReaderTest<!-- {{#class:com.google.gson.internal.bind.JsonElementReaderTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonElementReaderTest` class is a comprehensive test suite for validating the functionality of the `JsonTreeReader` class, which is used to read and parse JSON elements. It includes a variety of test cases that cover different JSON data types such as numbers, strings, booleans, nulls, arrays, and objects. The tests also check the behavior of the reader in both lenient and strict modes, handling of NaN and infinity values, and the ability to skip values and handle incorrect types. Additionally, it tests the reader's response to early closure and nested structures, ensuring robust error handling and correct parsing of JSON data.
- **Methods**:
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testNumbers`](#JsonElementReaderTesttestNumbers)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testLenientNansAndInfinities`](#JsonElementReaderTesttestLenientNansAndInfinities)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testStrictNansAndInfinities`](#JsonElementReaderTesttestStrictNansAndInfinities)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testNumbersFromStrings`](#JsonElementReaderTesttestNumbersFromStrings)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testStringsFromNumbers`](#JsonElementReaderTesttestStringsFromNumbers)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testBooleans`](#JsonElementReaderTesttestBooleans)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testNulls`](#JsonElementReaderTesttestNulls)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testStrings`](#JsonElementReaderTesttestStrings)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testArray`](#JsonElementReaderTesttestArray)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testObject`](#JsonElementReaderTesttestObject)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testEmptyArray`](#JsonElementReaderTesttestEmptyArray)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testNestedArrays`](#JsonElementReaderTesttestNestedArrays)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testNestedObjects`](#JsonElementReaderTesttestNestedObjects)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testEmptyObject`](#JsonElementReaderTesttestEmptyObject)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testSkipValue`](#JsonElementReaderTesttestSkipValue)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testWrongType`](#JsonElementReaderTesttestWrongType)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testNextJsonElement`](#JsonElementReaderTesttestNextJsonElement)
    - [`com.google.gson.internal.bind.JsonElementReaderTest.testEarlyClose`](#JsonElementReaderTesttestEarlyClose)

**Methods**

---
#### JsonElementReaderTest\.testNumbers<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testNumbers}} -->
The `testNumbers` method tests the `JsonTreeReader`'s ability to correctly parse and read integer, long, and double values from a JSON array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonElement` is created by parsing a JSON string representing an array of numbers `[1, 2, 3]`.
    - A `JsonTreeReader` is instantiated with the `JsonElement`.
    - The [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) method is called on the `JsonTreeReader` to start reading the array.
    - The [`nextInt`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt) method is called to read the first element, which is asserted to be equal to 1.
    - The [`nextLong`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextLong) method is called to read the second element, which is asserted to be equal to 2L.
    - The [`nextDouble`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble) method is called to read the third element, which is asserted to be equal to 3.0.
    - The [`endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray) method is called to finish reading the array.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correct parsing of numbers from a JSON array.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextLong`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextLong)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextDouble`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testLenientNansAndInfinities<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testLenientNansAndInfinities}} -->
The method `testLenientNansAndInfinities` tests the ability of `JsonTreeReader` to correctly parse and handle NaN and infinity values in a JSON array when operating in lenient mode.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string '[NaN, -Infinity, Infinity]' into a `JsonElement`.
    - Create a `JsonTreeReader` with the parsed `JsonElement`.
    - Set the `JsonTreeReader` to lenient mode using `setStrictness(Strictness.LENIENT)`.
    - Begin reading the array using `reader.beginArray()`.
    - Assert that the first value read as a double is NaN using `reader.nextDouble()`.
    - Assert that the second value read as a double is equal to `Double.NEGATIVE_INFINITY`.
    - Assert that the third value read as a double is equal to `Double.POSITIVE_INFINITY`.
    - End reading the array using `reader.endArray()`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonTreeReader` in lenient mode.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextDouble`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testStrictNansAndInfinities<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testStrictNansAndInfinities}} -->
The `testStrictNansAndInfinities` method tests the behavior of `JsonTreeReader` when reading a JSON array containing NaN and infinity values under strict parsing rules.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string '[NaN, -Infinity, Infinity]' into a `JsonElement`.
    - Create a `JsonTreeReader` with the parsed `JsonElement`.
    - Set the reader's strictness to `Strictness.LEGACY_STRICT`.
    - Begin reading the array using `reader.beginArray()`.
    - Attempt to read the first element as a double, expecting a `MalformedJsonException` due to NaN, and verify the exception message.
    - Read the first element as a string and verify it is 'NaN'.
    - Attempt to read the second element as a double, expecting a `MalformedJsonException` due to -Infinity, and verify the exception message.
    - Read the second element as a string and verify it is '-Infinity'.
    - Attempt to read the third element as a double, expecting a `MalformedJsonException` due to Infinity, and verify the exception message.
    - Read the third element as a string and verify it is 'Infinity'.
    - End reading the array using `reader.endArray()`.
- **Output**:
    - The method does not return any value but asserts the expected exceptions and messages when reading NaN and infinity values in strict mode.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextDouble`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextString)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testNumbersFromStrings<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testNumbersFromStrings}} -->
The `testNumbersFromStrings` method tests the ability of `JsonTreeReader` to correctly parse and convert string representations of numbers in a JSON array to their respective numeric types.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string array ["1", "2", "3"] is parsed into a `JsonElement`.
    - A `JsonTreeReader` is initialized with the parsed `JsonElement`.
    - The [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) method is called to start reading the array.
    - The [`nextInt`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt) method is called to read the first element as an integer and assert it equals 1.
    - The [`nextLong`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextLong) method is called to read the second element as a long and assert it equals 2L.
    - The [`nextDouble`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble) method is called to read the third element as a double and assert it equals 3.0.
    - The [`endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray) method is called to finish reading the array.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextLong`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextLong)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextDouble`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testStringsFromNumbers<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testStringsFromNumbers}} -->
The `testStringsFromNumbers` method tests the conversion of a numeric JSON element to a string using a `JsonTreeReader`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse the JSON string "[1]" into a `JsonElement`.
    - Create a `JsonTreeReader` with the parsed `JsonElement`.
    - Begin reading the array using `reader.beginArray()`.
    - Assert that the next string read from the `JsonTreeReader` is equal to "1" using `assertThat(reader.nextString()).isEqualTo("1")`.
    - End reading the array using `reader.endArray()`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextString)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testBooleans<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testBooleans}} -->
The `testBooleans` method tests the reading of boolean values from a JSON array using a `JsonTreeReader`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse the JSON string '[true, false]' into a `JsonElement`.
    - Create a `JsonTreeReader` with the parsed `JsonElement`.
    - Begin reading the array using `reader.beginArray()`.
    - Assert that the first boolean value read is `true` using `reader.nextBoolean()`.
    - Assert that the second boolean value read is `false` using `reader.nextBoolean()`.
    - End reading the array using `reader.endArray()`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of `JsonTreeReader` when reading boolean values.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextBoolean`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextBoolean)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testNulls<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testNulls}} -->
The `testNulls` method tests the ability of `JsonTreeReader` to correctly handle and read null values from a JSON array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string '[null,null]' into a `JsonElement`.
    - Create a `JsonTreeReader` using the parsed `JsonElement`.
    - Begin reading the array using `reader.beginArray()`.
    - Read the first null value using `reader.nextNull()`.
    - Read the second null value using `reader.nextNull()`.
    - End reading the array using `reader.endArray()`.
- **Output**:
    - The method does not return any value; it is a test method that verifies the correct handling of null values in a JSON array by the `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextNull`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextNull)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testStrings<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testStrings}} -->
The `testStrings` method tests the functionality of reading string elements from a JSON array using a `JsonTreeReader`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse the JSON string '["A","B"]' into a `JsonElement`.
    - Create a `JsonTreeReader` object using the parsed `JsonElement`.
    - Call `beginArray()` on the reader to start reading the array.
    - Use `nextString()` to read the first string element and assert it equals 'A'.
    - Use `nextString()` to read the second string element and assert it equals 'B'.
    - Call `endArray()` on the reader to finish reading the array.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextString)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testArray<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testArray}} -->
The `testArray` method tests the functionality of reading a JSON array using `JsonTreeReader` and verifies the sequence of JSON tokens and values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string '[1, 2, 3]' into a `JsonElement`.
    - Create a `JsonTreeReader` object using the parsed `JsonElement`.
    - Assert that the first token is `JsonToken.BEGIN_ARRAY`.
    - Begin reading the array using `reader.beginArray()`.
    - Assert that the next token is `JsonToken.NUMBER` and the next integer value is 1.
    - Assert that the next token is `JsonToken.NUMBER` and the next integer value is 2.
    - Assert that the next token is `JsonToken.NUMBER` and the next integer value is 3.
    - Assert that the next token is `JsonToken.END_ARRAY`.
    - End reading the array using `reader.endArray()`.
    - Assert that the next token is `JsonToken.END_DOCUMENT`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testObject<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testObject}} -->
The `testObject` method tests the functionality of reading a JSON object using `JsonTreeReader` and verifies the correct parsing of its elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string '{"A": 1, "B": 2}' into a `JsonElement`.
    - Create a `JsonTreeReader` instance with the parsed `JsonElement`.
    - Assert that the first token is `JsonToken.BEGIN_OBJECT`.
    - Begin reading the object using `reader.beginObject()`.
    - Assert that the next token is `JsonToken.NAME` and the name is 'A'.
    - Assert that the next token is `JsonToken.NUMBER` and the number is 1.
    - Assert that the next token is `JsonToken.NAME` and the name is 'B'.
    - Assert that the next token is `JsonToken.NUMBER` and the number is 2.
    - Assert that the next token is `JsonToken.END_OBJECT`.
    - End reading the object using `reader.endObject()`.
    - Assert that the next token is `JsonToken.END_DOCUMENT`.
- **Output**:
    - The method does not return any value but performs assertions to verify the correct parsing of a JSON object.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testEmptyArray<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testEmptyArray}} -->
The `testEmptyArray` method tests the ability of `JsonTreeReader` to correctly handle an empty JSON array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse an empty JSON array string "[]" into a `JsonElement`.
    - Create a `JsonTreeReader` object using the parsed `JsonElement`.
    - Invoke `beginArray()` on the `JsonTreeReader` to start reading the array.
    - Invoke `endArray()` on the `JsonTreeReader` to finish reading the array.
- **Output**:
    - The method does not return any value; it is a test method that verifies the correct handling of an empty JSON array by the `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testNestedArrays<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testNestedArrays}} -->
The `testNestedArrays` method tests the ability of `JsonTreeReader` to correctly navigate through nested JSON arrays.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string representing nested arrays '[[],[[]]]' into a `JsonElement`.
    - Create a `JsonTreeReader` object using the parsed `JsonElement`.
    - Begin reading the outermost array using `reader.beginArray()`.
    - Begin reading the first inner array using `reader.beginArray()`, then immediately end it with `reader.endArray()`.
    - Begin reading the second inner array using `reader.beginArray()`, then begin and end another nested array within it using `reader.beginArray()` and `reader.endArray()`.
    - End the second inner array with `reader.endArray()`.
    - End the outermost array with `reader.endArray()`.
- **Output**:
    - The method does not return any value; it is a test method that verifies the correct behavior of `JsonTreeReader` when handling nested arrays.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testNestedObjects<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testNestedObjects}} -->
The `testNestedObjects` method tests the ability of `JsonTreeReader` to correctly parse and navigate through a JSON object with nested objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string '{"A":{},"B":{"C":{}}}' into a `JsonElement`.
    - Create a `JsonTreeReader` using the parsed `JsonElement`.
    - Begin reading the JSON object using `reader.beginObject()`.
    - Assert that the first name in the object is 'A' using `reader.nextName()`.
    - Begin and immediately end reading the empty object associated with 'A'.
    - Assert that the next name in the object is 'B'.
    - Begin reading the object associated with 'B'.
    - Assert that the next name in the nested object is 'C'.
    - Begin and immediately end reading the empty object associated with 'C'.
    - End reading the object associated with 'B'.
    - End reading the outer JSON object.
- **Output**:
    - The method does not return any value; it performs assertions to validate the JSON parsing behavior.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testEmptyObject<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testEmptyObject}} -->
The `testEmptyObject` method tests the ability of `JsonTreeReader` to correctly handle an empty JSON object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse an empty JSON object string "{}" into a `JsonElement`.
    - Create a `JsonTreeReader` instance using the parsed `JsonElement`.
    - Invoke `beginObject()` on the `JsonTreeReader` to start reading the JSON object.
    - Invoke `endObject()` on the `JsonTreeReader` to finish reading the JSON object.
- **Output**:
    - The method does not return any value; it is a test method that verifies the correct handling of an empty JSON object by the `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testSkipValue<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testSkipValue}} -->
The `testSkipValue` method tests the [`skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue) functionality of the `JsonTreeReader` by skipping over certain elements in a JSON array and verifying the correct elements are read.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string into a `JsonElement` representing an array with mixed elements including strings, objects, and null.
    - Create a `JsonTreeReader` to read through the `JsonElement`.
    - Begin reading the array using `reader.beginArray()`.
    - Read the first string element and assert it equals "A".
    - Skip the next element (an object) using `reader.skipValue()`.
    - Read the next string element and assert it equals "C".
    - Skip the next element (an array) using `reader.skipValue()`.
    - Read the next string element and assert it equals "D".
    - Skip the next element (null) using `reader.skipValue()`.
    - End reading the array using `reader.endArray()`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the [`skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue) method.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextString)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testWrongType<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testWrongType}} -->
The `testWrongType` method tests the behavior of `JsonTreeReader` when attempting to read JSON elements with incorrect types, ensuring that appropriate exceptions are thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string '[[],"A"]' into a `JsonElement`.
    - Create a `JsonTreeReader` with the parsed `JsonElement`.
    - Begin reading the array using `reader.beginArray()`.
    - Attempt to read various types (boolean, null, string, int, long, double, name, object) from the first element (an empty array) and assert that `IllegalStateException` is thrown for each attempt.
    - Attempt to end the array and object, asserting `IllegalStateException` is thrown for each.
    - Begin and end the nested empty array using `reader.beginArray()` and `reader.endArray()`.
    - Attempt to read various types (boolean, null, int, long, double, name) from the second element (a string "A") and assert that `IllegalStateException` or `NumberFormatException` is thrown as appropriate.
    - Read the string "A" using `reader.nextString()` and assert it equals "A".
    - End the array using `reader.endArray()`.
- **Output**:
    - The method does not return any value; it performs assertions to verify that exceptions are thrown as expected when reading JSON elements with incorrect types.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextBoolean`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextBoolean)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextNull`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextNull)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextString)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextLong`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextLong)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextDouble`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextDouble)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testNextJsonElement<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testNextJsonElement}} -->
The `testNextJsonElement` method tests the behavior of the [`nextJsonElement`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextJsonElement) method in `JsonTreeReader` when reading a JSON object with various structures.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Parse a JSON string into a `JsonElement` object representing a JSON object with keys 'A', 'B', and 'C'.
    - Create a `JsonTreeReader` instance with the parsed `JsonElement`.
    - Begin reading the JSON object using `reader.beginObject()`.
    - Assert that calling `reader.nextJsonElement()` throws an `IllegalStateException` with a specific message when the next token is a name.
    - Read the next name 'A' and assert that `reader.nextJsonElement()` returns a `JsonPrimitive` with value 1.
    - Read the next name 'B', begin an object, and assert that calling `reader.nextJsonElement()` throws an `IllegalStateException`.
    - End the object for 'B'.
    - Read the next name 'C', begin an array, and assert that calling `reader.nextJsonElement()` throws an `IllegalStateException`.
    - End the array for 'C' and the main object.
    - Assert that calling `reader.nextJsonElement()` throws an `IllegalStateException` after the object is fully read.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of [`nextJsonElement`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextJsonElement).
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextJsonElement`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextJsonElement)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)


---
#### JsonElementReaderTest\.testEarlyClose<!-- {{#callable:com.google.gson.internal.bind.JsonElementReaderTest.testEarlyClose}} -->
The `testEarlyClose` method tests the behavior of a `JsonTreeReader` when it is closed prematurely and an attempt is made to read from it.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonElement` is created by parsing a JSON string representing an array `[1, 2, 3]`.
    - A `JsonTreeReader` is instantiated with the `JsonElement`.
    - The [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) method is called on the `JsonTreeReader` to start reading the array.
    - The [`close`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderclose) method is called on the `JsonTreeReader` to close it prematurely.
    - An `IllegalStateException` is expected to be thrown when [`peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek) is called on the closed `JsonTreeReader`.
    - The exception message is asserted to be 'JsonReader is closed'.
- **Output**:
    - The method does not return any value but asserts that an `IllegalStateException` is thrown with a specific message when attempting to read from a closed `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.close`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderclose)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
- **See also**: [`com.google.gson.internal.bind.JsonElementReaderTest`](#JsonElementReaderTest)  (Base Class)



