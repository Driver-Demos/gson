# Purpose
The `JsonTreeWriterTest` class is a comprehensive suite of unit tests designed to validate the functionality of the `JsonTreeWriter` class, which is part of the Google Gson library. This test class ensures that the `JsonTreeWriter` correctly constructs JSON data structures in memory, represented as `JsonElement` trees, rather than writing directly to an output stream. The tests cover a wide range of scenarios, including writing arrays and objects, handling nested structures, managing null values, and enforcing strictness rules for JSON writing. The class also tests the behavior of the `JsonTreeWriter` when dealing with special floating-point values like NaN and infinities, both in lenient and strict modes.

The test methods utilize assertions to verify the expected outcomes of various operations, such as beginning and ending JSON arrays and objects, writing values, and handling exceptions when operations are performed in an incorrect order or context. The tests also ensure that the `JsonTreeWriter` overrides all necessary methods from the `JsonWriter` class to fulfill its role of creating JSON element trees. This test suite is crucial for maintaining the reliability and correctness of the `JsonTreeWriter` functionality, ensuring that it adheres to the expected behavior and handles edge cases appropriately.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonNull`
- `com.google.gson.Strictness`
- `com.google.gson.common.MoreAsserts`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.io.Writer`
- `java.util.Arrays`
- `java.util.List`
- `org.junit.Test`


# Classes

---
### JsonTreeWriterTest<!-- {{#class:com.google.gson.internal.bind.JsonTreeWriterTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonTreeWriterTest` class is a comprehensive test suite for the `JsonTreeWriter` class, which is part of the Gson library. It contains a series of unit tests that validate the functionality of `JsonTreeWriter` in various scenarios, such as writing JSON arrays and objects, handling nested structures, managing strictness levels, and dealing with special cases like NaN and infinity values. The tests ensure that `JsonTreeWriter` correctly constructs JSON elements and handles errors appropriately, such as attempting to write after closing the writer or using names incorrectly in arrays.
- **Methods**:
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testArray`](#JsonTreeWriterTesttestArray)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testNestedArray`](#JsonTreeWriterTesttestNestedArray)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testObject`](#JsonTreeWriterTesttestObject)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testNestedObject`](#JsonTreeWriterTesttestNestedObject)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testWriteAfterClose`](#JsonTreeWriterTesttestWriteAfterClose)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testPrematureClose`](#JsonTreeWriterTesttestPrematureClose)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testNameAsTopLevelValue`](#JsonTreeWriterTesttestNameAsTopLevelValue)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testNameInArray`](#JsonTreeWriterTesttestNameInArray)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testTwoNames`](#JsonTreeWriterTesttestTwoNames)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testSerializeNullsFalse`](#JsonTreeWriterTesttestSerializeNullsFalse)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testSerializeNullsTrue`](#JsonTreeWriterTesttestSerializeNullsTrue)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testEmptyWriter`](#JsonTreeWriterTesttestEmptyWriter)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testBeginArray`](#JsonTreeWriterTesttestBeginArray)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testBeginObject`](#JsonTreeWriterTesttestBeginObject)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testValueString`](#JsonTreeWriterTesttestValueString)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testBoolValue`](#JsonTreeWriterTesttestBoolValue)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testBoolMaisValue`](#JsonTreeWriterTesttestBoolMaisValue)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testLenientNansAndInfinities`](#JsonTreeWriterTesttestLenientNansAndInfinities)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testStrictNansAndInfinities`](#JsonTreeWriterTesttestStrictNansAndInfinities)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testStrictBoxedNansAndInfinities`](#JsonTreeWriterTesttestStrictBoxedNansAndInfinities)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testJsonValue`](#JsonTreeWriterTesttestJsonValue)
    - [`com.google.gson.internal.bind.JsonTreeWriterTest.testOverrides`](#JsonTreeWriterTesttestOverrides)

**Methods**

---
#### JsonTreeWriterTest\.testArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testArray}} -->
The `testArray` method tests the functionality of the `JsonTreeWriter` to correctly write a JSON array with integer values and verify its output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `JsonTreeWriter` object named `writer`.
    - Begin a JSON array using `writer.beginArray()`.
    - Add integer values 1, 2, and 3 to the array using `writer.value()`.
    - End the JSON array using `writer.endArray()`.
    - Assert that the JSON structure created by `writer` matches the expected string representation "[1,2,3]" using `assertThat`.
- **Output**:
    - The method does not return any value, but it asserts that the JSON array created by `JsonTreeWriter` matches the expected output.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterendArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testNestedArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testNestedArray}} -->
The `testNestedArray` method tests the creation of a nested JSON array structure using `JsonTreeWriter` and verifies its correctness.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `JsonTreeWriter` object named `writer`.
    - Begin the first JSON array using `writer.beginArray()`.
    - Begin a nested JSON array within the first array using `writer.beginArray()`, then immediately close it with `writer.endArray()`.
    - Begin another JSON array within the first array using `writer.beginArray()`.
    - Within this second array, begin another nested JSON array using `writer.beginArray()`, then immediately close it with `writer.endArray()`.
    - Close the second array with `writer.endArray()`.
    - Close the first array with `writer.endArray()`.
    - Retrieve the JSON structure as a string using `writer.get().toString()` and assert that it equals the expected string representation "[[],[[]]]".
- **Output**:
    - The method does not return a value but asserts that the JSON structure created by `JsonTreeWriter` matches the expected nested array structure "[[],[[]]]".
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterendArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testObject}} -->
The `testObject` method tests the creation of a JSON object using `JsonTreeWriter` and verifies its string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance is created to facilitate JSON writing.
    - The [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterbeginObject) method is called on the writer to start a new JSON object.
    - The [`name`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWritername) method is used to set the name of the first property to "A", followed by the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method to set its value to 1.
    - The [`name`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWritername) method is used again to set the name of the second property to "B", followed by the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method to set its value to 2.
    - The [`endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterendObject) method is called to complete the JSON object.
    - The `assertThat` method is used to verify that the string representation of the JSON object matches the expected string "{"A":1,"B":2}".
- **Output**:
    - The method does not return any value, but it asserts that the JSON object created matches the expected string representation.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.name`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterendObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testNestedObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testNestedObject}} -->
The `testNestedObject` method tests the creation of a nested JSON object structure using `JsonTreeWriter` and verifies its correctness.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance is created to build a JSON structure.
    - The method begins a new JSON object using `beginObject()`.
    - A name 'A' is added to the object, followed by another nested object.
    - Within the nested object, a name 'B' is added, followed by another empty nested object.
    - The nested objects are closed using `endObject()`.
    - A new name 'C' is added to the main object, followed by an empty nested object.
    - The main object is closed using `endObject()`.
    - The resulting JSON structure is retrieved and converted to a string.
    - An assertion checks if the generated JSON string matches the expected structure `{"A":{"B":{}},"C":{}}`.
- **Output**:
    - The method does not return a value but asserts that the JSON structure created matches the expected string representation.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.name`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWritername)
    - [`com.google.gson.internal.bind.JsonTreeWriter.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterendObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testWriteAfterClose<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testWriteAfterClose}} -->
The `testWriteAfterClose` method tests that attempting to write to a `JsonTreeWriter` after it has been closed throws an `IllegalStateException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance is created.
    - The writer's strictness is set to `Strictness.LENIENT`.
    - An array is begun using `beginArray()`, a value 'A' is added, and the array is ended with `endArray()`.
    - The writer is closed using `close()`.
    - An assertion is made that an `IllegalStateException` is thrown when attempting to begin a new array with `beginArray()` after the writer has been closed.
- **Output**:
    - The method does not return any value but asserts that an `IllegalStateException` is thrown when writing after closing the writer.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterendArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.close`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterclose)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testPrematureClose<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testPrematureClose}} -->
The `testPrematureClose` method tests that closing a `JsonTreeWriter` before completing a JSON document throws an `IOException` with a specific message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `JsonTreeWriter` object named `writer`.
    - Set the strictness of `writer` to `Strictness.LENIENT`.
    - Begin a JSON array using `writer.beginArray()`.
    - Use `assertThrows` to verify that calling `writer.close()` throws an `IOException`.
    - Check that the exception message is 'Incomplete document' using `assertThat`.
- **Output**:
    - The method does not return any value; it is a test method that asserts behavior.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.close`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterclose)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testNameAsTopLevelValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testNameAsTopLevelValue}} -->
The `testNameAsTopLevelValue` method tests the behavior of `JsonTreeWriter` when attempting to write a name at the top level and after closing the writer.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance is created.
    - An `IllegalStateException` is expected and asserted when attempting to write a name 'hello' at the top level, with the message 'Did not expect a name'.
    - A value `12` is written to the writer, and then the writer is closed.
    - Another `IllegalStateException` is expected and asserted when attempting to write a name 'hello' after the writer is closed, with the message 'Please begin an object before writing a name.'
- **Output**:
    - The method does not return any value; it performs assertions to verify the expected exceptions and messages.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.name`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWritername)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.close`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterclose)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testNameInArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testNameInArray}} -->
The `testNameInArray` method tests that attempting to write a name in a JSON array using `JsonTreeWriter` throws an `IllegalStateException` with a specific message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance is created.
    - The method begins a JSON array using `writer.beginArray()`.
    - An `IllegalStateException` is expected and asserted when `writer.name("hello")` is called, verifying the exception message is 'Please begin an object before writing a name.'.
    - A value `12` is added to the array using `writer.value(12)`.
    - Again, an `IllegalStateException` is expected and asserted when `writer.name("hello")` is called, verifying the exception message is 'Please begin an object before writing a name.'.
    - The JSON array is ended using `writer.endArray()`.
    - The final JSON structure is asserted to be `[12]`.
- **Output**:
    - The method does not return a value but asserts that the `JsonTreeWriter` correctly throws exceptions and produces the expected JSON output.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testTwoNames<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testTwoNames}} -->
The `testTwoNames` method tests that attempting to write two consecutive names in a JSON object using `JsonTreeWriter` throws an `IllegalStateException` with a specific message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` object is instantiated.
    - The [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) method is called on the writer to start a new JSON object.
    - The [`name`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername) method is called with the argument "a" to set a name in the JSON object.
    - The `assertThrows` method is used to verify that calling [`name`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername) again with "a" throws an `IllegalStateException`.
    - The exception message is checked to ensure it equals "Did not expect a name".
- **Output**:
    - The method does not return any value; it performs assertions to validate behavior.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testSerializeNullsFalse<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testSerializeNullsFalse}} -->
The method `testSerializeNullsFalse` tests that when null serialization is disabled, null values are not included in the JSON output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` object is instantiated.
    - The [`setSerializeNulls`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetSerializeNulls) method is called on the writer with `false` as an argument to disable null serialization.
    - The writer begins a JSON object with `beginObject()`.
    - A name 'A' is added to the object using `name("A")`.
    - A null value is added to the object using `nullValue()`.
    - The JSON object is closed with `endObject()`.
    - An assertion checks that the resulting JSON string is equal to an empty object `{}`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the `JsonTreeWriter` when null serialization is disabled.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setSerializeNulls`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetSerializeNulls)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testSerializeNullsTrue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testSerializeNullsTrue}} -->
The method `testSerializeNullsTrue` tests the behavior of `JsonTreeWriter` when serializing null values with the `serializeNulls` option set to true.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` object is instantiated.
    - The [`setSerializeNulls`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetSerializeNulls) method is called on the writer with the argument `true`, enabling the serialization of null values.
    - The [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) method is called to start writing a JSON object.
    - The [`name`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername) method is called with the argument "A" to set the name of the next value in the JSON object.
    - The [`nullValue`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue) method is called to write a null value for the previously set name.
    - The [`endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject) method is called to complete the JSON object.
    - The [`get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget) method is called on the writer to retrieve the JSON representation, which is then converted to a string.
    - An assertion is made to check that the resulting JSON string is equal to `{"A":null}`.
- **Output**:
    - The method does not return a value but asserts that the JSON string representation of the object is `{"A":null}`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setSerializeNulls`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetSerializeNulls)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testEmptyWriter<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testEmptyWriter}} -->
The `testEmptyWriter` method verifies that a newly instantiated `JsonTreeWriter` returns `JsonNull.INSTANCE` when its [`get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget) method is called.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a new `JsonTreeWriter` object named `writer`.
    - Use the `assertThat` method to check that the result of `writer.get()` is equal to `JsonNull.INSTANCE`.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the `JsonTreeWriter` is initially empty, represented by `JsonNull.INSTANCE`.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testBeginArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testBeginArray}} -->
The `testBeginArray` method tests that the [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) method of `JsonTreeWriter` returns the writer instance itself.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `JsonTreeWriter` is created.
    - The [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) method is called on the `JsonTreeWriter` instance.
    - An assertion checks that the result of [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) is equal to the `JsonTreeWriter` instance itself.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray).
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testBeginObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testBeginObject}} -->
The `testBeginObject` method tests that the [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) method of `JsonTreeWriter` returns the writer instance itself.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `JsonTreeWriter` is created.
    - The [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) method is called on the `JsonTreeWriter` instance.
    - An assertion checks that the result of [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) is equal to the `JsonTreeWriter` instance itself.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) returns the `JsonTreeWriter` instance.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testValueString<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testValueString}} -->
The `testValueString` method tests that the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method of `JsonTreeWriter` returns the writer itself when a string is passed as an argument.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` object named `writer` is instantiated.
    - A string variable `n` is initialized with the value "as".
    - The [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method of `writer` is called with `n` as the argument.
    - An assertion checks that the result of `writer.value(n)` is equal to `writer` itself.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method returns the `JsonTreeWriter` instance.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testBoolValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testBoolValue}} -->
The `testBoolValue` method tests that the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method of `JsonTreeWriter` correctly handles a boolean input and returns the writer itself.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new instance of `JsonTreeWriter` is created.
    - A boolean variable `bool` is set to `true`.
    - The [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method of `JsonTreeWriter` is called with `bool` as the argument.
    - An assertion checks that the result of `writer.value(bool)` is equal to the `writer` instance itself.
- **Output**:
    - The method does not return any value but asserts that the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method returns the `JsonTreeWriter` instance.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testBoolMaisValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testBoolMaisValue}} -->
The `testBoolMaisValue` method tests that the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method of `JsonTreeWriter` correctly handles a `Boolean` input and returns the writer itself.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` object named `writer` is instantiated.
    - A `Boolean` object named `bool` is initialized with the value `true`.
    - The [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method of `writer` is called with `bool` as the argument.
    - An assertion checks that the result of `writer.value(bool)` is equal to `writer` itself.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the [`value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method returns the `JsonTreeWriter` instance.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testLenientNansAndInfinities<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testLenientNansAndInfinities}} -->
The method `testLenientNansAndInfinities` tests the ability of `JsonTreeWriter` to handle NaN and infinity values in lenient mode.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance is created.
    - The writer's strictness is set to `Strictness.LENIENT`.
    - The writer begins an array context using `beginArray()`.
    - The writer adds `Float.NaN`, `Float.NEGATIVE_INFINITY`, `Float.POSITIVE_INFINITY`, `Double.NaN`, `Double.NEGATIVE_INFINITY`, and `Double.POSITIVE_INFINITY` to the array using the `value()` method.
    - The writer ends the array context using `endArray()`.
    - The resulting JSON string is retrieved and asserted to be equal to "[NaN,-Infinity,Infinity,NaN,-Infinity,Infinity]" using `assertThat()`.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correct handling of NaN and infinity values in lenient mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeWriter.java.driver.md#JsonTreeWriterget)
    - [`com.google.gson.JsonElement.toString`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testStrictNansAndInfinities<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testStrictNansAndInfinities}} -->
The method `testStrictNansAndInfinities` tests that writing NaN and infinity values in strict mode throws an `IllegalArgumentException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` object is instantiated.
    - The writer's strictness is set to `Strictness.LEGACY_STRICT`.
    - The writer begins an array using `beginArray()`.
    - The method asserts that writing `Float.NaN` throws an `IllegalArgumentException`.
    - The method asserts that writing `Float.NEGATIVE_INFINITY` throws an `IllegalArgumentException`.
    - The method asserts that writing `Float.POSITIVE_INFINITY` throws an `IllegalArgumentException`.
    - The method asserts that writing `Double.NaN` throws an `IllegalArgumentException`.
    - The method asserts that writing `Double.NEGATIVE_INFINITY` throws an `IllegalArgumentException`.
    - The method asserts that writing `Double.POSITIVE_INFINITY` throws an `IllegalArgumentException`.
- **Output**:
    - The method does not return any value; it verifies that exceptions are thrown for invalid inputs in strict mode.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testStrictBoxedNansAndInfinities<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testStrictBoxedNansAndInfinities}} -->
The method `testStrictBoxedNansAndInfinities` tests that writing boxed NaN and infinity values to a `JsonTreeWriter` in `LEGACY_STRICT` mode throws an `IllegalArgumentException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance is created.
    - The writer's strictness is set to `Strictness.LEGACY_STRICT`.
    - The writer begins an array context using `beginArray()`.
    - The method asserts that writing `Float.NaN`, `Float.NEGATIVE_INFINITY`, `Float.POSITIVE_INFINITY`, `Double.NaN`, `Double.NEGATIVE_INFINITY`, and `Double.POSITIVE_INFINITY` as boxed values (using `Float.valueOf()` and `Double.valueOf()`) to the writer throws an `IllegalArgumentException`.
- **Output**:
    - The method does not return any value; it is a test method that verifies exceptions are thrown for invalid inputs.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testJsonValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testJsonValue}} -->
The `testJsonValue` method tests that calling [`jsonValue`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterjsonValue) on a `JsonTreeWriter` instance throws an `UnsupportedOperationException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeWriter` instance named `writer` is created.
    - The [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) method is called on `writer` to start an array context.
    - The `assertThrows` method is used to verify that calling [`jsonValue`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterjsonValue) with the argument "test" on `writer` throws an `UnsupportedOperationException`.
- **Output**:
    - The method does not return any value; it is a test method that asserts an exception is thrown.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.stream.JsonWriter.jsonValue`](../../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterjsonValue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)


---
#### JsonTreeWriterTest\.testOverrides<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriterTest.testOverrides}} -->
The `testOverrides` method verifies that the `JsonTreeWriter` class correctly overrides all relevant methods from the `JsonWriter` class, except for a specified list of ignored methods.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A list of method signatures to be ignored during the override check is created using `Arrays.asList`.
    - The `MoreAsserts.assertOverridesMethods` method is called with `JsonWriter.class`, `JsonTreeWriter.class`, and the list of ignored methods to verify that all other methods are overridden.
- **Output**:
    - The method does not return any value; it is a test method that asserts conditions.
- **Functions called**:
    - [`com.google.gson.common.MoreAsserts.assertOverridesMethods`](../../common/MoreAsserts.java.driver.md#MoreAssertsassertOverridesMethods)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriterTest`](#JsonTreeWriterTest)  (Base Class)



