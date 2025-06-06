# Purpose
The `MixedStreamTest` Java class is a comprehensive test suite designed to validate the functionality of JSON serialization and deserialization using the Gson library. It focuses on testing the behavior of `JsonReader` and `JsonWriter` in various scenarios, ensuring that JSON data can be accurately read from and written to streams. The class includes tests for writing and reading JSON arrays of [`Car`](#CarCar) objects, verifying that the serialized output matches the expected JSON string. It also tests the handling of different states and configurations of `JsonReader` and `JsonWriter`, such as lenient mode, HTML-safe mode, and closed state, to ensure robustness and correct error handling.

The class defines a nested static [`Car`](#CarCar) class, which serves as the data model for the tests. This class includes fields for the car's name and color, along with appropriate constructors, [`hashCode`](#CarhashCode), and [`equals`](#Carequals) methods to facilitate object comparison. The test methods utilize assertions to verify the correctness of the JSON operations, including checking for exceptions when invalid operations are performed. The suite also explores advanced features of Gson, such as handling special floating-point values and disabling HTML escaping, providing a thorough examination of the library's capabilities in handling JSON data streams.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.io.StringReader`
- `java.io.StringWriter`
- `java.lang.reflect.Type`
- `java.util.Arrays`
- `java.util.List`
- `org.junit.Test`


# Classes

---
### MixedStreamTest<!-- {{#class:com.google.gson.MixedStreamTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `MixedStreamTest` class is a test suite designed to validate the functionality of JSON serialization and deserialization using the Gson library, specifically focusing on mixed streaming of JSON data. It includes a series of JUnit test methods that check the correct behavior of reading and writing JSON data, handling of invalid states, and ensuring that the state of `JsonReader` and `JsonWriter` objects is not improperly mutated during operations. The class also tests the handling of special cases such as null values, closed streams, and HTML-safe writing with and without escaping.
- **Fields**:
    - `BLUE_MUSTANG`: `Car` A static final instance of the Car class representing a blue Mustang.
    - `BLACK_BMW`: `Car` A static final instance of the Car class representing a black BMW.
    - `RED_MIATA`: `Car` A static final instance of the Car class representing a red Miata.
    - `CARS_JSON`: `String` A static final String containing the JSON representation of the car instances.
- **Methods**:
    - [`com.google.gson.MixedStreamTest.testWriteMixedStreamed`](#MixedStreamTesttestWriteMixedStreamed)
    - [`com.google.gson.MixedStreamTest.testReadMixedStreamed`](#MixedStreamTesttestReadMixedStreamed)
    - [`com.google.gson.MixedStreamTest.testReadDoesNotMutateState`](#MixedStreamTesttestReadDoesNotMutateState)
    - [`com.google.gson.MixedStreamTest.testWriteDoesNotMutateState`](#MixedStreamTesttestWriteDoesNotMutateState)
    - [`com.google.gson.MixedStreamTest.testReadInvalidState`](#MixedStreamTesttestReadInvalidState)
    - [`com.google.gson.MixedStreamTest.testReadClosed`](#MixedStreamTesttestReadClosed)
    - [`com.google.gson.MixedStreamTest.testWriteInvalidState`](#MixedStreamTesttestWriteInvalidState)
    - [`com.google.gson.MixedStreamTest.testWriteClosed`](#MixedStreamTesttestWriteClosed)
    - [`com.google.gson.MixedStreamTest.testWriteNulls`](#MixedStreamTesttestWriteNulls)
    - [`com.google.gson.MixedStreamTest.testReadNulls`](#MixedStreamTesttestReadNulls)
    - [`com.google.gson.MixedStreamTest.testWriteHtmlSafeWithEscaping`](#MixedStreamTesttestWriteHtmlSafeWithEscaping)
    - [`com.google.gson.MixedStreamTest.testWriteHtmlSafeWithoutEscaping`](#MixedStreamTesttestWriteHtmlSafeWithoutEscaping)
    - [`com.google.gson.MixedStreamTest.testWriteLenient`](#MixedStreamTesttestWriteLenient)

**Methods**

---
#### MixedStreamTest\.testWriteMixedStreamed<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteMixedStreamed}} -->
The `testWriteMixedStreamed` method tests the serialization of a list of `Car` objects into a JSON array using Gson and verifies the output against a predefined JSON string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `Gson` object for JSON operations.
    - Create a `StringWriter` to capture the JSON output.
    - Create a `JsonWriter` using the `StringWriter` to write JSON data.
    - Begin a JSON array using `jsonWriter.beginArray()`.
    - Set indentation for the JSON output using `jsonWriter.setIndent("  ")`.
    - Serialize three `Car` objects (`BLUE_MUSTANG`, `BLACK_BMW`, `RED_MIATA`) into the JSON array using `gson.toJson()`.
    - End the JSON array using `jsonWriter.endArray()`.
    - Assert that the JSON string written to `StringWriter` matches the expected `CARS_JSON` string using `assertThat`.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correctness of the JSON serialization.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.setIndent`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetIndent)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testReadMixedStreamed<!-- {{#callable:com.google.gson.MixedStreamTest.testReadMixedStreamed}} -->
The `testReadMixedStreamed` method tests the deserialization of a JSON array of car objects using Gson and verifies that the deserialized objects match expected car instances.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `Gson` object for JSON operations.
    - Create a `StringReader` initialized with the `CARS_JSON` string, which contains JSON data representing an array of car objects.
    - Create a `JsonReader` using the `StringReader` to read the JSON data.
    - Call [`beginArray`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginArray) on the `JsonReader` to start reading the JSON array.
    - Deserialize the first car object from the JSON array using `gson.fromJson` and assert that it equals `BLUE_MUSTANG`.
    - Deserialize the second car object from the JSON array using `gson.fromJson` and assert that it equals `BLACK_BMW`.
    - Deserialize the third car object from the JSON array using `gson.fromJson` and assert that it equals `RED_MIATA`.
    - Call [`endArray`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendArray) on the `JsonReader` to finish reading the JSON array.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.beginArray`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.stream.JsonReader.endArray`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendArray)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testReadDoesNotMutateState<!-- {{#callable:com.google.gson.MixedStreamTest.testReadDoesNotMutateState}} -->
The `testReadDoesNotMutateState` method verifies that the lenient state of a `JsonReader` is not altered by the deserialization process using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated for JSON operations.
    - A `JsonReader` is created with a `StringReader` containing the JSON data `CARS_JSON`.
    - The `JsonReader` is set to begin reading an array with `beginArray()`.
    - The lenient mode of `JsonReader` is set to `false` using `setLenient(false)`.
    - A `Car` object is deserialized from the `JsonReader` using `gson.fromJson()`, and it is asserted that the object is not null.
    - It is asserted that the lenient mode of `JsonReader` remains `false` after deserialization.
    - The lenient mode of `JsonReader` is set to `true` using `setLenient(true)`.
    - Another `Car` object is deserialized from the `JsonReader`, and it is asserted that the object is not null.
    - It is asserted that the lenient mode of `JsonReader` remains `true` after deserialization.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.beginArray`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.setLenient`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadersetLenient)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.stream.JsonReader.isLenient`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderisLenient)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testWriteDoesNotMutateState<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteDoesNotMutateState}} -->
The `testWriteDoesNotMutateState` method verifies that the state of a `JsonWriter` object remains unchanged after writing JSON data using the Gson library.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object and a `JsonWriter` object with a `StringWriter` are instantiated.
    - The `JsonWriter` begins an array with `beginArray()`.
    - The `JsonWriter` is set to HTML safe and lenient modes using `setHtmlSafe(true)` and `setLenient(true)`.
    - The `Gson` object serializes a `Car` object (`BLUE_MUSTANG`) to JSON using the `JsonWriter`.
    - Assertions check that the `JsonWriter` remains in HTML safe and lenient modes.
    - The `JsonWriter` is set to non-HTML safe and non-lenient modes using `setHtmlSafe(false)` and `setLenient(false)`.
    - The `Gson` object serializes the same `Car` object to JSON again using the `JsonWriter`.
    - Assertions check that the `JsonWriter` remains in non-HTML safe and non-lenient modes.
- **Output**:
    - The method does not return any value; it uses assertions to verify the state of the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.setHtmlSafe`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.setLenient`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetLenient)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.stream.JsonWriter.isHtmlSafe`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterisHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.isLenient`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterisLenient)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testReadInvalidState<!-- {{#callable:com.google.gson.MixedStreamTest.testReadInvalidState}} -->
The `testReadInvalidState` method tests that a `JsonParseException` is thrown when attempting to deserialize a JSON object into a `String` using a `JsonReader` that is in an invalid state.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - A `JsonReader` is created using a `StringReader` initialized with the `CARS_JSON` string.
    - The `JsonReader` is instructed to begin reading an array with `beginArray()`.
    - The `JsonReader` is then instructed to begin reading an object with `beginObject()`, which is an invalid state for the subsequent operation.
    - The method asserts that a `JsonParseException` is thrown when attempting to deserialize the JSON using `gson.fromJson(jsonReader, String.class)`.
- **Output**:
    - The method does not return any value but verifies that a `JsonParseException` is thrown under the specified conditions.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.beginArray`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginObject)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testReadClosed<!-- {{#callable:com.google.gson.MixedStreamTest.testReadClosed}} -->
The `testReadClosed` method tests that attempting to read from a closed `JsonReader` throws a `JsonParseException` with a specific error message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - A `JsonReader` is created using a `StringReader` initialized with `CARS_JSON`.
    - The `JsonReader` is immediately closed using the `close()` method.
    - The method uses `assertThrows` to verify that calling `gson.fromJson` with the closed `JsonReader` throws a `JsonParseException`.
    - The exception is captured in variable `e`.
    - An assertion checks that the cause of the exception `e` has a message equal to "JsonReader is closed".
- **Output**:
    - The method does not return any value but asserts that a `JsonParseException` is thrown with the message "JsonReader is closed".
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.close`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderclose)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testWriteInvalidState<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteInvalidState}} -->
The `testWriteInvalidState` method tests that writing a JSON object with an invalid state using Gson throws an `IllegalStateException` with a specific message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated to handle JSON operations.
    - A `JsonWriter` is created with a `StringWriter` to capture JSON output.
    - The `JsonWriter` begins writing a JSON object using `beginObject()`.
    - The method attempts to serialize the `BLUE_MUSTANG` object into JSON using the `Gson` instance and the `JsonWriter`.
    - An `IllegalStateException` is expected to be thrown due to the invalid state of the `JsonWriter`.
    - The exception is captured and asserted to have the message 'Nesting problem.'
- **Output**:
    - The method does not return any value but asserts that an `IllegalStateException` is thrown with the message 'Nesting problem.'
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testWriteClosed<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteClosed}} -->
The `testWriteClosed` method tests that attempting to write to a closed `JsonWriter` throws an `IllegalStateException` with a specific message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated.
    - A `JsonWriter` is created with a `StringWriter`.
    - The `JsonWriter` begins and ends an array, then is closed.
    - An attempt is made to serialize a `Car` object to the closed `JsonWriter`, which is expected to throw an `IllegalStateException`.
    - The exception is caught and its message is asserted to be 'JsonWriter is closed.'
- **Output**:
    - The method does not return a value; it asserts that an `IllegalStateException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testWriteNulls<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteNulls}} -->
The `testWriteNulls` method tests the behavior of Gson when writing null values to a JSON writer.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated.
    - The method asserts that a `NullPointerException` is thrown when attempting to serialize a `JsonPrimitive` with a null `JsonWriter`.
    - A `StringWriter` is created and used to instantiate a `JsonWriter`.
    - The method serializes a null value using the `Gson` object and the `JsonWriter`.
    - The method asserts that the output of the `StringWriter` is the string "null".
- **Output**:
    - The method does not return any value; it performs assertions to validate behavior.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testReadNulls<!-- {{#callable:com.google.gson.MixedStreamTest.testReadNulls}} -->
The `testReadNulls` method tests the Gson library's behavior when attempting to deserialize JSON from null inputs, ensuring that a NullPointerException is thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a new Gson object.
    - Use `assertThrows` to verify that calling `gson.fromJson` with a null `JsonReader` and a valid class type throws a `NullPointerException`.
    - Use `assertThrows` to verify that calling `gson.fromJson` with a valid `JsonReader` and a null type throws a `NullPointerException`.
- **Output**:
    - The method does not return any value; it asserts that exceptions are thrown under specific conditions.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testWriteHtmlSafeWithEscaping<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteHtmlSafeWithEscaping}} -->
The `testWriteHtmlSafeWithEscaping` method tests the JSON serialization of a list of special HTML characters with HTML escaping enabled using Gson.
- **Modifiers**: `@Test`, `public`
- **Inputs**: None
- **Control Flow**:
    - Create a list `contents` containing special HTML characters: '<', '>', '&', '=', and '''.
    - Define a `Type` object `type` representing a list of strings using `TypeToken`.
    - Instantiate a `StringWriter` object `writer` to capture the JSON output.
    - Use `Gson` to serialize the `contents` list into JSON format with HTML escaping, writing the result to `writer`.
    - Assert that the serialized JSON string in `writer` matches the expected escaped output: `["\u003c","\u003e","\u0026","\u003d","\u0027"]`.
- **Output**:
    - The method does not return a value but asserts that the JSON output matches the expected escaped string.
- **Functions called**:
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testWriteHtmlSafeWithoutEscaping<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteHtmlSafeWithoutEscaping}} -->
The method `testWriteHtmlSafeWithoutEscaping` tests the serialization of a list of special HTML characters into JSON without escaping them.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A list of strings containing special HTML characters ('<', '>', '&', '=', and "'") is created.
    - The type of the list is determined using `TypeToken`.
    - A `StringWriter` is instantiated to capture the JSON output.
    - A `Gson` object is created with HTML escaping disabled using `GsonBuilder().disableHtmlEscaping().create()`.
    - The list of strings is serialized into JSON using the [`toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method, writing the output to the `StringWriter`.
    - An assertion checks that the JSON output matches the expected string representation of the list without HTML escaping.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON output.
- **Functions called**:
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.GsonBuilder.disableHtmlEscaping`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderdisableHtmlEscaping)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)


---
#### MixedStreamTest\.testWriteLenient<!-- {{#callable:com.google.gson.MixedStreamTest.testWriteLenient}} -->
The `testWriteLenient` method tests the serialization of a list of special floating-point values using Gson with and without lenient settings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A list of `Double` values, including special floating-point values like `NaN`, `NEGATIVE_INFINITY`, and `POSITIVE_INFINITY`, is created.
    - A `Type` object representing a list of `Double` is obtained using `TypeToken`.
    - A `StringWriter` and a `JsonWriter` are instantiated to capture the JSON output.
    - A `GsonBuilder` is configured to serialize special floating-point values and used to serialize the list of `Double` values into JSON using the `JsonWriter`.
    - An assertion checks that the JSON output matches the expected string representation of the list with special floating-point values.
    - An `IllegalArgumentException` is expected to be thrown when attempting to serialize the list using a default `Gson` instance without lenient settings, and the exception message is verified.
- **Output**:
    - The method does not return a value; it performs assertions to verify the correct behavior of JSON serialization with special floating-point values.
- **Functions called**:
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.GsonBuilder.serializeSpecialFloatingPointValues`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderserializeSpecialFloatingPointValues)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.MixedStreamTest`](#MixedStreamTest)  (Base Class)



---
### Car<!-- {{#class:com.google.gson.MixedStreamTest.Car}} -->
- **Modifiers**: `static`, `final`
- **Description**: The `Car` class is a simple data structure representing a car with a name and a color, designed to be used with the Gson library for JSON serialization and deserialization. It includes a constructor for initializing the car's name and color, a default constructor for Gson compatibility, and overrides for `hashCode` and `equals` methods to ensure proper comparison and hashing based on the car's attributes.
- **Fields**:
    - `name`: `String` A string representing the name of the car.
    - `color`: `int` An integer representing the color of the car, likely in a hexadecimal format.
- **Methods**:
    - [`com.google.gson.MixedStreamTest.Car.Car`](#CarCar)
    - [`com.google.gson.MixedStreamTest.Car.Car`](#CarCar)
    - [`com.google.gson.MixedStreamTest.Car.hashCode`](#CarhashCode)
    - [`com.google.gson.MixedStreamTest.Car.equals`](#Carequals)

**Methods**

---
#### Car\.Car<!-- {{#callable:com.google.gson.MixedStreamTest.Car.Car}} -->
The `Car` constructor initializes a new `Car` object with a specified name and color.
- **Inputs**:
    - `name`: A `String` representing the name of the car.
    - `color`: An `int` representing the color of the car, typically in RGB format.
- **Control Flow**:
    - The constructor assigns the provided `name` to the `name` field of the `Car` object.
    - The constructor assigns the provided `color` to the `color` field of the `Car` object.
- **Output**:
    - This constructor does not return any value as it is used to instantiate a `Car` object.
- **See also**: [`com.google.gson.MixedStreamTest.Car`](#MixedStreamTest.Car)  (Base Class)


---
#### Car\.Car<!-- {{#callable:com.google.gson.MixedStreamTest.Car.Car}} -->
The `Car` constructor initializes a `Car` object with default values.
- **Inputs**: None
- **Control Flow**:
    - The constructor is empty, indicating it does not perform any operations or initialize any fields explicitly.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.MixedStreamTest.Car`](#MixedStreamTest.Car)  (Base Class)


---
#### Car\.hashCode<!-- {{#callable:com.google.gson.MixedStreamTest.Car.hashCode}} -->
The [`hashCode`](GsonTest.java.driver.md#DummyFactoryhashCode) method computes a hash code for a `Car` object by combining the hash code of its `name` field with its `color` field using a bitwise XOR operation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method retrieves the hash code of the `name` field, which is a `String`.
    - It performs a bitwise XOR operation between the hash code of the `name` and the `color` field, which is an `int`.
    - The result of the XOR operation is returned as the hash code of the `Car` object.
- **Output**:
    - An integer representing the hash code of the `Car` object.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.hashCode`](GsonTest.java.driver.md#DummyFactoryhashCode)
- **See also**: [`com.google.gson.MixedStreamTest.Car`](#MixedStreamTest.Car)  (Base Class)


---
#### Car\.equals<!-- {{#callable:com.google.gson.MixedStreamTest.Car.equals}} -->
The [`equals`](GsonTest.java.driver.md#DummyFactoryequals) method checks if a given object is a `Car` and has the same `name` and `color` as the current `Car` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: An object to be compared with the current `Car` instance for equality.
- **Control Flow**:
    - Check if the input object `o` is an instance of `Car`.
    - If `o` is a `Car`, cast it to a `Car` object and compare its `name` field with the current instance's `name` field using the [`equals`](GsonTest.java.driver.md#DummyFactoryequals) method.
    - Also, compare the `color` field of the casted `Car` object with the current instance's `color` field using the `==` operator.
    - Return `true` if both the `name` and `color` fields match; otherwise, return `false`.
- **Output**:
    - A boolean value indicating whether the input object is equal to the current `Car` instance.
- **Functions called**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.MixedStreamTest.Car`](#MixedStreamTest.Car)  (Base Class)



