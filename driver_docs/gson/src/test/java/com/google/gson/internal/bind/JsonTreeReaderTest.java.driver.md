# Purpose
The `JsonTreeReaderTest` class is a unit test suite designed to validate the functionality of the `JsonTreeReader` class, which is part of the internal binding package of the Google Gson library. This test class focuses on ensuring that the `JsonTreeReader` correctly handles various JSON structures and operations, such as skipping values, handling end-of-document scenarios, and dealing with custom JSON element subclasses. The tests cover a range of scenarios, including reading from empty and filled JSON objects, managing JSON arrays, and verifying the behavior when encountering custom subclasses of `JsonElement`. The tests also ensure that the `JsonTreeReader` correctly overrides methods from its superclass, `JsonReader`, to read from a `JsonElement` instead of a `Reader`.

The test suite includes specific tests for the `skipValue` method, which is crucial for navigating JSON structures without processing every element. It also checks the behavior of the `JsonTreeReader` when it reaches the end of a document or an array, ensuring that it correctly identifies these states. Additionally, the suite tests the handling of a custom subclass of `JsonElement`, ensuring that unsupported subclasses trigger appropriate exceptions. The class also includes a test to verify that the `JsonTreeReader` ignores the nesting limit, which is a design choice due to its internal nature and the potential for being created implicitly. Overall, this test suite provides comprehensive coverage of the `JsonTreeReader`'s functionality, ensuring its reliability and correctness within the Gson library.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.JsonArray`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonNull`
- `com.google.gson.JsonObject`
- `com.google.gson.common.MoreAsserts`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.IOException`
- `java.io.Reader`
- `java.util.Arrays`
- `java.util.List`
- `org.junit.Test`


# Classes

---
### JsonTreeReaderTest<!-- {{#class:com.google.gson.internal.bind.JsonTreeReaderTest}} -->
- **Modifiers**: `public`
- **Description**: The `JsonTreeReaderTest` class is a test suite for the `JsonTreeReader` class, which is part of the Gson library used for reading JSON data. This class contains various test methods that validate the behavior of `JsonTreeReader` when handling different JSON structures, such as empty and filled JSON objects, arrays, and custom JSON element subclasses. It also tests the handling of JSON reading operations like skipping values, checking for the end of documents, and ensuring that the nesting limit is ignored. The tests ensure that `JsonTreeReader` correctly overrides methods from `JsonReader` and handles JSON parsing as expected, including throwing exceptions for unsupported operations.
- **Methods**:
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_emptyJsonObject`](#JsonTreeReaderTesttestSkipValue_emptyJsonObject)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_filledJsonObject`](#JsonTreeReaderTesttestSkipValue_filledJsonObject)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_name`](#JsonTreeReaderTesttestSkipValue_name)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_afterEndOfDocument`](#JsonTreeReaderTesttestSkipValue_afterEndOfDocument)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_atArrayEnd`](#JsonTreeReaderTesttestSkipValue_atArrayEnd)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_atObjectEnd`](#JsonTreeReaderTesttestSkipValue_atObjectEnd)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testHasNext_endOfDocument`](#JsonTreeReaderTesttestHasNext_endOfDocument)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testCustomJsonElementSubclass`](#JsonTreeReaderTesttestCustomJsonElementSubclass)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testNestingLimitIgnored`](#JsonTreeReaderTesttestNestingLimitIgnored)
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testOverrides`](#JsonTreeReaderTesttestOverrides)

**Methods**

---
#### JsonTreeReaderTest\.testSkipValue\_emptyJsonObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_emptyJsonObject}} -->
The method tests the behavior of the JsonTreeReader's skipValue method when initialized with an empty JsonObject.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new JsonTreeReader instance is created with an empty JsonObject as input.
    - The skipValue method is called on the JsonTreeReader instance, which should skip the current value.
    - An assertion checks that the next token in the reader is JsonToken.END_DOCUMENT, indicating the end of the JSON document.
    - Another assertion checks that the path in the reader is "$", indicating the root of the JSON structure.
- **Output**:
    - The method does not return any value but asserts the expected state of the JsonTreeReader after skipping a value in an empty JsonObject.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testSkipValue\_filledJsonObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_filledJsonObject}} -->
The method `testSkipValue_filledJsonObject` tests the behavior of the `JsonTreeReader` when skipping a value in a filled JSON object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonObject` is created and populated with various properties, including a `JsonArray`, boolean, integer, `JsonNull`, another `JsonObject`, and a string.
    - A `JsonTreeReader` is instantiated with the populated `JsonObject`.
    - The [`skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue) method is called on the `JsonTreeReader`, which skips the current value in the JSON structure.
    - Assertions are made to verify that after skipping, the `JsonTreeReader` is at the end of the document and the path is at the root ('$').
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the `JsonTreeReader` is at the end of the document and the path is '$' after skipping the value.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testSkipValue\_name<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_name}} -->
The `testSkipValue_name` method tests the behavior of the `JsonTreeReader` when skipping a value in a JSON object and verifies the subsequent state of the reader.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonObject` is created and a property 'a' with value 'value' is added to it.
    - A `JsonTreeReader` is initialized with the created `JsonObject`.
    - The `beginObject()` method is called on the reader to start reading the JSON object.
    - The `skipValue()` method is called to skip the current value in the JSON object.
    - An assertion checks that the next token is a `JsonToken.STRING`.
    - An assertion checks that the path of the reader is `$.<skipped>`.
    - An assertion checks that the next string value read by the reader is 'value'.
- **Output**:
    - The method does not return any value but performs assertions to verify the behavior of the `JsonTreeReader` after skipping a value.
- **Functions called**:
    - [`com.google.gson.JsonObject.addProperty`](../../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testSkipValue\_afterEndOfDocument<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_afterEndOfDocument}} -->
The method `testSkipValue_afterEndOfDocument` tests the behavior of the `JsonTreeReader` when attempting to skip a value after reaching the end of a JSON document.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeReader` is initialized with an empty `JsonObject`.
    - The method begins reading the object with `reader.beginObject()` and immediately ends it with `reader.endObject()`.
    - An assertion checks that the reader's current token is `JsonToken.END_DOCUMENT`, indicating the end of the document.
    - The reader's path is asserted to be `"$"`, representing the root of the JSON structure.
    - The method calls `reader.skipValue()`, which should have no effect since the document has ended.
    - Another assertion checks that the reader's current token remains `JsonToken.END_DOCUMENT`.
    - The reader's path is again asserted to be `"$"`.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of the `JsonTreeReader`.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testSkipValue\_atArrayEnd<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_atArrayEnd}} -->
The `testSkipValue_atArrayEnd` method tests the behavior of the `JsonTreeReader` when skipping a value at the end of a JSON array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeReader` is instantiated with an empty `JsonArray`.
    - The `beginArray()` method is called on the reader to start reading the array.
    - The `skipValue()` method is called to skip the current value in the array.
    - An assertion checks that the `peek()` method returns `JsonToken.END_DOCUMENT`, indicating the end of the document.
    - Another assertion checks that the `getPath()` method returns the string `"$"`, indicating the root path.
- **Output**:
    - The method does not return any value but asserts that the `JsonTreeReader` correctly identifies the end of the document and the root path after skipping a value at the end of an array.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testSkipValue\_atObjectEnd<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testSkipValue_atObjectEnd}} -->
The method `testSkipValue_atObjectEnd` tests the behavior of the `JsonTreeReader` when skipping a value at the end of a JSON object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeReader` is initialized with an empty `JsonObject`.
    - The [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) method is called on the reader to start reading the object.
    - The [`skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue) method is called to skip the current value in the JSON object.
    - An assertion checks that the [`peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek) method returns `JsonToken.END_DOCUMENT`, indicating the end of the JSON document.
    - Another assertion checks that the [`getPath`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath) method returns `$`, indicating the root path of the JSON structure.
- **Output**:
    - The method does not return any value but asserts the state of the `JsonTreeReader` after skipping a value at the end of a JSON object.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testHasNext\_endOfDocument<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testHasNext_endOfDocument}} -->
The method `testHasNext_endOfDocument` tests whether the [`hasNext`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderhasNext) method of `JsonTreeReader` returns `false` after reading an empty JSON object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonTreeReader` is instantiated with an empty `JsonObject`.
    - The [`beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject) method is called on the reader to start reading the JSON object.
    - The [`endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject) method is called to signify the end of the JSON object.
    - The [`hasNext`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderhasNext) method is called on the reader, and it is asserted that the result is `false`.
- **Output**:
    - The method does not return any value as it is a test method; it asserts that [`hasNext`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderhasNext) returns `false` after reading an empty JSON object.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.hasNext`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderhasNext)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testCustomJsonElementSubclass<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testCustomJsonElementSubclass}} -->
The `testCustomJsonElementSubclass` method tests that a `JsonTreeReader` throws a `MalformedJsonException` when encountering a custom subclass of `JsonElement`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A custom subclass `CustomSubclass` of `JsonElement` is defined with an overridden `deepCopy` method that returns `this`.
    - A `JsonArray` is created and an instance of `CustomSubclass` is added to it.
    - A `JsonTreeReader` is initialized with the `JsonArray`.
    - The [`beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray) method is called on the `JsonTreeReader` to start reading the array.
    - The `assertThrows` method is used to verify that calling [`peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek) on the `JsonTreeReader` throws a `MalformedJsonException`.
    - The exception message is asserted to be equal to a specific message indicating that the custom subclass is not supported.
- **Output**:
    - The method does not return a value; it asserts that a `MalformedJsonException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testNestingLimitIgnored<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testNestingLimitIgnored}} -->
The `testNestingLimitIgnored` method tests that the `JsonTreeReader` ignores the nesting limit when reading deeply nested JSON arrays.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize an integer `limit` to 10 and create a `JsonArray` named `json`.
    - Create a reference `current` pointing to `json`.
    - Iterate `limit` times to add nested `JsonArray` objects within `json`, resulting in `limit + 1` nested arrays.
    - Instantiate a `JsonTreeReader` with `json` and set its nesting limit to `limit`.
    - Assert that the reader's nesting limit is equal to `limit`.
    - Iterate `limit` times, calling `beginArray()` on the reader to traverse into each nested array.
    - Call `beginArray()` once more to test that no exception is thrown despite exceeding the limit.
    - Call `endArray()` once to begin unwinding the nested arrays.
    - Iterate `limit` times, calling `endArray()` to fully unwind all nested arrays.
    - Assert that the reader's next token is `JsonToken.END_DOCUMENT`, indicating the end of the JSON structure.
    - Close the reader.
- **Output**:
    - The method does not return any value but asserts that the `JsonTreeReader` can handle deeply nested arrays without throwing an exception due to nesting limit.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.stream.JsonReader.setNestingLimit`](../../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetNestingLimit)
    - [`com.google.gson.stream.JsonReader.getNestingLimit`](../../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetNestingLimit)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.close`](../../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderclose)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)


---
#### JsonTreeReaderTest\.testOverrides<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testOverrides}} -->
The `testOverrides` method verifies that the `JsonTreeReader` class correctly overrides all necessary methods from the `JsonReader` class, except for a specified list of ignored methods.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A list of method names to be ignored during the override check is created using `Arrays.asList`.
    - The `MoreAsserts.assertOverridesMethods` method is called with `JsonReader.class`, `JsonTreeReader.class`, and the list of ignored methods to verify that all other methods are overridden.
- **Output**:
    - The method does not return any value; it is a test method that asserts conditions.
- **Functions called**:
    - [`com.google.gson.JsonArray.asList`](../../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.common.MoreAsserts.assertOverridesMethods`](../../common/MoreAsserts.java.driver.md#MoreAssertsassertOverridesMethods)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest`](#JsonTreeReaderTest)  (Base Class)



---
### CustomSubclass<!-- {{#class:com.google.gson.internal.bind.JsonTreeReaderTest.testCustomJsonElementSubclass.CustomSubclass}} -->
- **Description**: The `CustomSubclass` is a specialized subclass of `JsonElement` that overrides the `deepCopy` method to return itself, effectively making it immutable in terms of deep copying. This class is used in testing scenarios to demonstrate the behavior of `JsonTreeReader` when encountering custom subclasses of `JsonElement`, which are not supported and result in a `MalformedJsonException`.
- **Methods**:
    - [`com.google.gson.internal.bind.JsonTreeReaderTest.testCustomJsonElementSubclass.CustomSubclass.deepCopy`](#JsonTreeReaderTesttestCustomJsonElementSubclass.CustomSubclass.deepCopy)
- **Extends/Implements**:
    - [`com.google.gson.JsonElement`](../../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElement)

**Methods**

---
#### CustomSubclass\.deepCopy<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReaderTest.testCustomJsonElementSubclass.CustomSubclass.deepCopy}} -->
The `deepCopy` method returns the current instance of the `JsonElement` subclass without creating a new copy.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is overridden from a superclass, indicating it is intended to provide a specific implementation for a subclass of `JsonElement`.
    - The method simply returns `this`, which is the current instance of the class, without performing any additional operations or creating a new object.
- **Output**:
    - The method returns the current instance of the `JsonElement` subclass (`this`).
- **See also**: [`com.google.gson.internal.bind.JsonTreeReaderTest.testCustomJsonElementSubclass.CustomSubclass`](#JsonTreeReaderTest.testCustomJsonElementSubclass.CustomSubclass)  (Base Class)



