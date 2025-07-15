# Purpose
The provided Java source code file is a comprehensive suite of unit tests for the `GsonBuilder` class, which is part of the Google Gson library. This library is widely used for converting Java objects to JSON and vice versa. The tests in this file are designed to verify the functionality and robustness of the `GsonBuilder` class, ensuring that it behaves correctly under various conditions and configurations. The tests cover a wide range of scenarios, including the creation of `Gson` instances, the impact of modifying a `GsonBuilder` after creating a `Gson` instance, the registration of custom type adapters, and the handling of field modifiers and date formats.

The file includes tests that validate the exclusion of fields with specific modifiers, the registration of type adapters for core types, and the behavior of the `GsonBuilder` when setting date formats with valid and invalid patterns. It also tests the strictness settings of JSON readers and writers, ensuring that the `GsonBuilder` can be configured to handle JSON parsing and writing in different modes. Additionally, the file contains tests for error handling, such as attempting to register type adapters for built-in types and handling invalid version numbers. Overall, this file serves as a critical component in maintaining the reliability and correctness of the Gson library by ensuring that the `GsonBuilder` class functions as expected across a variety of use cases.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.io.StringReader`
- `java.io.StringWriter`
- `java.lang.reflect.Modifier`
- `java.lang.reflect.Type`
- `java.text.DateFormat`
- `java.util.Date`
- `org.junit.Ignore`
- `org.junit.Test`


# Classes

---
### GsonBuilderTest<!-- {{#class:com.google.gson.GsonBuilderTest}} -->
- **Modifiers**: `public`
- **Description**: The `GsonBuilderTest` class is a comprehensive suite of unit tests for the `GsonBuilder` class from the Gson library, which is used for building `Gson` instances with custom configurations. It tests various functionalities such as creating multiple `Gson` instances, modifying `GsonBuilder` after creation, excluding fields with specific modifiers, handling transient fields, registering type adapters, setting date formats, and managing strictness levels. The tests ensure that `GsonBuilder` behaves correctly under different scenarios, including invalid configurations and custom type handling.
- **Fields**:
    - `NULL_TYPE_ADAPTER`: `TypeAdapter<Object>` A static final `TypeAdapter` instance that throws an `AssertionError` for both read and write operations.
- **Methods**:
    - [`com.google.gson.GsonBuilderTest.write`](#GsonBuilderTestwrite)
    - [`com.google.gson.GsonBuilderTest.read`](#GsonBuilderTestread)
    - [`com.google.gson.GsonBuilderTest.testCreatingMoreThanOnce`](#GsonBuilderTesttestCreatingMoreThanOnce)
    - [`com.google.gson.GsonBuilderTest.testModificationAfterCreate`](#GsonBuilderTesttestModificationAfterCreate)
    - [`com.google.gson.GsonBuilderTest.assertDefaultGson`](#GsonBuilderTestassertDefaultGson)
    - [`com.google.gson.GsonBuilderTest.assertCustomGson`](#GsonBuilderTestassertCustomGson)
    - [`com.google.gson.GsonBuilderTest.testExcludeFieldsWithModifiers`](#GsonBuilderTesttestExcludeFieldsWithModifiers)
    - [`com.google.gson.GsonBuilderTest.testTransientFieldExclusion`](#GsonBuilderTesttestTransientFieldExclusion)
    - [`com.google.gson.GsonBuilderTest.testRegisterTypeAdapterForCoreType`](#GsonBuilderTesttestRegisterTypeAdapterForCoreType)
    - [`com.google.gson.GsonBuilderTest.testDisableJdkUnsafe`](#GsonBuilderTesttestDisableJdkUnsafe)
    - [`com.google.gson.GsonBuilderTest.testSetVersionInvalid`](#GsonBuilderTesttestSetVersionInvalid)
    - [`com.google.gson.GsonBuilderTest.testDefaultStrictness`](#GsonBuilderTesttestDefaultStrictness)
    - [`com.google.gson.GsonBuilderTest.testSetLenient`](#GsonBuilderTesttestSetLenient)
    - [`com.google.gson.GsonBuilderTest.testSetStrictness`](#GsonBuilderTesttestSetStrictness)
    - [`com.google.gson.GsonBuilderTest.testRegisterTypeAdapterForObjectAndJsonElements`](#GsonBuilderTesttestRegisterTypeAdapterForObjectAndJsonElements)
    - [`com.google.gson.GsonBuilderTest.testRegisterTypeAdapterForJsonElements`](#GsonBuilderTesttestRegisterTypeAdapterForJsonElements)
    - [`com.google.gson.GsonBuilderTest.testRegisterTypeHierarchyAdapterJsonElements`](#GsonBuilderTesttestRegisterTypeHierarchyAdapterJsonElements)
    - [`com.google.gson.GsonBuilderTest.testRegisterTypeHierarchyAdapterJsonElements_Allowed`](#GsonBuilderTesttestRegisterTypeHierarchyAdapterJsonElements_Allowed)
    - [`com.google.gson.GsonBuilderTest.testSetDateFormatWithInvalidPattern`](#GsonBuilderTesttestSetDateFormatWithInvalidPattern)
    - [`com.google.gson.GsonBuilderTest.testSetDateFormatWithValidPattern`](#GsonBuilderTesttestSetDateFormatWithValidPattern)
    - [`com.google.gson.GsonBuilderTest.testSetDateFormatNullPattern`](#GsonBuilderTesttestSetDateFormatNullPattern)
    - [`com.google.gson.GsonBuilderTest.testSetDateFormatEmptyPattern`](#GsonBuilderTesttestSetDateFormatEmptyPattern)
    - [`com.google.gson.GsonBuilderTest.testSetDateFormatValidStyle`](#GsonBuilderTesttestSetDateFormatValidStyle)
    - [`com.google.gson.GsonBuilderTest.testSetDateFormatInvalidStyle`](#GsonBuilderTesttestSetDateFormatInvalidStyle)

**Methods**

---
#### GsonBuilderTest\.write<!-- {{#callable:com.google.gson.GsonBuilderTest.write}} -->
The `write` method in the `TypeAdapter` class throws an `AssertionError` when invoked.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used for writing JSON data.
    - `value`: An `Object` representing the value to be written to the JSON output.
- **Control Flow**:
    - The method immediately throws an `AssertionError`, indicating that it is not intended to be used or that its implementation is incomplete.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.read<!-- {{#callable:com.google.gson.GsonBuilderTest.read}} -->
The `read` method in the `TypeAdapter` class throws an `AssertionError` when invoked.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object that is intended to be used for reading JSON input.
- **Control Flow**:
    - The method immediately throws an `AssertionError`, indicating that it is not intended to be used or that its implementation is incomplete.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testCreatingMoreThanOnce<!-- {{#callable:com.google.gson.GsonBuilderTest.testCreatingMoreThanOnce}} -->
The `testCreatingMoreThanOnce` method tests the behavior of creating multiple `Gson` instances from a `GsonBuilder` and verifies that modifications to the builder result in different `Gson` instances.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `GsonBuilder` object named `builder`.
    - Create a `Gson` instance named `gson` using `builder.create()` and assert that it is not null.
    - Create another `Gson` instance using `builder.create()` and assert that it is not null.
    - Modify the `builder` by setting a field naming strategy using `builder.setFieldNamingStrategy(f -> "test")`.
    - Create another `Gson` instance named `otherGson` using the modified `builder.create()` and assert that it is not null.
    - Assert that the original `gson` instance is not the same instance as `otherGson`, indicating that the modification to the builder resulted in a different `Gson` instance.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of `Gson` instances created from a `GsonBuilder`.
- **Functions called**:
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.GsonBuilder.setFieldNamingStrategy`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetFieldNamingStrategy)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testModificationAfterCreate<!-- {{#callable:com.google.gson.GsonBuilderTest.testModificationAfterCreate}} -->
The `testModificationAfterCreate` method verifies that modifications to a `GsonBuilder` after creating a `Gson` instance do not affect the original `Gson` instance, but do affect new `Gson` instances created from the modified `GsonBuilder`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created and used to create a `Gson` instance.
    - The `GsonBuilder` is modified by registering custom type adapters and type hierarchy adapters for `CustomClass1`, `CustomClass2`, and `CustomClass3`.
    - The [`assertDefaultGson`](#GsonBuilderTestassertDefaultGson) method is called to verify that the original `Gson` instance remains unaffected by the modifications to the `GsonBuilder`.
    - A new `Gson` instance is created from the original `Gson` instance using `newBuilder().create()`, and [`assertDefaultGson`](#GsonBuilderTestassertDefaultGson) is called again to verify it is also unaffected by the `GsonBuilder` modifications.
    - A new `Gson` instance is created from the modified `GsonBuilder`, and [`assertCustomGson`](#GsonBuilderTestassertCustomGson) is called to verify that this new instance reflects the modifications.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of `Gson` and `GsonBuilder`.
- **Functions called**:
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.GsonBuilderTest.assertDefaultGson`](#GsonBuilderTestassertDefaultGson)
    - [`com.google.gson.Gson.newBuilder`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewBuilder)
    - [`com.google.gson.GsonBuilderTest.assertCustomGson`](#GsonBuilderTestassertCustomGson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.assertDefaultGson<!-- {{#callable:com.google.gson.GsonBuilderTest.assertDefaultGson}} -->
The `assertDefaultGson` method verifies that a given `Gson` instance uses default reflective adapters and instance creators for specific custom classes.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `gson`: An instance of the `Gson` class to be tested for default behavior.
- **Control Flow**:
    - Convert an instance of `CustomClass1` to JSON using the provided `Gson` instance and assert that the result is an empty JSON object `{}`.
    - Convert an instance of `CustomClass2` to JSON using the provided `Gson` instance and assert that the result is an empty JSON object `{}`.
    - Deserialize an empty JSON object `{}` into an instance of `CustomClass3` using the provided `Gson` instance and assert that the `s` field of the resulting object equals `CustomClass3.NO_ARG_CONSTRUCTOR_VALUE`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `Gson` instance.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.assertCustomGson<!-- {{#callable:com.google.gson.GsonBuilderTest.assertCustomGson}} -->
The `assertCustomGson` method verifies that a given `Gson` instance correctly serializes and deserializes specific custom classes using custom adapters.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `gson`: An instance of the `Gson` class to be tested for custom serialization and deserialization behavior.
- **Control Flow**:
    - Convert an instance of `CustomClass1` to JSON using the provided `Gson` instance and assert that the result is equal to the string "custom-adapter".
    - Convert an instance of `CustomClass2` to JSON using the provided `Gson` instance and assert that the result is equal to the string "custom-hierarchy-adapter".
    - Deserialize an empty JSON object into an instance of `CustomClass3` using the provided `Gson` instance and assert that the `s` field of the resulting object is equal to "custom-instance".
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `Gson` instance.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testExcludeFieldsWithModifiers<!-- {{#callable:com.google.gson.GsonBuilderTest.testExcludeFieldsWithModifiers}} -->
The method `testExcludeFieldsWithModifiers` tests the exclusion of fields with specific modifiers (volatile and private) from JSON serialization using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder` with the [`excludeFieldsWithModifiers`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers) method, specifying `Modifier.VOLATILE` and `Modifier.PRIVATE` as the modifiers to exclude.
    - A `HasModifiers` object is serialized to JSON using the `gson.toJson` method.
    - An assertion checks that the resulting JSON string is equal to `{"d":"d"}`, confirming that fields with the specified modifiers are excluded from serialization.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the Gson serialization.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.excludeFieldsWithModifiers`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers)
    - [`com.google.gson.GsonBuilder.create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testTransientFieldExclusion<!-- {{#callable:com.google.gson.GsonBuilderTest.testTransientFieldExclusion}} -->
The `testTransientFieldExclusion` method tests that Gson correctly excludes transient fields from JSON serialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder` with the [`excludeFieldsWithModifiers`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers) method, which by default excludes transient fields.
    - A `HasTransients` object is serialized to JSON using the `gson.toJson` method.
    - An assertion checks that the resulting JSON string is equal to `{"a":"a"}`, confirming that the transient field is excluded.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of Gson.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.excludeFieldsWithModifiers`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderexcludeFieldsWithModifiers)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testRegisterTypeAdapterForCoreType<!-- {{#callable:com.google.gson.GsonBuilderTest.testRegisterTypeAdapterForCoreType}} -->
The method `testRegisterTypeAdapterForCoreType` tests the registration of a null type adapter for several core Java types using the GsonBuilder.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define an array `types` containing several core Java types: `byte.class`, `int.class`, `double.class`, `Short.class`, `Long.class`, and `String.class`.
    - Iterate over each `type` in the `types` array.
    - For each `type`, create a new `GsonBuilder` instance and register a `NULL_TYPE_ADAPTER` for the current `type`.
- **Output**:
    - The method does not return any value; it is a test method that verifies the registration of type adapters for core types.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testDisableJdkUnsafe<!-- {{#callable:com.google.gson.GsonBuilderTest.testDisableJdkUnsafe}} -->
The `testDisableJdkUnsafe` method tests that disabling JDK Unsafe in Gson results in a `JsonIOException` when trying to deserialize a class without a no-args constructor.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is created using `GsonBuilder` with `disableJdkUnsafe()` method called.
    - The method `assertThrows` is used to verify that a `JsonIOException` is thrown when attempting to deserialize a JSON string into `ClassWithoutNoArgsConstructor` using the `gson.fromJson` method.
    - The exception message is asserted to ensure it matches the expected message indicating the inability to create an instance due to JDK Unsafe being disabled.
- **Output**:
    - The method does not return any value; it asserts that a `JsonIOException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.disableJdkUnsafe`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderdisableJdkUnsafe)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetVersionInvalid<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetVersionInvalid}} -->
The `testSetVersionInvalid` method tests that setting an invalid version on a `GsonBuilder` instance throws an `IllegalArgumentException` with the expected error message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created.
    - The method uses `assertThrows` to verify that calling [`setVersion`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetVersion) with `Double.NaN` on the `GsonBuilder` instance throws an `IllegalArgumentException`.
    - The exception message is checked to ensure it equals 'Invalid version: NaN'.
    - The method again uses `assertThrows` to verify that calling [`setVersion`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetVersion) with `-0.1` on the `GsonBuilder` instance throws an `IllegalArgumentException`.
    - The exception message is checked to ensure it equals 'Invalid version: -0.1'.
- **Output**:
    - The method does not return any value; it verifies that exceptions are thrown with the correct messages.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setVersion`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetVersion)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testDefaultStrictness<!-- {{#callable:com.google.gson.GsonBuilderTest.testDefaultStrictness}} -->
The `testDefaultStrictness` method verifies that the default strictness level for JSON reading and writing in a `Gson` instance is set to `LEGACY_STRICT`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created and used to create a `Gson` instance.
    - A `JsonReader` is created using the `Gson` instance and a `StringReader` initialized with an empty JSON object (`{}`).
    - The strictness level of the `JsonReader` is asserted to be `Strictness.LEGACY_STRICT`.
    - A `JsonWriter` is created using the `Gson` instance and a `StringWriter`.
    - The strictness level of the `JsonWriter` is asserted to be `Strictness.LEGACY_STRICT`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the strictness level of JSON readers and writers.
- **Functions called**:
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.newJsonReader`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonReader)
    - [`com.google.gson.stream.JsonReader.getStrictness`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetStrictness)
    - [`com.google.gson.Gson.newJsonWriter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonWriter)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetLenient<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetLenient}} -->
The `testSetLenient` method tests that a Gson instance created with a lenient GsonBuilder has lenient strictness for both JSON reading and writing.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `GsonBuilder` instance is created.
    - The [`setLenient`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetLenient) method is called on the builder to enable lenient parsing.
    - A `Gson` instance is created from the builder.
    - A `JsonReader` is created using the `Gson` instance and a `StringReader` initialized with an empty JSON object.
    - The strictness of the `JsonReader` is asserted to be `Strictness.LENIENT`.
    - A `JsonWriter` is created using the `Gson` instance and a `StringWriter`.
    - The strictness of the `JsonWriter` is asserted to be `Strictness.LENIENT`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the lenient strictness of the Gson instance.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setLenient`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetLenient)
    - [`com.google.gson.GsonBuilder.create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.newJsonReader`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonReader)
    - [`com.google.gson.stream.JsonWriter.getStrictness`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritergetStrictness)
    - [`com.google.gson.Gson.newJsonWriter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonWriter)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetStrictness<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetStrictness}} -->
The `testSetStrictness` method tests that the strictness level set in a `GsonBuilder` is correctly applied to both `JsonReader` and `JsonWriter` instances created from the resulting `Gson` object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `Strictness` variable with the value `Strictness.STRICT`.
    - Create a `GsonBuilder` instance.
    - Set the strictness of the `GsonBuilder` to the initialized `Strictness` value using `setStrictness(strictness)`.
    - Create a `Gson` instance from the `GsonBuilder`.
    - Assert that the `Strictness` of a `JsonReader` created from the `Gson` instance is equal to the initialized `Strictness` value.
    - Assert that the `Strictness` of a `JsonWriter` created from the `Gson` instance is equal to the initialized `Strictness` value.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correct behavior of the `Gson` instance.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setStrictness`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetStrictness)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.newJsonReader`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonReader)
    - [`com.google.gson.stream.JsonReader.getStrictness`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetStrictness)
    - [`com.google.gson.Gson.newJsonWriter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonWriter)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testRegisterTypeAdapterForObjectAndJsonElements<!-- {{#callable:com.google.gson.GsonBuilderTest.testRegisterTypeAdapterForObjectAndJsonElements}} -->
This method tests that registering a type adapter for certain core types like Object using GsonBuilder throws an IllegalArgumentException.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a string variable `errorMessage` with the value 'Cannot override built-in adapter for '.
    - Create an array `types` containing the class `Object.class`.
    - Instantiate a `GsonBuilder` object named `gsonBuilder`.
    - Iterate over each `type` in the `types` array.
    - For each `type`, use `assertThrows` to verify that registering a type adapter for the `type` with `gsonBuilder` throws an `IllegalArgumentException`.
    - Check that the exception message is equal to `errorMessage` concatenated with the `type`.
- **Output**:
    - The method does not return any value; it asserts that an exception is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testRegisterTypeAdapterForJsonElements<!-- {{#callable:com.google.gson.GsonBuilderTest.testRegisterTypeAdapterForJsonElements}} -->
The method `testRegisterTypeAdapterForJsonElements` verifies that registering a type adapter for `JsonArray` does not override the built-in adapter and that the default serialization behavior remains unchanged.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder` with a registered type adapter for `JsonArray` using `NULL_TYPE_ADAPTER`.
    - The `TypeAdapter` for `JsonArray` is retrieved from the `Gson` instance.
    - An assertion checks that the retrieved adapter is not the same instance as `NULL_TYPE_ADAPTER`.
    - Another assertion checks that the [`toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the adapter serializes an empty `JsonArray` to the string "[]".
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the registered adapter is not used and the default serialization behavior is maintained.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.getAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testRegisterTypeHierarchyAdapterJsonElements<!-- {{#callable:com.google.gson.GsonBuilderTest.testRegisterTypeHierarchyAdapterJsonElements}} -->
The method tests the behavior of registering type hierarchy adapters for JsonElement and its subclasses in GsonBuilder, ensuring that it throws an IllegalArgumentException for these types but allows it for Object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a String variable `errorMessage` with the value 'Cannot override built-in adapter for '.
    - Create an array `types` containing `JsonElement.class` and `JsonArray.class`.
    - Instantiate a `GsonBuilder` object named `gsonBuilder`.
    - Iterate over each `type` in the `types` array.
    - For each `type`, use `assertThrows` to verify that registering a type hierarchy adapter for the `type` with `NULL_TYPE_ADAPTER` throws an `IllegalArgumentException`.
    - Assert that the exception message is equal to `errorMessage` concatenated with the `type`.
    - Register a type hierarchy adapter for `Object.class` with `NULL_TYPE_ADAPTER` without expecting an exception.
- **Output**:
    - The method does not return any value; it is a test method that asserts expected exceptions and behaviors.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testRegisterTypeHierarchyAdapterJsonElements\_Allowed<!-- {{#callable:com.google.gson.GsonBuilderTest.testRegisterTypeHierarchyAdapterJsonElements_Allowed}} -->
The method tests that registering a type hierarchy adapter for JsonArray is allowed but does not affect the default adapter behavior.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Gson object is created using GsonBuilder with a registered type hierarchy adapter for JsonArray using NULL_TYPE_ADAPTER.
    - The TypeAdapter for JsonArray is retrieved from the Gson object.
    - An assertion checks that the retrieved adapter is not the same instance as NULL_TYPE_ADAPTER, indicating the registered adapter was not used.
    - Another assertion checks that converting a new JsonArray to JSON using the adapter results in an empty JSON array string '[]'.
- **Output**:
    - The method does not return any value as it is a test method using assertions to verify behavior.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.getAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetDateFormatWithInvalidPattern<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetDateFormatWithInvalidPattern}} -->
The method `testSetDateFormatWithInvalidPattern` tests that setting an invalid date format pattern in a `GsonBuilder` throws an `IllegalArgumentException` with a specific error message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created.
    - An invalid date format pattern string is defined.
    - The method asserts that an `IllegalArgumentException` is thrown when attempting to set the invalid date format pattern using `builder.setDateFormat(invalidPattern)`.
    - The exception's message is checked to ensure it matches the expected error message indicating the pattern is not valid.
- **Output**:
    - The method does not return any value; it is a test method that verifies behavior through assertions.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetDateFormatWithValidPattern<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetDateFormatWithValidPattern}} -->
The method `testSetDateFormatWithValidPattern` tests that setting a valid date format pattern on a `GsonBuilder` does not throw an exception.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `GsonBuilder` object.
    - Define a valid date format pattern string `"yyyy-MM-dd"`.
    - Call [`setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat) on the `GsonBuilder` instance with the valid pattern, ensuring no exception is thrown.
- **Output**:
    - The method does not return any value; it verifies that no exception is thrown when setting a valid date format pattern.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetDateFormatNullPattern<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetDateFormatNullPattern}} -->
The method `testSetDateFormatNullPattern` tests the behavior of the `GsonBuilder` when setting a null date format, ensuring it resets to the default format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `GsonBuilder` object.
    - Create a `Date` object initialized to the epoch time (0).
    - Convert the `Date` object to JSON using the default `GsonBuilder` settings and store the result in `originalFormatted`.
    - Set a custom date format ('yyyy-MM-dd') on the `GsonBuilder`, convert the `Date` object to JSON, and store the result in `customFormatted`.
    - Assert that `customFormatted` is not equal to `originalFormatted`, indicating the custom format was applied.
    - Set the date format to `null` on the `GsonBuilder`, convert the `Date` object to JSON, and store the result in `resetFormatted`.
    - Assert that `resetFormatted` is equal to `originalFormatted`, indicating the format was reset to the default.
- **Output**:
    - The method does not return a value; it uses assertions to verify the behavior of the `GsonBuilder` when setting a null date format.
- **Functions called**:
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetDateFormatEmptyPattern<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetDateFormatEmptyPattern}} -->
The method `testSetDateFormatEmptyPattern` verifies that setting an empty date format pattern in a `GsonBuilder` does not alter the default date serialization behavior.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created.
    - A `Date` object is instantiated with the epoch time (0).
    - The `Date` object is serialized to JSON using the default `GsonBuilder` configuration, and the result is stored in `originalFormatted`.
    - The `GsonBuilder` is configured with an empty date format pattern ("    "), and the `Date` object is serialized again, storing the result in `emptyFormatted`.
    - An assertion checks that `emptyFormatted` is equal to `originalFormatted`, confirming that the empty pattern was ignored.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the `GsonBuilder` when an empty date format pattern is set.
- **Functions called**:
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetDateFormatValidStyle<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetDateFormatValidStyle}} -->
The method `testSetDateFormatValidStyle` tests that setting valid date styles in a `GsonBuilder` does not throw exceptions.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created.
    - An array `validStyles` is initialized with valid date format styles: `DateFormat.FULL`, `DateFormat.LONG`, `DateFormat.MEDIUM`, and `DateFormat.SHORT`.
    - A loop iterates over each style in `validStyles`.
    - For each style, `builder.setDateFormat(style)` is called to set the date format style.
    - For each style, `builder.setDateFormat(style, style)` is called to set both date and time format styles.
- **Output**:
    - The method does not return any value; it verifies that no exceptions are thrown when setting valid date styles.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)


---
#### GsonBuilderTest\.testSetDateFormatInvalidStyle<!-- {{#callable:com.google.gson.GsonBuilderTest.testSetDateFormatInvalidStyle}} -->
The method `testSetDateFormatInvalidStyle` tests the `GsonBuilder.setDateFormat` method to ensure it throws an `IllegalArgumentException` when provided with invalid style values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created.
    - The method uses `assertThrows` to verify that calling [`setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat) with an invalid style value of `-1` throws an `IllegalArgumentException`.
    - The exception message is checked to ensure it equals 'Invalid style: -1'.
    - The method repeats the above steps for another invalid style value of `4`.
    - The method tests [`setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat) with two parameters, ensuring that invalid style values for either parameter throw an `IllegalArgumentException`.
    - The exception messages for these cases are also verified to match the expected 'Invalid style: -1'.
- **Output**:
    - The method does not return any value; it verifies that exceptions are thrown for invalid input.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
- **See also**: [`com.google.gson.GsonBuilderTest`](#GsonBuilderTest)  (Base Class)



---
### CustomClass1<!-- {{#class:com.google.gson.GsonBuilderTest.CustomClass1}} -->
- **Modifiers**: `static`
- **Description**: `CustomClass1` is a simple static inner class within the `GsonBuilderTest` class, primarily used for testing purposes in the context of Gson serialization and deserialization.


---
### CustomClass2<!-- {{#class:com.google.gson.GsonBuilderTest.CustomClass2}} -->
- **Modifiers**: `static`
- **Description**: `CustomClass2` is a static inner class within the `GsonBuilderTest` class, primarily used for testing purposes in the context of the Gson library. It is utilized in the test cases to verify the behavior of Gson's type adapter registration and serialization/deserialization processes, particularly when custom type hierarchy adapters are involved.


---
### CustomClass3<!-- {{#class:com.google.gson.GsonBuilderTest.CustomClass3}} -->
- **Modifiers**: `static`
- **Description**: CustomClass3 is a static class designed to encapsulate a string value, providing constructors for both custom and default initialization. It includes a static final field for a default string value used in the no-argument constructor.
- **Fields**:
    - `NO_ARG_CONSTRUCTOR_VALUE`: `String` A static final string used as the default value for the no-argument constructor.
    - `s`: `String` A final string field that holds the value passed during the object's construction.
- **Methods**:
    - [`com.google.gson.GsonBuilderTest.CustomClass3.CustomClass3`](#CustomClass3CustomClass3)
    - [`com.google.gson.GsonBuilderTest.CustomClass3.CustomClass3`](#CustomClass3CustomClass3)

**Methods**

---
#### CustomClass3\.CustomClass3<!-- {{#callable:com.google.gson.GsonBuilderTest.CustomClass3.CustomClass3}} -->
The constructor `CustomClass3(String s)` initializes a new instance of `CustomClass3` with a specified string value.
- **Modifiers**: `public`
- **Inputs**:
    - `s`: A string value used to initialize the instance variable `s` of the `CustomClass3` object.
- **Control Flow**:
    - The constructor takes a single string argument `s`.
    - It assigns the value of the argument `s` to the instance variable `this.s`.
- **Output**:
    - This constructor does not return any value as it is a constructor for initializing an object of `CustomClass3`.
- **See also**: [`com.google.gson.GsonBuilderTest.CustomClass3`](#GsonBuilderTest.CustomClass3)  (Base Class)


---
#### CustomClass3\.CustomClass3<!-- {{#callable:com.google.gson.GsonBuilderTest.CustomClass3.CustomClass3}} -->
The `CustomClass3` constructor initializes an instance of `CustomClass3` with a default string value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor calls another constructor of the same class using `this` keyword, passing `NO_ARG_CONSTRUCTOR_VALUE` as an argument.
- **Output**:
    - An instance of `CustomClass3` is created with its `s` field set to `NO_ARG_CONSTRUCTOR_VALUE`.
- **See also**: [`com.google.gson.GsonBuilderTest.CustomClass3`](#GsonBuilderTest.CustomClass3)  (Base Class)



---
### HasModifiers<!-- {{#class:com.google.gson.GsonBuilderTest.HasModifiers}} -->
- **Modifiers**: `static`
- **Description**: The `HasModifiers` class is a simple static class that contains four string fields with various access and concurrency modifiers, demonstrating the use of `private`, `volatile`, and default (package-private) access levels.
- **Fields**:
    - `a`: `String` A private string field initialized to "a".
    - `b`: `String` A volatile string field initialized to "b".
    - `c`: `String` A private volatile string field initialized to "c".
    - `d`: `String` A package-private string field initialized to "d".


---
### HasTransients<!-- {{#class:com.google.gson.GsonBuilderTest.HasTransients}} -->
- **Modifiers**: `static`
- **Description**: The `HasTransients` class is a simple static class that contains a single transient field `a` of type `String`, initialized to the value "a". The transient keyword indicates that this field should not be serialized when the object is converted to a byte stream, which is useful in scenarios where certain fields should not be persisted.
- **Fields**:
    - `a`: `String` A transient String field initialized to "a".


---
### ClassWithoutNoArgsConstructor<!-- {{#class:com.google.gson.GsonBuilderTest.ClassWithoutNoArgsConstructor}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithoutNoArgsConstructor` is a private static class that lacks a no-argument constructor, having only a single constructor that takes a `String` parameter. This design choice is significant in the context of the Gson library, as it demonstrates a scenario where Gson cannot instantiate the class without using JDK Unsafe or an `InstanceCreator`, highlighting the importance of having a no-argument constructor for classes that need to be deserialized by Gson.
- **Methods**:
    - [`com.google.gson.GsonBuilderTest.ClassWithoutNoArgsConstructor.ClassWithoutNoArgsConstructor`](#ClassWithoutNoArgsConstructorClassWithoutNoArgsConstructor)

**Methods**

---
#### ClassWithoutNoArgsConstructor\.ClassWithoutNoArgsConstructor<!-- {{#callable:com.google.gson.GsonBuilderTest.ClassWithoutNoArgsConstructor.ClassWithoutNoArgsConstructor}} -->
The constructor `ClassWithoutNoArgsConstructor` initializes an instance of the class with a given string parameter.
- **Modifiers**: `public`
- **Inputs**:
    - `s`: A string parameter used to initialize the class instance.
- **Control Flow**:
    - The constructor takes a single string argument 's'.
    - It initializes an instance of the class using the provided string.
- **Output**:
    - This constructor does not return any value as it is a constructor for the class.
- **See also**: [`com.google.gson.GsonBuilderTest.ClassWithoutNoArgsConstructor`](#GsonBuilderTest.ClassWithoutNoArgsConstructor)  (Base Class)



