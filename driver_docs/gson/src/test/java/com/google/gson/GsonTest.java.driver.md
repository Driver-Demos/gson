# Purpose
The provided Java source code is a comprehensive test suite for the Gson library, specifically focusing on the functionality and behavior of the `Gson` class. This test suite is designed to ensure the correctness and robustness of Gson's serialization and deserialization processes, as well as its configuration capabilities. The code includes a variety of unit tests that cover different aspects of the Gson library, such as custom type adapters, concurrency handling, and the behavior of Gson's builder pattern. The tests utilize JUnit for assertions and are structured to verify that Gson behaves as expected under various conditions, including custom configurations and edge cases.

Key technical components of this test suite include the use of custom `TypeAdapter` implementations to test Gson's extensibility, the use of `TypeAdapterFactory` to verify the creation and delegation of adapters, and the handling of concurrency issues with `CountDownLatch` and `AtomicReference`. The tests also explore the behavior of Gson's `newBuilder()` method, ensuring that modifications to a builder do not affect the original Gson instance. This suite is crucial for maintaining the integrity of the Gson library, providing a reliable mechanism to catch regressions and ensure that new features or changes do not introduce bugs.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.Gson.FutureTypeAdapter`
- `com.google.gson.internal.Excluder`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.IOException`
- `java.io.StringReader`
- `java.io.StringWriter`
- `java.text.DateFormat`
- `java.util.ArrayList`
- `java.util.Collections`
- `java.util.HashMap`
- `java.util.concurrent.CountDownLatch`
- `java.util.concurrent.atomic.AtomicInteger`
- `java.util.concurrent.atomic.AtomicReference`
- `org.junit.Test`


# Classes

---
### GsonTest<!-- {{#class:com.google.gson.GsonTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `GsonTest` class is a comprehensive suite of unit tests for the Gson library, designed to verify the functionality and robustness of various Gson features, including custom serialization and deserialization strategies, type adapter factories, and concurrency handling. It includes tests for default and custom configurations, ensuring that Gson behaves correctly under different scenarios, such as handling null values, managing type adapters, and maintaining thread safety. The class also tests the behavior of Gson's builder pattern, ensuring that modifications to builders do not affect the original Gson instances.
- **Fields**:
    - `CUSTOM_EXCLUDER`: `Excluder` A static final Excluder instance configured to exclude fields without the @Expose annotation and disable inner class serialization.
    - `CUSTOM_FIELD_NAMING_STRATEGY`: `FieldNamingStrategy` A static final FieldNamingStrategy that renames all fields to 'foo'.
    - `CUSTOM_OBJECT_TO_NUMBER_STRATEGY`: `ToNumberStrategy` A static final ToNumberStrategy that converts objects to numbers using the DOUBLE policy.
    - `CUSTOM_NUMBER_TO_NUMBER_STRATEGY`: `ToNumberStrategy` A static final ToNumberStrategy that converts numbers using the LAZILY_PARSED_NUMBER policy.
- **Methods**:
    - [`com.google.gson.GsonTest.testStrictnessDefault`](#GsonTesttestStrictnessDefault)
    - [`com.google.gson.GsonTest.testOverridesDefaultExcluder`](#GsonTesttestOverridesDefaultExcluder)
    - [`com.google.gson.GsonTest.testClonedTypeAdapterFactoryListsAreIndependent`](#GsonTesttestClonedTypeAdapterFactoryListsAreIndependent)
    - [`com.google.gson.GsonTest.testFromJson_WrongResultType`](#GsonTesttestFromJson_WrongResultType)
    - [`com.google.gson.GsonTest.testGetAdapter_Null`](#GsonTesttestGetAdapter_Null)
    - [`com.google.gson.GsonTest.testGetAdapter_Concurrency`](#GsonTesttestGetAdapter_Concurrency)
    - [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency`](#GsonTesttestGetAdapter_FutureAdapterConcurrency)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter`](#GsonTesttestGetDelegateAdapter)
    - [`com.google.gson.GsonTest.testNewJsonWriter_Default`](#GsonTesttestNewJsonWriter_Default)
    - [`com.google.gson.GsonTest.testNewJsonWriter_Custom`](#GsonTesttestNewJsonWriter_Custom)
    - [`com.google.gson.GsonTest.testNewJsonReader_Default`](#GsonTesttestNewJsonReader_Default)
    - [`com.google.gson.GsonTest.testNewJsonReader_Custom`](#GsonTesttestNewJsonReader_Custom)
    - [`com.google.gson.GsonTest.testDefaultGsonNewBuilderModification`](#GsonTesttestDefaultGsonNewBuilderModification)
    - [`com.google.gson.GsonTest.assertDefaultGson`](#GsonTestassertDefaultGson)
    - [`com.google.gson.GsonTest.testNewBuilderModification`](#GsonTesttestNewBuilderModification)
    - [`com.google.gson.GsonTest.assertCustomGson`](#GsonTestassertCustomGson)

**Methods**

---
#### GsonTest\.testStrictnessDefault<!-- {{#callable:com.google.gson.GsonTest.testStrictnessDefault}} -->
The `testStrictnessDefault` method verifies that the `strictness` field of a newly created `Gson` object is `null` by default.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Gson` object is instantiated.
    - The `strictness` field of the `Gson` object is checked to ensure it is `null` using the `assertThat` method from the `Truth` library.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the default state of the `strictness` field in a `Gson` object.
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testOverridesDefaultExcluder<!-- {{#callable:com.google.gson.GsonTest.testOverridesDefaultExcluder}} -->
The method `testOverridesDefaultExcluder` tests if a `Gson` instance correctly overrides its default settings with custom configurations.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated with custom configurations including a custom excluder, field naming strategy, and other settings.
    - Assertions are made to verify that the `Gson` instance's excluder, field naming strategy, and other properties match the custom configurations provided during instantiation.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `Gson` instance.
- **Functions called**:
    - [`com.google.gson.Gson.fieldNamingStrategy`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfieldNamingStrategy)
    - [`com.google.gson.Gson.serializeNulls`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls)
    - [`com.google.gson.Gson.htmlSafe`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonhtmlSafe)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testClonedTypeAdapterFactoryListsAreIndependent<!-- {{#callable:com.google.gson.GsonTest.testClonedTypeAdapterFactoryListsAreIndependent}} -->
This method tests that the type adapter factory lists in a cloned Gson object are independent from the original Gson object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create an original Gson object with custom configurations and empty type adapter factory lists.
    - Clone the original Gson object using its newBuilder method and register a new type adapter for the int class in the clone.
    - Assert that the clone's factories list size is one more than the original's, indicating that the clone's list is independent.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the independence of the type adapter factory lists.
- **Functions called**:
    - [`com.google.gson.Gson.newBuilder`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewBuilder)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testFromJson\_WrongResultType<!-- {{#callable:com.google.gson.GsonTest.testFromJson_WrongResultType}} -->
The `testFromJson_WrongResultType` method tests the behavior of Gson when a type adapter returns a different type than expected during JSON deserialization.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a custom `IntegerAdapter` class extending `TypeAdapter<Integer>` that always returns the integer 3 when reading JSON and throws an error when writing JSON.
    - Create a `Gson` instance with `IntegerAdapter` registered for `Boolean.class` and attempt to deserialize a JSON string "true" into a `Boolean`, expecting a `ClassCastException`.
    - Verify that the exception message indicates the wrong type was returned by the adapter.
    - Create another `Gson` instance with `IntegerAdapter` registered for `int.class` and verify that deserializing "0" into an `int` returns 3, demonstrating that boxed primitives are allowed.
    - Define a `NullAdapter` class extending `TypeAdapter<Object>` that always returns `null` when reading JSON and throws an error when writing JSON.
    - Create a `Gson` instance with `NullAdapter` registered for `Boolean.class` and verify that deserializing "true" into a `Boolean` returns `null`, demonstrating that returning `null` is allowed.
- **Output**:
    - The method does not return any value; it performs assertions to verify expected behavior.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.internal.Excluder.create`](../../../../../main/java/com/google/gson/internal/Excluder.java.driver.md#Excludercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testGetAdapter\_Null<!-- {{#callable:com.google.gson.GsonTest.testGetAdapter_Null}} -->
The `testGetAdapter_Null` method tests that calling `Gson.getAdapter` with a null `TypeToken` argument throws a `NullPointerException` with a specific error message.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` object is instantiated.
    - The `assertThrows` method is used to verify that calling `gson.getAdapter` with a null `TypeToken` throws a `NullPointerException`.
    - The exception's message is checked to ensure it equals 'type must not be null'.
- **Output**:
    - The method does not return any value; it asserts that a `NullPointerException` is thrown with a specific message.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testGetAdapter\_Concurrency<!-- {{#callable:com.google.gson.GsonTest.testGetAdapter_Concurrency}} -->
The `testGetAdapter_Concurrency` method tests the concurrency behavior of the Gson library when multiple threads request type adapters simultaneously.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `DummyAdapter` class is defined, extending `TypeAdapter`, with unimplemented `write` and `read` methods that throw `AssertionError`.
    - An `AtomicInteger` and an `AtomicReference` are initialized to track the number of adapter instances created and to store the adapter obtained by a separate thread, respectively.
    - A `Gson` instance is created with a custom `TypeAdapterFactory` that creates a new `DummyAdapter` instance and starts a separate thread to request an adapter for the same type.
    - The separate thread sets the `threadAdapter` reference to the adapter it retrieves.
    - The main thread retrieves an adapter for the requested type and asserts that two adapter instances were created and both are instances of `DummyAdapter`.
- **Output**:
    - The method does not return a value but asserts that two `DummyAdapter` instances are created and both are of the correct type.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonArray.set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.Gson.getAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testGetAdapter\_FutureAdapterConcurrency<!-- {{#callable:com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency}} -->
The method `testGetAdapter_FutureAdapterConcurrency` tests the concurrency behavior of Gson's [`getAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter) method when dealing with cyclic dependencies and unresolved `FutureTypeAdapter` instances.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define an inner class `WrappingAdapter` that wraps another `TypeAdapter` and overrides the [`write`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite) method to handle infinite recursion by tracking nested calls.
    - Initialize two `CountDownLatch` objects, `isThreadWaiting` and `canThreadProceed`, to manage thread synchronization.
    - Create a `Gson` instance with a custom `TypeAdapterFactory` that handles `CustomClass1` and `CustomClass2`, introducing a cyclic dependency between them.
    - Start a new thread that requests a `TypeAdapter` for `CustomClass1`, which will wait due to the `CountDownLatch`.
    - In the main thread, request a `TypeAdapter` for `CustomClass1`, ensuring it does not fail due to unresolved `FutureTypeAdapter`.
    - Allow the other thread to proceed by counting down `canThreadProceed`, resolving its `FutureTypeAdapter`, and verify the output.
- **Output**:
    - The method does not return a value but asserts that the JSON output of the adapters is equal to "[["wrapped-nested"]]".
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.TypeAdapter.write`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.create`](#GsonTesttestGetAdapter_FutureAdapterConcurrency.create)
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.Gson.getAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.JsonArray.set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testGetDelegateAdapter<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter}} -->
The `testGetDelegateAdapter` method tests the behavior of the `Gson.getDelegateAdapter` method with custom `TypeAdapterFactory` and `TypeAdapter` implementations.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a `DummyAdapter` class extending `TypeAdapter<Number>` with overridden `read`, `write`, and `toString` methods.
    - Define a `DummyFactory` class implementing `TypeAdapterFactory` with overridden [`create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate), [[`equals`](#GsonTesttestGetDelegateAdapter.DummyFactory.equals)](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectequals), and `hashCode` methods.
    - Create two `DummyAdapter` instances (`adapter1` and `adapter2`) and corresponding `DummyFactory` instances (`factory1` and `factory2`).
    - Create a `Gson` instance with `factory1` and `factory2` registered in 'last in, first out' order.
    - Create a `TypeToken` for `Number` type.
    - Use `assertThrows` to verify `NullPointerException` is thrown when `null` is passed to [`getDelegateAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter).
    - Assert that [`getDelegateAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter) returns `adapter2` for an unknown factory and `type`.
    - Assert that [`getDelegateAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter) returns `adapter1` for `factory2` and `type`.
    - Assert that [`getDelegateAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter) returns a default adapter (not `DummyAdapter`) for `factory1` and `type`.
    - Create a `DummyFactory` (`factory1Eq`) equivalent to `factory1` and verify equality.
    - Assert that [`getDelegateAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter) returns `adapter2` for `factory1Eq` and `type`, ignoring custom [[`equals`](#GsonTesttestGetDelegateAdapter.DummyFactory.equals)](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectequals) method.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of `Gson.getDelegateAdapter`.
- **Functions called**:
    - [`com.google.gson.JsonObject.equals`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectequals)
    - [`com.google.gson.GsonBuilder.registerTypeAdapterFactory`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapterFactory)
    - [`com.google.gson.GsonBuilder.create`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.Gson.getDelegateAdapter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](#GsonTesttestGetDelegateAdapter.DummyFactory.equals)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testNewJsonWriter\_Default<!-- {{#callable:com.google.gson.GsonTest.testNewJsonWriter_Default}} -->
The `testNewJsonWriter_Default` method tests the default behavior of a `JsonWriter` created by Gson, ensuring it correctly handles JSON object creation and throws an exception when attempting to add multiple top-level values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` is instantiated to capture the JSON output.
    - A `JsonWriter` is created using Gson's [`newJsonWriter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonWriter) method with the `StringWriter`.
    - The `JsonWriter` begins a JSON object, writes a name-value pair with a null value, and another name-value pair with a boolean value.
    - The JSON object is closed using [`endObject`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject).
    - An attempt is made to write an additional top-level value, which is expected to throw an `IllegalStateException`.
    - The exception is caught and its message is asserted to ensure it matches the expected error message.
    - The `JsonWriter` is closed, and the resulting JSON string is asserted to match the expected output.
- **Output**:
    - The method does not return a value but asserts that the JSON output is correct and that an exception is thrown when expected.
- **Functions called**:
    - [`com.google.gson.Gson.newJsonWriter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonWriter)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testNewJsonWriter\_Custom<!-- {{#callable:com.google.gson.GsonTest.testNewJsonWriter_Custom}} -->
The `testNewJsonWriter_Custom` method tests the creation and functionality of a custom-configured `JsonWriter` using `GsonBuilder` with specific settings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `StringWriter` instance is created to capture the JSON output.
    - A `JsonWriter` is instantiated using a `GsonBuilder` with custom settings: HTML escaping is disabled, non-executable JSON is generated, pretty printing is enabled, null values are serialized, and lenient parsing is set.
    - The `JsonWriter` begins writing a JSON object, adds a name-value pair with a null value, and another name-value pair with a boolean value.
    - An additional top-level value is added to the JSON output.
    - The `JsonWriter` is closed, finalizing the JSON output.
    - An assertion checks that the output matches the expected JSON string.
- **Output**:
    - The method does not return a value but asserts that the JSON output matches the expected string: ")]}'\n{\n  \"test\": null,\n  \"<test2\": true\n}1".
- **Functions called**:
    - [`com.google.gson.GsonBuilder.disableHtmlEscaping`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderdisableHtmlEscaping)
    - [`com.google.gson.GsonBuilder.generateNonExecutableJson`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildergenerateNonExecutableJson)
    - [`com.google.gson.GsonBuilder.setPrettyPrinting`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetPrettyPrinting)
    - [`com.google.gson.Gson.serializeNulls`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonserializeNulls)
    - [`com.google.gson.stream.JsonWriter.setLenient`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetLenient)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.newJsonWriter`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonWriter)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testNewJsonReader\_Default<!-- {{#callable:com.google.gson.GsonTest.testNewJsonReader_Default}} -->
The method `testNewJsonReader_Default` tests the behavior of `JsonReader` when reading a malformed JSON string without quotes, expecting a `MalformedJsonException` to be thrown.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A string `json` is initialized with the value `"test"`, which is a malformed JSON string because it lacks quotes.
    - A `JsonReader` object is created using `Gson`'s [`newJsonReader`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonReader) method, passing a `StringReader` initialized with the `json` string.
    - The method `assertThrows` is used to verify that calling `jsonReader.nextString()` throws a `MalformedJsonException`.
    - The `JsonReader` is closed using `jsonReader.close()`.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies that a `MalformedJsonException` is thrown when attempting to read a malformed JSON string.
- **Functions called**:
    - [`com.google.gson.Gson.newJsonReader`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonReader)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testNewJsonReader\_Custom<!-- {{#callable:com.google.gson.GsonTest.testNewJsonReader_Custom}} -->
The method `testNewJsonReader_Custom` tests the creation and functionality of a lenient `JsonReader` using a custom `GsonBuilder`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A string `json` is initialized with the value "test".
    - A `JsonReader` is created using a `GsonBuilder` with lenient settings, reading from a `StringReader` initialized with `json`.
    - The method asserts that the next string read by `jsonReader` is equal to "test".
    - The `jsonReader` is closed.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setLenient`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetLenient)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.Gson.newJsonReader`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewJsonReader)
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.close`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterclose)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testDefaultGsonNewBuilderModification<!-- {{#callable:com.google.gson.GsonTest.testDefaultGsonNewBuilderModification}} -->
The method tests that modifications to a GsonBuilder obtained from a default Gson instance do not affect the original Gson instance or a new GsonBuilder created from it, but do affect a new Gson instance created from the modified GsonBuilder.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new Gson instance is created using the default constructor.
    - A GsonBuilder is obtained from the Gson instance using the newBuilder() method.
    - Custom type adapters and hierarchy adapters are registered with the GsonBuilder for CustomClass1, CustomClass2, and CustomClass3.
    - The assertDefaultGson method is called to verify that the original Gson instance remains unaffected by the modifications to the GsonBuilder.
    - A new Gson instance is created from a new GsonBuilder obtained from the original Gson instance, and assertDefaultGson is called again to verify it remains unaffected.
    - A new Gson instance is created from the modified GsonBuilder, and assertCustomGson is called to verify it uses the custom adapters.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of Gson and GsonBuilder.
- **Functions called**:
    - [`com.google.gson.Gson.newBuilder`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewBuilder)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.GsonBuilderTest.assertDefaultGson`](GsonBuilderTest.java.driver.md#GsonBuilderTestassertDefaultGson)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.GsonBuilderTest.assertCustomGson`](GsonBuilderTest.java.driver.md#GsonBuilderTestassertCustomGson)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.assertDefaultGson<!-- {{#callable:com.google.gson.GsonTest.assertDefaultGson}} -->
The `assertDefaultGson` method verifies that a given `Gson` instance uses default reflective adapters and instance creators for specific custom classes.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `gson`: An instance of the `Gson` class to be tested for default behavior.
- **Control Flow**:
    - Convert an instance of `CustomClass1` to JSON using the provided `Gson` instance and assert that the result is an empty JSON object `{}`.
    - Convert an instance of `CustomClass2` to JSON using the provided `Gson` instance and assert that the result is an empty JSON object `{}`.
    - Deserialize an empty JSON object `{}` into an instance of `CustomClass3` using the provided `Gson` instance and assert that the `s` field of the resulting object equals `CustomClass3.NO_ARG_CONSTRUCTOR_VALUE`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `Gson` instance.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.testNewBuilderModification<!-- {{#callable:com.google.gson.GsonTest.testNewBuilderModification}} -->
The `testNewBuilderModification` method tests the behavior of modifying a `GsonBuilder` obtained from an existing `Gson` instance and ensures that the original `Gson` instance remains unaffected by these modifications.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using a `GsonBuilder` with custom type adapters for `CustomClass1`, `CustomClass2`, and `CustomClass3`.
    - The [`assertCustomGson`](GsonBuilderTest.java.driver.md#GsonBuilderTestassertCustomGson) method is called to verify the behavior of the `Gson` instance with the custom adapters.
    - A new `GsonBuilder` is obtained from the existing `Gson` instance using `gson.newBuilder()`, and this builder is modified with new type adapters for the same classes.
    - The [`assertCustomGson`](GsonBuilderTest.java.driver.md#GsonBuilderTestassertCustomGson) method is called again to ensure that the original `Gson` instance is unaffected by the modifications to the new `GsonBuilder`.
    - A new `Gson` instance is created from the modified `GsonBuilder`, and its behavior is verified to reflect the changes using assertions on the serialized and deserialized outputs of `CustomClass1`, `CustomClass2`, and `CustomClass3`.
- **Output**:
    - The method does not return any value but uses assertions to verify that the original `Gson` instance remains unchanged and that the new `Gson` instance reflects the modifications made to the `GsonBuilder`.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.registerTypeHierarchyAdapter`](../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeHierarchyAdapter)
    - [`com.google.gson.JsonArrayAsListSuiteTest.ListGenerator.create`](JsonArrayAsListSuiteTest.java.driver.md#ListGeneratorcreate)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.GsonBuilderTest.assertCustomGson`](GsonBuilderTest.java.driver.md#GsonBuilderTestassertCustomGson)
    - [`com.google.gson.Gson.newBuilder`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonnewBuilder)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)


---
#### GsonTest\.assertCustomGson<!-- {{#callable:com.google.gson.GsonTest.assertCustomGson}} -->
The `assertCustomGson` method verifies that a given `Gson` instance correctly serializes and deserializes specific custom classes using custom adapters.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `gson`: An instance of the `Gson` class that is expected to have custom type adapters registered for `CustomClass1`, `CustomClass2`, and `CustomClass3`.
- **Control Flow**:
    - Convert an instance of `CustomClass1` to JSON using the provided `Gson` instance and store the result in `json1`.
    - Assert that `json1` is equal to the string `"custom-adapter"`.
    - Convert an instance of `CustomClass2` to JSON using the provided `Gson` instance and store the result in `json2`.
    - Assert that `json2` is equal to the string `"custom-hierarchy-adapter"`.
    - Deserialize an empty JSON object into an instance of `CustomClass3` using the provided `Gson` instance and store the result in `customClass3`.
    - Assert that the `s` field of `customClass3` is equal to the string `"custom-instance"`.
- **Output**:
    - The method does not return any value, but it will throw an assertion error if any of the assertions fail.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.GsonTest`](#GsonTest)  (Base Class)



---
### TestTypeAdapter<!-- {{#class:com.google.gson.GsonTest.TestTypeAdapter}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `TestTypeAdapter` class is a private static final inner class that extends the `TypeAdapter` class from the Gson library, providing a basic implementation for serializing and deserializing JSON data. It overrides the `write` method to provide a test stub for writing JSON data and the `read` method to return null, serving as a placeholder for testing purposes.
- **Methods**:
    - [`com.google.gson.GsonTest.TestTypeAdapter.write`](#TestTypeAdapterwrite)
    - [`com.google.gson.GsonTest.TestTypeAdapter.read`](#TestTypeAdapterread)

**Methods**

---
#### TestTypeAdapter\.write<!-- {{#callable:com.google.gson.GsonTest.TestTypeAdapter.write}} -->
The `write` method is a stub intended to be overridden for writing a JSON representation of an object using a `JsonWriter`.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - `value`: An `Object` that represents the data to be written in JSON format.
- **Control Flow**:
    - The method is currently a stub and does not contain any implementation.
- **Output**:
    - The method does not return any value as it is a void method.
- **See also**: [`com.google.gson.GsonTest.TestTypeAdapter`](#GsonTest.TestTypeAdapter)  (Base Class)


---
#### TestTypeAdapter\.read<!-- {{#callable:com.google.gson.GsonTest.TestTypeAdapter.read}} -->
The `read` method in `TestTypeAdapter` returns `null` when called.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which JSON data is to be read.
- **Control Flow**:
    - The method is overridden from a superclass or interface.
    - The method immediately returns `null` without performing any operations.
- **Output**:
    - The method returns `null`.
- **See also**: [`com.google.gson.GsonTest.TestTypeAdapter`](#GsonTest.TestTypeAdapter)  (Base Class)



---
### IntegerAdapter<!-- {{#class:com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter}} -->
- **Description**: The `IntegerAdapter` class is a custom implementation of the `TypeAdapter` for the `Integer` type, designed primarily for testing purposes. It overrides the `read` method to skip the JSON value and return a constant integer value of 3, while the `write` method throws an `AssertionError`, indicating that writing is not required for the test. The `toString` method is overridden to return a custom string identifier for the adapter.
- **Methods**:
    - [`com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter.read`](#GsonTesttestFromJson_WrongResultType.IntegerAdapter.read)
    - [`com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter.write`](#GsonTesttestFromJson_WrongResultType.IntegerAdapter.write)
    - [`com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter.toString`](#GsonTesttestFromJson_WrongResultType.IntegerAdapter.toString)

**Methods**

---
#### IntegerAdapter\.read<!-- {{#callable:com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter.read}} -->
The `read` method skips the current JSON value in the `JsonReader` and returns the integer 3.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON value is read and skipped.
- **Control Flow**:
    - The method calls `in.skipValue()` to skip the current JSON value in the `JsonReader`.
    - The method then returns the integer 3.
- **Output**:
    - The method returns an `Integer` with the value 3.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
- **See also**: [`com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter`](#GsonTest.testFromJson_WrongResultType.IntegerAdapter)  (Base Class)


---
#### IntegerAdapter\.write<!-- {{#callable:com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter.write}} -->
The `write` method throws an `AssertionError` indicating it is not needed for the test.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object where the JSON output would be written.
    - `value`: An `Integer` value that would be written to the `JsonWriter`.
- **Control Flow**:
    - The method immediately throws an `AssertionError` with the message 'not needed for test'.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter`](#GsonTest.testFromJson_WrongResultType.IntegerAdapter)  (Base Class)


---
#### IntegerAdapter\.toString<!-- {{#callable:com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter.toString}} -->
The `toString` method returns a fixed string "custom-adapter".
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns the string "custom-adapter" without any conditions or iterations.
- **Output**:
    - A string literal "custom-adapter".
- **See also**: [`com.google.gson.GsonTest.testFromJson_WrongResultType.IntegerAdapter`](#GsonTest.testFromJson_WrongResultType.IntegerAdapter)  (Base Class)



---
### NullAdapter<!-- {{#class:com.google.gson.GsonTest.testFromJson_WrongResultType.NullAdapter}} -->
- **Description**: The `NullAdapter` class is a specialized implementation of the `TypeAdapter` class for handling JSON serialization and deserialization in the Gson library. It is designed to read JSON input and skip the value, returning `null` instead, and it throws an `AssertionError` when attempting to write a value, indicating that writing is not needed for its intended use case, which is primarily for testing purposes.
- **Methods**:
    - [`com.google.gson.GsonTest.testFromJson_WrongResultType.NullAdapter.read`](#GsonTesttestFromJson_WrongResultType.NullAdapter.read)
    - [`com.google.gson.GsonTest.testFromJson_WrongResultType.NullAdapter.write`](#GsonTesttestFromJson_WrongResultType.NullAdapter.write)

**Methods**

---
#### NullAdapter\.read<!-- {{#callable:com.google.gson.GsonTest.testFromJson_WrongResultType.NullAdapter.read}} -->
The `read` method skips the current JSON value in the `JsonReader` and returns `null`.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON value is to be read and skipped.
- **Control Flow**:
    - The method calls `in.skipValue()` to skip the current JSON value in the `JsonReader` object.
    - The method returns `null`.
- **Output**:
    - The method returns `null` after skipping the JSON value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.skipValue`](../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderskipValue)
- **See also**: [`com.google.gson.GsonTest.testFromJson_WrongResultType.NullAdapter`](#GsonTest.testFromJson_WrongResultType.NullAdapter)  (Base Class)


---
#### NullAdapter\.write<!-- {{#callable:com.google.gson.GsonTest.testFromJson_WrongResultType.NullAdapter.write}} -->
The `write` method throws an `AssertionError` indicating it is not needed for the test.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object where the JSON output would be written.
    - `value`: An `Object` that represents the value to be written to the JSON output.
- **Control Flow**:
    - The method immediately throws an `AssertionError` with the message 'not needed for test'.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.GsonTest.testFromJson_WrongResultType.NullAdapter`](#GsonTest.testFromJson_WrongResultType.NullAdapter)  (Base Class)



---
### DummyAdapter<!-- {{#class:com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter}} -->
- **Description**: The `DummyAdapter` class is a specialized implementation of the `TypeAdapter` class for `Number` types, primarily used for testing purposes. It contains a private integer field `number` that is used to differentiate instances of this adapter, and it overrides the `read` and `write` methods to throw `AssertionError`, indicating that these operations are not needed for the test scenarios. The `toString` method is overridden to provide a custom string representation that includes the adapter's number, which aids in debugging and assertion error messages.
- **Fields**:
    - `number`: `int` A private integer field used to identify the adapter instance.
- **Methods**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.DummyAdapter`](#GsonTesttestGetDelegateAdapter.DummyAdapter.DummyAdapter)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.read`](#GsonTesttestGetDelegateAdapter.DummyAdapter.read)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.write`](#GsonTesttestGetDelegateAdapter.DummyAdapter.write)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.toString`](#GsonTesttestGetDelegateAdapter.DummyAdapter.toString)

**Methods**

---
#### DummyAdapter\.DummyAdapter<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.DummyAdapter}} -->
The `DummyAdapter` constructor initializes a new instance of the `DummyAdapter` class with a specified integer value.
- **Inputs**:
    - `number`: An integer value used to initialize the `number` field of the `DummyAdapter` instance.
- **Control Flow**:
    - The constructor takes an integer parameter `number`.
    - It assigns the value of `number` to the instance variable `this.number`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `DummyAdapter` class.
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter`](#GsonTest.testGetDelegateAdapter.DummyAdapter)  (Base Class)


---
#### DummyAdapter\.read<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.read}} -->
The `read` method in the `TestTypeAdapter` class throws an `AssertionError` indicating it is not needed for the test.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which JSON data would be read.
- **Control Flow**:
    - The method immediately throws an `AssertionError` with the message 'not needed for test'.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter`](#GsonTest.testGetDelegateAdapter.DummyAdapter)  (Base Class)


---
#### DummyAdapter\.write<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.write}} -->
The `write` method throws an `AssertionError` indicating it is not needed for the test.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object where the JSON output would be written.
    - `value`: A `Number` object representing the value to be written to the JSON output.
- **Control Flow**:
    - The method immediately throws an `AssertionError` with the message 'not needed for test'.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter`](#GsonTest.testGetDelegateAdapter.DummyAdapter)  (Base Class)


---
#### DummyAdapter\.toString<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter.toString}} -->
The `toString` method returns a string representation of the `DummyAdapter` object, which includes the prefix 'adapter-' followed by the adapter's number.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method concatenates the string 'adapter-' with the `number` field of the `DummyAdapter` class and returns the resulting string.
- **Output**:
    - A string that represents the `DummyAdapter` object, formatted as 'adapter-' followed by the adapter's number.
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyAdapter`](#GsonTest.testGetDelegateAdapter.DummyAdapter)  (Base Class)



---
### WrappingAdapter<!-- {{#class:com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter}} -->
- **Modifiers**: ``
- **Description**: The `WrappingAdapter` class is a specialized implementation of the `TypeAdapter` class, designed to wrap another `TypeAdapter` instance and manage recursive calls during JSON serialization. It overrides the `write` method to handle potential infinite recursion by tracking the depth of nested calls and writing a placeholder value when necessary. The `read` method is not implemented as it is not required for the specific test scenario this class is used in.
- **Fields**:
    - `wrapped`: `TypeAdapter<?>` A final field holding the wrapped `TypeAdapter` instance.
    - `isFirstCall`: `boolean` A boolean flag used to track if the current call is the first in a potential recursive sequence.
- **Methods**:
    - [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter.WrappingAdapter`](#GsonTesttestGetAdapter_FutureAdapterConcurrency.WrappingAdapter.WrappingAdapter)
    - [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter.write`](#GsonTesttestGetAdapter_FutureAdapterConcurrency.WrappingAdapter.write)
    - [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter.read`](#GsonTesttestGetAdapter_FutureAdapterConcurrency.WrappingAdapter.read)

**Methods**

---
#### WrappingAdapter\.WrappingAdapter<!-- {{#callable:com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter.WrappingAdapter}} -->
The `WrappingAdapter` constructor initializes a new instance of the `WrappingAdapter` class by assigning a provided `TypeAdapter` to its `wrapped` field.
- **Modifiers**: ``
- **Inputs**:
    - `wrapped`: A `TypeAdapter<?>` object that is to be wrapped by the `WrappingAdapter`.
- **Control Flow**:
    - Assigns the provided `wrapped` `TypeAdapter` to the instance variable `this.wrapped`.
- **Output**:
    - There is no return value as this is a constructor.
- **See also**: [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter`](#GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter)  (Base Class)


---
#### WrappingAdapter\.write<!-- {{#callable:com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter.write}} -->
The [`write`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite) method serializes an object of type `T` to JSON using a `JsonWriter`, handling potential infinite recursion by tracking the depth of nested calls.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write JSON data.
    - [`value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): An object of type `T` to be serialized to JSON.
- **Control Flow**:
    - Check if `isFirstCall` is true, indicating the first call to this method.
    - If true, set `isFirstCall` to false, begin a JSON array, call `wrapped.write(out, null)`, end the JSON array, and reset `isFirstCall` to true.
    - If false, write the string "wrapped-nested" to the `JsonWriter`.
- **Output**:
    - The method does not return a value but writes JSON data to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.TypeAdapter.write`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter`](#GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter)  (Base Class)


---
#### WrappingAdapter\.read<!-- {{#callable:com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter.read}} -->
The `read` method throws an `AssertionError` indicating it is not needed for the test.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object that is intended to be used for reading JSON input.
- **Control Flow**:
    - The method immediately throws an `AssertionError` with the message 'not needed for this test'.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter`](#GsonTest.testGetAdapter_FutureAdapterConcurrency.WrappingAdapter)  (Base Class)



---
### DummyFactory<!-- {{#class:com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory}} -->
- **Description**: The `DummyFactory` class is a custom implementation of the `TypeAdapterFactory` interface, designed to provide a specific `TypeAdapter` instance, `DummyAdapter`, for use with the Gson library. It overrides the `create` method to return the `DummyAdapter` instance, and it also overrides the `equals` and `hashCode` methods to ensure proper equality checks and hash code generation based on the contained `DummyAdapter` instance.
- **Fields**:
    - `adapter`: `DummyAdapter` A final field that holds a reference to a `DummyAdapter` instance, which is used to create type adapters.
- **Methods**:
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.DummyFactory`](#GsonTesttestGetDelegateAdapter.DummyFactory.DummyFactory)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.create`](#GsonTesttestGetDelegateAdapter.DummyFactory.create)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](#GsonTesttestGetDelegateAdapter.DummyFactory.equals)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.hashCode`](#GsonTesttestGetDelegateAdapter.DummyFactory.hashCode)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### DummyFactory\.DummyFactory<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.DummyFactory}} -->
The `DummyFactory` constructor initializes a `DummyFactory` instance with a given `DummyAdapter`.
- **Modifiers**: `private`
- **Inputs**:
    - `adapter`: An instance of `DummyAdapter` that will be used to initialize the `DummyFactory`.
- **Control Flow**:
    - The constructor takes a `DummyAdapter` object as a parameter.
    - It assigns the provided `DummyAdapter` to the `adapter` field of the `DummyFactory` instance.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of `DummyFactory`.
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory`](#GsonTest.testGetDelegateAdapter.DummyFactory)  (Base Class)


---
#### DummyFactory\.create<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.create}} -->
The `create` method returns a pre-defined `TypeAdapter` instance for a given `Gson` and `TypeToken`.
- **Modifiers**: `public`, `<T>`, `@Override`
- **Inputs**:
    - `gson`: An instance of the `Gson` class, which is used for JSON serialization and deserialization.
    - `type`: A `TypeToken<T>` representing the type for which the `TypeAdapter` is being requested.
- **Control Flow**:
    - The method is annotated with `@SuppressWarnings("unchecked")` to suppress unchecked cast warnings.
    - The method returns the `adapter` field cast to `TypeAdapter<T>`.
- **Output**:
    - The method returns a `TypeAdapter<T>` instance, which is a pre-defined adapter for the specified type.
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory`](#GsonTest.testGetDelegateAdapter.DummyFactory)  (Base Class)


---
#### DummyFactory\.equals<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals}} -->
The [`equals`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectequals) method checks if the given object is an instance of `DummyFactory` and if its `adapter` field is equal to the current object's `adapter` field.
- **Modifiers**: `public`
- **Inputs**:
    - `obj`: The object to be compared with the current instance of `DummyFactory`.
- **Control Flow**:
    - Check if the input object `obj` is an instance of `DummyFactory`.
    - If true, cast `obj` to `DummyFactory` and compare its `adapter` field with the current instance's `adapter` field using the [`equals`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectequals) method.
    - Return the result of the comparison.
- **Output**:
    - A boolean value indicating whether the input object is equal to the current instance of `DummyFactory`.
- **Functions called**:
    - [`com.google.gson.JsonObject.equals`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectequals)
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory`](#GsonTest.testGetDelegateAdapter.DummyFactory)  (Base Class)


---
#### DummyFactory\.hashCode<!-- {{#callable:com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.hashCode}} -->
The `hashCode` method returns the hash code of the `adapter` object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly calls and returns the result of the `hashCode` method on the `adapter` object.
- **Output**:
    - An integer representing the hash code of the `adapter` object.
- **See also**: [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory`](#GsonTest.testGetDelegateAdapter.DummyFactory)  (Base Class)



---
### CustomClass1<!-- {{#class:com.google.gson.GsonTest.CustomClass1}} -->
- **Modifiers**: `private`, `static`
- **Description**: CustomClass1 is a private static inner class within the GsonTest class, primarily serving as a placeholder or a simple data structure for testing purposes within the Gson library's unit tests.


---
### CustomClass2<!-- {{#class:com.google.gson.GsonTest.CustomClass2}} -->
- **Modifiers**: `private`, `static`
- **Description**: `CustomClass2` is a private static inner class within the `GsonTest` class, primarily serving as a placeholder or a simple data structure without any fields or methods defined.


---
### CustomClass3<!-- {{#class:com.google.gson.GsonTest.CustomClass3}} -->
- **Modifiers**: `private`, `static`
- **Description**: CustomClass3 is a private static class designed to be used internally within the GsonTest class, providing a simple structure with a single string field. It includes a constructor that accepts a string parameter to initialize the field, as well as a no-argument constructor that defaults the field to a predefined constant value, which is useful for serialization and deserialization processes, particularly with Gson.
- **Fields**:
    - `NO_ARG_CONSTRUCTOR_VALUE`: `String` A static final string constant used as the default value for the no-argument constructor.
    - `s`: `String` A final string field that holds the value passed to the constructor or the default value if the no-argument constructor is used.
- **Methods**:
    - [`com.google.gson.GsonTest.CustomClass3.CustomClass3`](#CustomClass3CustomClass3)
    - [`com.google.gson.GsonTest.CustomClass3.CustomClass3`](#CustomClass3CustomClass3)

**Methods**

---
#### CustomClass3\.CustomClass3<!-- {{#callable:com.google.gson.GsonTest.CustomClass3.CustomClass3}} -->
The constructor `CustomClass3(String s)` initializes a `CustomClass3` object with a specified string value.
- **Modifiers**: `public`
- **Inputs**:
    - `s`: A string value used to initialize the `s` field of the `CustomClass3` object.
- **Control Flow**:
    - The constructor assigns the input string `s` to the instance variable `this.s`.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of the `CustomClass3` class.
- **See also**: [`com.google.gson.GsonTest.CustomClass3`](#GsonTest.CustomClass3)  (Base Class)


---
#### CustomClass3\.CustomClass3<!-- {{#callable:com.google.gson.GsonTest.CustomClass3.CustomClass3}} -->
The `CustomClass3` constructor initializes an instance with a default string value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor is called without any arguments.
    - It internally calls another constructor of the same class with a constant string `NO_ARG_CONSTRUCTOR_VALUE`.
- **Output**:
    - An instance of `CustomClass3` initialized with a default string value.
- **See also**: [`com.google.gson.GsonTest.CustomClass3`](#GsonTest.CustomClass3)  (Base Class)



