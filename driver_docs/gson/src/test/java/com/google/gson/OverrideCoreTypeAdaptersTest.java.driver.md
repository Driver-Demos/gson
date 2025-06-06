# Purpose
The `OverrideCoreTypeAdaptersTest` Java file is a unit test class designed to verify the functionality of custom type adapters in the Gson library, which is a popular Java library for converting Java objects to JSON and vice versa. This file specifically tests the ability to override the default serialization and deserialization behavior for core data types, such as `Boolean` and `String`. The class defines two custom `TypeAdapter` implementations: `booleanAsIntAdapter`, which serializes a `Boolean` as an integer (1 for true, 0 for false), and `swapCaseStringAdapter`, which serializes a `String` in uppercase and deserializes it in lowercase. These adapters are registered with a `GsonBuilder` to create a `Gson` instance that uses the custom serialization logic.

The test methods within the class, annotated with `@Test`, validate the behavior of these custom adapters by asserting the expected JSON output and the deserialized Java objects. For instance, the [`testOverrideWrapperBooleanAdapter`](#OverrideCoreTypeAdaptersTesttestOverrideWrapperBooleanAdapter) and [`testOverridePrimitiveBooleanAdapter`](#OverrideCoreTypeAdaptersTesttestOverridePrimitiveBooleanAdapter) methods ensure that the `Boolean` values are correctly serialized and deserialized according to the custom logic defined in `booleanAsIntAdapter`. Similarly, the [`testOverrideStringAdapter`](#OverrideCoreTypeAdaptersTesttestOverrideStringAdapter) method checks the functionality of `swapCaseStringAdapter`. This file provides a focused functionality by testing the customization of core type serialization in Gson, ensuring that developers can extend and modify the default behavior to suit specific application needs.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.util.Locale`
- `org.junit.Test`


# Classes

---
### OverrideCoreTypeAdaptersTest<!-- {{#class:com.google.gson.OverrideCoreTypeAdaptersTest}} -->
- **Modifiers**: `public`
- **Description**: The `OverrideCoreTypeAdaptersTest` class is a test suite designed to verify the functionality of custom type adapters in the Gson library, specifically for Boolean and String types. It includes two static final `TypeAdapter` instances: `booleanAsIntAdapter` and `swapCaseStringAdapter`, which override the default serialization and deserialization behavior for Boolean and String types, respectively. The class contains three test methods that use the JUnit framework to assert the correct behavior of these custom adapters when registered with a `Gson` instance, ensuring that Booleans can be serialized as integers and Strings can be serialized with swapped case.
- **Fields**:
    - `booleanAsIntAdapter`: `TypeAdapter<Boolean>` A static final TypeAdapter for Boolean that serializes Booleans as integers (1 or 0).
    - `swapCaseStringAdapter`: `TypeAdapter<String>` A static final TypeAdapter for String that serializes Strings with uppercase and deserializes them with lowercase.
- **Methods**:
    - [`com.google.gson.OverrideCoreTypeAdaptersTest.write`](#OverrideCoreTypeAdaptersTestwrite)
    - [`com.google.gson.OverrideCoreTypeAdaptersTest.read`](#OverrideCoreTypeAdaptersTestread)
    - [`com.google.gson.OverrideCoreTypeAdaptersTest.write`](#OverrideCoreTypeAdaptersTestwrite)
    - [`com.google.gson.OverrideCoreTypeAdaptersTest.read`](#OverrideCoreTypeAdaptersTestread)
    - [`com.google.gson.OverrideCoreTypeAdaptersTest.testOverrideWrapperBooleanAdapter`](#OverrideCoreTypeAdaptersTesttestOverrideWrapperBooleanAdapter)
    - [`com.google.gson.OverrideCoreTypeAdaptersTest.testOverridePrimitiveBooleanAdapter`](#OverrideCoreTypeAdaptersTesttestOverridePrimitiveBooleanAdapter)
    - [`com.google.gson.OverrideCoreTypeAdaptersTest.testOverrideStringAdapter`](#OverrideCoreTypeAdaptersTesttestOverrideStringAdapter)

**Methods**

---
#### OverrideCoreTypeAdaptersTest\.write<!-- {{#callable:com.google.gson.OverrideCoreTypeAdaptersTest.write}} -->
The `write` method writes a boolean value as an integer (1 for true, 0 for false) to a JSON writer.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `Boolean` object representing the value to be written as an integer.
- **Control Flow**:
    - The method checks if the [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) is true.
    - If [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) is true, it writes the integer 1 to the `JsonWriter`.
    - If [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) is false, it writes the integer 0 to the `JsonWriter`.
- **Output**:
    - The method does not return any value; it writes an integer representation of a boolean to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.OverrideCoreTypeAdaptersTest`](#OverrideCoreTypeAdaptersTest)  (Base Class)


---
#### OverrideCoreTypeAdaptersTest\.read<!-- {{#callable:com.google.gson.OverrideCoreTypeAdaptersTest.read}} -->
The `read` method reads an integer from a `JsonReader` and returns `true` if the integer is non-zero, otherwise `false`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which an integer is read.
- **Control Flow**:
    - Call `nextInt()` on the `JsonReader` object `in` to read the next integer value.
    - Check if the read integer value is not equal to zero.
    - Return `true` if the integer is non-zero, otherwise return `false`.
- **Output**:
    - A `Boolean` value that is `true` if the read integer is non-zero, otherwise `false`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextInt`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.OverrideCoreTypeAdaptersTest`](#OverrideCoreTypeAdaptersTest)  (Base Class)


---
#### OverrideCoreTypeAdaptersTest\.write<!-- {{#callable:com.google.gson.OverrideCoreTypeAdaptersTest.write}} -->
The `write` method writes a string value to a `JsonWriter` in uppercase using the US locale.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `out`: A `JsonWriter` object to which the string value will be written.
    - [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `String` value that will be converted to uppercase and written to the `JsonWriter`.
- **Control Flow**:
    - The method takes a `JsonWriter` and a `String` as parameters.
    - It converts the input string [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) to uppercase using the US locale.
    - The uppercase string is then written to the `JsonWriter` using the [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method of `JsonWriter`.
- **Output**:
    - The method does not return any value; it writes the uppercase string to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.OverrideCoreTypeAdaptersTest`](#OverrideCoreTypeAdaptersTest)  (Base Class)


---
#### OverrideCoreTypeAdaptersTest\.read<!-- {{#callable:com.google.gson.OverrideCoreTypeAdaptersTest.read}} -->
The `read` method reads a string from a `JsonReader` and converts it to lowercase using the US locale.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which the method reads the next string.
- **Control Flow**:
    - Call `in.nextString()` to read the next string from the `JsonReader`.
    - Convert the string to lowercase using `Locale.US`.
- **Output**:
    - Returns the lowercase version of the string read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.OverrideCoreTypeAdaptersTest`](#OverrideCoreTypeAdaptersTest)  (Base Class)


---
#### OverrideCoreTypeAdaptersTest\.testOverrideWrapperBooleanAdapter<!-- {{#callable:com.google.gson.OverrideCoreTypeAdaptersTest.testOverrideWrapperBooleanAdapter}} -->
The method tests the behavior of a custom Gson TypeAdapter for the Boolean wrapper class that serializes Booleans as integers.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created with a custom TypeAdapter for the Boolean class that serializes Booleans as integers.
    - The method asserts that serializing a primitive boolean true results in the string "true".
    - The method asserts that serializing a Boolean object true results in the string "1".
    - The method asserts that deserializing the string "true" to a primitive boolean results in Boolean.TRUE.
    - The method asserts that deserializing the string "1" to a Boolean object results in Boolean.TRUE.
    - The method asserts that deserializing the string "0" to a Boolean object results in Boolean.FALSE.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the custom TypeAdapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.OverrideCoreTypeAdaptersTest`](#OverrideCoreTypeAdaptersTest)  (Base Class)


---
#### OverrideCoreTypeAdaptersTest\.testOverridePrimitiveBooleanAdapter<!-- {{#callable:com.google.gson.OverrideCoreTypeAdaptersTest.testOverridePrimitiveBooleanAdapter}} -->
The method tests the custom serialization and deserialization of primitive boolean values using a type adapter in Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson instance is created with a custom type adapter for primitive boolean values, which serializes booleans as integers (1 for true, 0 for false).
    - The method asserts that serializing 'true' as a primitive boolean results in '1'.
    - It asserts that serializing 'true' as a Boolean object results in 'true'.
    - It asserts that deserializing '1' as a primitive boolean results in Boolean.TRUE.
    - It asserts that deserializing 'true' as a Boolean object results in Boolean.TRUE.
    - It asserts that serializing 'false' as a primitive boolean results in '0'.
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of the custom type adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.OverrideCoreTypeAdaptersTest`](#OverrideCoreTypeAdaptersTest)  (Base Class)


---
#### OverrideCoreTypeAdaptersTest\.testOverrideStringAdapter<!-- {{#callable:com.google.gson.OverrideCoreTypeAdaptersTest.testOverrideStringAdapter}} -->
The `testOverrideStringAdapter` method tests the custom serialization and deserialization of strings using a type adapter that swaps the case of the string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created with a custom `TypeAdapter` for `String` that swaps the case of the string.
    - The method asserts that serializing the string "Hello" results in the JSON string "HELLO".
    - The method asserts that deserializing the JSON string "Hello" results in the string "hello".
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the custom string adapter.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.OverrideCoreTypeAdaptersTest`](#OverrideCoreTypeAdaptersTest)  (Base Class)



