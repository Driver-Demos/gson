# Purpose
The `DefaultTypeAdaptersTest` Java file is a comprehensive suite of functional tests designed to validate the serialization and deserialization capabilities of the Gson library for various common Java classes. This file is part of the `com.google.gson.functional` package and leverages the JUnit testing framework to ensure that Gson correctly handles data types such as `Class`, `URL`, `URI`, `UUID`, `Locale`, `BigDecimal`, `BigInteger`, `Date`, `Calendar`, `JsonElement`, and collections like `Set`, `BitSet`, `TreeSet`, `Properties`, `StringBuilder`, and `StringBuffer`. The tests cover both default behavior and scenarios where custom type adapters are registered, ensuring that Gson's flexibility and extensibility are thoroughly examined.

The file is structured to include setup and teardown methods that configure the environment for consistent test results, such as setting default time zones and locales. Each test method focuses on a specific data type or functionality, using assertions to verify that the serialized JSON output matches expected values and that deserialized objects retain their original properties. The file also includes custom type adapters, such as `MyClassTypeAdapter` and [`NumberAsStringAdapter`](#NumberAsStringAdapterNumberAsStringAdapter), to demonstrate how Gson can be extended to handle types not natively supported. This test suite is crucial for maintaining the reliability and robustness of the Gson library, ensuring it meets the needs of developers working with diverse data types in JSON serialization and deserialization tasks.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.common.truth.Truth.assertWithMessage`
- `org.junit.Assert.assertThrows`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonArray`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonNull`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.TypeAdapter`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.Constructor`
- `java.lang.reflect.Type`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `java.net.InetAddress`
- `java.net.URI`
- `java.net.URL`
- `java.text.DateFormat`
- `java.util.ArrayList`
- `java.util.Arrays`
- `java.util.BitSet`
- `java.util.Calendar`
- `java.util.Date`
- `java.util.GregorianCalendar`
- `java.util.HashSet`
- `java.util.List`
- `java.util.Locale`
- `java.util.Properties`
- `java.util.Set`
- `java.util.TimeZone`
- `java.util.TreeSet`
- `java.util.UUID`
- `org.junit.After`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### DefaultTypeAdaptersTest<!-- {{#class:com.google.gson.functional.DefaultTypeAdaptersTest}} -->
- **Modifiers**: `public`
- **Description**: The `DefaultTypeAdaptersTest` class is a comprehensive suite of unit tests designed to validate the serialization and deserialization capabilities of the Gson library for various data types, including primitive types, collections, and complex objects like URLs, URIs, and Dates. It ensures that Gson's default type adapters handle these types correctly, and it also tests custom type adapters for specific classes like `Class` and `BigDecimal`. The class sets up a controlled environment by adjusting the default `TimeZone` and `Locale` before each test and restoring them afterward, ensuring consistent test results.
- **Fields**:
    - `gson`: `Gson` An instance of the Gson class used for JSON serialization and deserialization.
    - `oldTimeZone`: `TimeZone` Stores the original default TimeZone to restore after tests.
    - `oldLocale`: `Locale` Stores the original default Locale to restore after tests.
- **Methods**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.setUp`](#DefaultTypeAdaptersTestsetUp)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.tearDown`](#DefaultTypeAdaptersTesttearDown)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testClassSerialization`](#DefaultTypeAdaptersTesttestClassSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testClassDeserialization`](#DefaultTypeAdaptersTesttestClassDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUrlSerialization`](#DefaultTypeAdaptersTesttestUrlSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUrlDeserialization`](#DefaultTypeAdaptersTesttestUrlDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUrlNullSerialization`](#DefaultTypeAdaptersTesttestUrlNullSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUrlNullDeserialization`](#DefaultTypeAdaptersTesttestUrlNullDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUriSerialization`](#DefaultTypeAdaptersTesttestUriSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUriDeserialization`](#DefaultTypeAdaptersTesttestUriDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerialization`](#DefaultTypeAdaptersTesttestNullSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerializationAndDeserialization`](#DefaultTypeAdaptersTesttestNullSerializationAndDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerializationAndDeserialization`](#DefaultTypeAdaptersTesttestNullSerializationAndDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUuidSerialization`](#DefaultTypeAdaptersTesttestUuidSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testUuidDeserialization`](#DefaultTypeAdaptersTesttestUuidDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleSerializationWithLanguage`](#DefaultTypeAdaptersTesttestLocaleSerializationWithLanguage)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleDeserializationWithLanguage`](#DefaultTypeAdaptersTesttestLocaleDeserializationWithLanguage)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleSerializationWithLanguageCountry`](#DefaultTypeAdaptersTesttestLocaleSerializationWithLanguageCountry)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleDeserializationWithLanguageCountry`](#DefaultTypeAdaptersTesttestLocaleDeserializationWithLanguageCountry)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleSerializationWithLanguageCountryVariant`](#DefaultTypeAdaptersTesttestLocaleSerializationWithLanguageCountryVariant)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleDeserializationWithLanguageCountryVariant`](#DefaultTypeAdaptersTesttestLocaleDeserializationWithLanguageCountryVariant)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testBigDecimalFieldSerialization`](#DefaultTypeAdaptersTesttestBigDecimalFieldSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testBigDecimalFieldDeserialization`](#DefaultTypeAdaptersTesttestBigDecimalFieldDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testBadValueForBigDecimalDeserialization`](#DefaultTypeAdaptersTesttestBadValueForBigDecimalDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testBigIntegerFieldSerialization`](#DefaultTypeAdaptersTesttestBigIntegerFieldSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testBigIntegerFieldDeserialization`](#DefaultTypeAdaptersTesttestBigIntegerFieldDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testOverrideBigIntegerTypeAdapter`](#DefaultTypeAdaptersTesttestOverrideBigIntegerTypeAdapter)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testOverrideBigDecimalTypeAdapter`](#DefaultTypeAdaptersTesttestOverrideBigDecimalTypeAdapter)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testSetSerialization`](#DefaultTypeAdaptersTesttestSetSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testBitSetSerialization`](#DefaultTypeAdaptersTesttestBitSetSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testBitSetDeserialization`](#DefaultTypeAdaptersTesttestBitSetDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateSerialization`](#DefaultTypeAdaptersTesttestDefaultDateSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateDeserialization`](#DefaultTypeAdaptersTesttestDefaultDateDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsDate`](#DefaultTypeAdaptersTestassertEqualsDate)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsTime`](#DefaultTypeAdaptersTestassertEqualsTime)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateSerializationUsingBuilder`](#DefaultTypeAdaptersTesttestDefaultDateSerializationUsingBuilder)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateDeserializationUsingBuilder`](#DefaultTypeAdaptersTesttestDefaultDateDeserializationUsingBuilder)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultCalendarSerialization`](#DefaultTypeAdaptersTesttestDefaultCalendarSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultCalendarDeserialization`](#DefaultTypeAdaptersTesttestDefaultCalendarDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultGregorianCalendarSerialization`](#DefaultTypeAdaptersTesttestDefaultGregorianCalendarSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultGregorianCalendarDeserialization`](#DefaultTypeAdaptersTesttestDefaultGregorianCalendarDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithStyle`](#DefaultTypeAdaptersTesttestDateSerializationWithStyle)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithDateStyle`](#DefaultTypeAdaptersTesttestDateSerializationWithDateStyle)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDateStyleOverwritesPattern`](#DefaultTypeAdaptersTesttestDateStyleOverwritesPattern)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithPattern`](#DefaultTypeAdaptersTesttestDateSerializationWithPattern)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDateDeserializationWithPattern`](#DefaultTypeAdaptersTesttestDateDeserializationWithPattern)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithPatternNotOverridenByTypeAdapter`](#DefaultTypeAdaptersTesttestDateSerializationWithPatternNotOverridenByTypeAdapter)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationInCollection`](#DefaultTypeAdaptersTesttestDateSerializationInCollection)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonPrimitiveSerialization`](#DefaultTypeAdaptersTesttestJsonPrimitiveSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonPrimitiveDeserialization`](#DefaultTypeAdaptersTesttestJsonPrimitiveDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonNullSerialization`](#DefaultTypeAdaptersTesttestJsonNullSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testNullJsonElementSerialization`](#DefaultTypeAdaptersTesttestNullJsonElementSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonArraySerialization`](#DefaultTypeAdaptersTesttestJsonArraySerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonArrayDeserialization`](#DefaultTypeAdaptersTesttestJsonArrayDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonObjectSerialization`](#DefaultTypeAdaptersTesttestJsonObjectSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonObjectDeserialization`](#DefaultTypeAdaptersTesttestJsonObjectDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonNullDeserialization`](#DefaultTypeAdaptersTesttestJsonNullDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testJsonElementTypeMismatch`](#DefaultTypeAdaptersTesttestJsonElementTypeMismatch)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testPropertiesSerialization`](#DefaultTypeAdaptersTesttestPropertiesSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testPropertiesDeserialization`](#DefaultTypeAdaptersTesttestPropertiesDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testTreeSetSerialization`](#DefaultTypeAdaptersTesttestTreeSetSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testTreeSetDeserialization`](#DefaultTypeAdaptersTesttestTreeSetDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testStringBuilderSerialization`](#DefaultTypeAdaptersTesttestStringBuilderSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testStringBuilderDeserialization`](#DefaultTypeAdaptersTesttestStringBuilderDeserialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testStringBufferSerialization`](#DefaultTypeAdaptersTesttestStringBufferSerialization)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testStringBufferDeserialization`](#DefaultTypeAdaptersTesttestStringBufferDeserialization)

**Methods**

---
#### DefaultTypeAdaptersTest\.setUp<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.setUp}} -->
Sets up the test environment by configuring the default time zone and locale.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Stores the current default time zone in `oldTimeZone`.
    - Sets the default time zone to 'America/Los_Angeles'.
    - Stores the current default locale in `oldLocale`.
    - Sets the default locale to `Locale.US`.
    - Initializes the `gson` instance with a new `Gson` object.
- **Output**:
    - No output is returned as this method is a setup method for tests.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.tearDown<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.tearDown}} -->
Restores the previous default `TimeZone` and `Locale` settings after tests.
- **Inputs**: None
- **Control Flow**:
    - Sets the default `TimeZone` back to the value stored in `oldTimeZone`.
    - Sets the default `Locale` back to the value stored in `oldLocale`.
- **Output**:
    - This method does not return any value; it performs cleanup operations.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testClassSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testClassSerialization}} -->
Tests the serialization of `Class` objects using Gson.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `gson`: An instance of `Gson` used for serialization.
    - `String.class`: The `Class` object representing the `String` class.
- **Control Flow**:
    - The method first attempts to serialize `String.class` using the default `Gson` instance, expecting an `UnsupportedOperationException` to be thrown.
    - It asserts that the exception message indicates that a type adapter for `Class` was not registered.
    - Next, it creates a new `Gson` instance with a custom type adapter for `Class` and serializes `String.class` again.
    - Finally, it asserts that the serialized output matches the expected JSON representation of the `String` class.
- **Output**:
    - The method does not return a value but asserts that the serialization of `String.class` produces the expected JSON output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testClassDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testClassDeserialization}} -->
Tests the deserialization of Java `Class` objects using Gson.
- **Inputs**: None
- **Control Flow**:
    - The method begins by asserting that deserializing a string representation of a class ("String.class") without a type adapter throws an `UnsupportedOperationException`.
    - It checks that the exception message indicates the need for a type adapter for `java.lang.Class`.
    - Next, it creates a new `Gson` instance with a custom type adapter (`MyClassTypeAdapter`) registered for `Class.class`.
    - Finally, it asserts that deserializing the string "java.lang.String" correctly returns a `Class` object that is assignable to `String.class`.
- **Output**:
    - The method does not return a value; it performs assertions to validate the behavior of the Gson deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUrlSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUrlSerialization}} -->
Tests the serialization of a `URL` object to its JSON representation.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A `String` representing a URL is defined.
    - A `URL` object is created using the defined string.
    - The `gson.toJson()` method is called to serialize the `URL` object to JSON.
    - The result is compared to the expected JSON string using an assertion.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON representation of the `URL` object matches the expected string.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUrlDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUrlDeserialization}} -->
Tests the deserialization of `URL` objects from JSON strings.
- **Inputs**:
    - `urlValue`: A string representing the expected URL value, which is 'http://google.com/'.
    - `json`: A JSON string representation of the URL, which includes escaped characters.
- **Control Flow**:
    - The method initializes a string `urlValue` with the expected URL.
    - It then defines a JSON string `json` that represents the URL with escaped characters.
    - The method uses `gson.fromJson` to deserialize the `json` string into a `URL` object `target1`.
    - It asserts that the external form of `target1` matches `urlValue`.
    - Next, it deserializes `urlValue` directly into another `URL` object `target2` using `gson.fromJson`.
    - Finally, it asserts that the external form of `target2` also matches `urlValue`.
- **Output**:
    - The method does not return a value but asserts that the deserialized `URL` objects match the expected URL string.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUrlNullSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUrlNullSerialization}} -->
Tests the serialization of a class containing a null URL field.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates an instance of `ClassWithUrlField`, which contains a URL field initialized to null.
    - Uses the `gson` object to serialize the `target` instance to JSON.
    - Asserts that the resulting JSON string is equal to an empty JSON object '{}'.
- **Output**:
    - The method outputs a JSON string representation of the `target` object, which is expected to be '{}', indicating that the URL field is null.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUrlNullDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUrlNullDeserialization}} -->
Tests the deserialization of a JSON string into a class with a URL field, ensuring that the URL field is null when the JSON is empty.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing an empty object is defined as '{}'.
    - The `gson.fromJson` method is called to deserialize the JSON string into an instance of `ClassWithUrlField`.
    - An assertion is made to check that the `url` field of the deserialized object is null.
- **Output**:
    - The method does not return a value; it asserts that the `url` field of the deserialized object is null.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUriSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUriSerialization}} -->
Tests the serialization of a `URI` object to its JSON representation.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A `String` representing a URI is defined.
    - A `URI` object is created using the defined string.
    - The `gson.toJson()` method is called to serialize the `URI` object to JSON.
    - The result is asserted to be equal to the expected JSON string representation of the URI.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON representation of the `URI` matches the expected output.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUriDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUriDeserialization}} -->
Tests the deserialization of a `URI` from a JSON string.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A string `uriValue` is initialized with the value 'http://google.com/'.
    - A JSON string `json` is created by enclosing `uriValue` in double quotes.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `URI` object named `target`.
    - The `toASCIIString` method of the `target` URI is called to get its string representation.
    - An assertion is made to check if the ASCII string representation of `target` equals the original `uriValue`.
- **Output**:
    - The method does not return a value but asserts that the deserialized `URI` matches the original string.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testNullSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerialization}} -->
Tests the serialization and deserialization of null values for various classes using Gson.
- **Inputs**: None
- **Control Flow**:
    - Calls the [`testNullSerializationAndDeserialization`](#DefaultTypeAdaptersTesttestNullSerializationAndDeserialization) method for a variety of classes including primitive wrappers, collections, and other common types.
    - Each call checks if the Gson library correctly handles null values for the specified class.
- **Output**:
    - No direct output; the method performs assertions to verify that the serialization and deserialization of null values are handled correctly.
- **Functions called**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerializationAndDeserialization`](#DefaultTypeAdaptersTesttestNullSerializationAndDeserialization)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testNullSerializationAndDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerializationAndDeserialization}} -->
Tests the serialization and deserialization of null values for a specified class type.
- **Modifiers**: `private`
- **Inputs**:
    - `c`: A `Class<?>` object representing the type to be tested for null serialization and deserialization.
- **Control Flow**:
    - Calls the overloaded method `testNullSerializationAndDeserialization(Gson gson, Class<?> c)` with the `gson` instance and the provided class type `c`.
- **Output**:
    - No direct output; the method performs assertions to verify that serializing and deserializing null values for the specified class type behaves as expected.
- **Functions called**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerializationAndDeserialization`](#DefaultTypeAdaptersTesttestNullSerializationAndDeserialization)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testNullSerializationAndDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testNullSerializationAndDeserialization}} -->
Tests the serialization and deserialization of null values using Gson.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON serialization and deserialization.
    - `c`: A `Class<?>` object representing the type to be serialized or deserialized.
- **Control Flow**:
    - The method first serializes a null value to JSON using `gson.toJson(null, c)` and asserts that the result is the string 'null'.
    - Then, it deserializes the JSON string 'null' back to an object of type `c` using `gson.fromJson('null', c)` and asserts that the result is null.
- **Output**:
    - The method does not return a value; it performs assertions to verify that the serialization and deserialization of null values behave as expected.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUuidSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUuidSerialization}} -->
Tests the serialization of a `UUID` object to its JSON representation.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A `String` representing a UUID is defined.
    - The `String` is converted to a `UUID` object using `UUID.fromString()`.
    - The `UUID` object is serialized to JSON using `gson.toJson()`.
    - The resulting JSON string is compared to the expected JSON representation of the UUID.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON string matches the expected format.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testUuidDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testUuidDeserialization}} -->
Tests the deserialization of a UUID from a JSON string.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**:
    - `uuidValue`: A string representation of a UUID to be deserialized.
    - `json`: A JSON string that contains the UUID value, formatted as a quoted string.
- **Control Flow**:
    - A UUID string is defined and formatted as a JSON string.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `UUID` object.
    - An assertion is made to check if the deserialized UUID matches the original UUID string.
- **Output**:
    - The method does not return a value but asserts that the deserialized UUID matches the expected UUID string.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testLocaleSerializationWithLanguage<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleSerializationWithLanguage}} -->
Tests the serialization of a `Locale` object with a specified language.
- **Inputs**: None
- **Control Flow**:
    - A `Locale` object is created with the language code 'en'.
    - The `gson.toJson()` method is called to serialize the `Locale` object to JSON.
    - The result is compared to the expected JSON string '"en"' using an assertion.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `Locale` object is equal to the expected string '"en"'.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testLocaleDeserializationWithLanguage<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleDeserializationWithLanguage}} -->
Tests the deserialization of a JSON string representing a language code into a `Locale` object.
- **Inputs**:
    - `json`: A JSON string representing a language code, specifically '"en"'.
- **Control Flow**:
    - The method begins by defining a JSON string that represents the language code for English.
    - It then uses the `gson` object to deserialize the JSON string into a `Locale` object.
    - Finally, it asserts that the language of the deserialized `Locale` object is equal to 'en'.
- **Output**:
    - The method does not return a value; it asserts that the language of the deserialized `Locale` is 'en'.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testLocaleSerializationWithLanguageCountry<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleSerializationWithLanguageCountry}} -->
Tests the serialization of a `Locale` object representing Canadian French.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `Locale` object for Canadian French using `Locale.CANADA_FRENCH`.
    - Serializes the `Locale` object to JSON using `gson.toJson()`.
    - Asserts that the serialized JSON string is equal to the expected value "fr_CA".
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `Locale` object is correct.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testLocaleDeserializationWithLanguageCountry<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleDeserializationWithLanguageCountry}} -->
Tests the deserialization of a `Locale` object from a JSON string representing a language and country.
- **Inputs**:
    - `json`: A JSON string representing a locale in the format 'language_country', specifically "fr_CA".
- **Control Flow**:
    - The method begins by defining a JSON string that represents the locale for Canada French.
    - It then uses the `gson` object to deserialize the JSON string into a `Locale` object.
    - Finally, it asserts that the deserialized `Locale` object is equal to `Locale.CANADA_FRENCH`.
- **Output**:
    - The method does not return a value but asserts that the deserialized `Locale` object matches the expected `Locale.CANADA_FRENCH`.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testLocaleSerializationWithLanguageCountryVariant<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleSerializationWithLanguageCountryVariant}} -->
Tests the serialization of a `Locale` object with language, country, and variant.
- **Inputs**:
    - `target`: A `Locale` object initialized with language 'de', country 'DE', and variant 'EURO'.
- **Control Flow**:
    - Creates a `Locale` object with the specified language, country, and variant.
    - Serializes the `Locale` object to JSON format using the `gson` instance.
    - Asserts that the resulting JSON string matches the expected format for the `Locale`.
- **Output**:
    - A JSON string representation of the `Locale` object, expected to be '"de_DE_EURO"'.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testLocaleDeserializationWithLanguageCountryVariant<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testLocaleDeserializationWithLanguageCountryVariant}} -->
Tests the deserialization of a `Locale` object from a JSON string containing language, country, and variant.
- **Inputs**:
    - `json`: A JSON string representing a `Locale`, specifically formatted as "language_country_variant".
- **Control Flow**:
    - The method initializes a JSON string representing a `Locale` with language 'de', country 'DE', and variant 'EURO'.
    - It uses the `gson.fromJson` method to deserialize the JSON string into a `Locale` object.
    - Assertions are made to verify that the deserialized `Locale` object has the expected language, country, and variant values.
- **Output**:
    - The method does not return a value but asserts that the deserialized `Locale` object has the correct language, country, and variant.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testBigDecimalFieldSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testBigDecimalFieldSerialization}} -->
Tests the serialization of a `BigDecimal` field in a class.
- **Modifiers**: `public`, `Test`
- **Inputs**:
    - `target`: An instance of `ClassWithBigDecimal` initialized with a string representation of a `BigDecimal`.
- **Control Flow**:
    - Creates an instance of `ClassWithBigDecimal` with a specific value.
    - Serializes the instance to JSON using `gson.toJson()`.
    - Extracts the actual `BigDecimal` value from the JSON string.
    - Asserts that the extracted value matches the original `BigDecimal` value of the instance.
- **Output**:
    - The method does not return a value; it asserts that the serialized value matches the expected `BigDecimal`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testBigDecimalFieldDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testBigDecimalFieldDeserialization}} -->
Tests the deserialization of a `BigDecimal` field from JSON.
- **Inputs**:
    - `expected`: An instance of `ClassWithBigDecimal` that contains the expected value to be deserialized.
    - `json`: A JSON string representation of the `ClassWithBigDecimal` object.
    - `actual`: An instance of `ClassWithBigDecimal` that is created by deserializing the JSON string.
- **Control Flow**:
    - Creates an expected instance of `ClassWithBigDecimal` with a specific value.
    - Retrieves the expected JSON representation of the `expected` instance.
    - Deserializes the JSON string into an `actual` instance of `ClassWithBigDecimal` using `gson.fromJson`.
    - Asserts that the value of the `actual` instance is equal to the value of the `expected` instance.
- **Output**:
    - The method does not return a value but asserts that the deserialized `actual` object's value matches the expected value.
- **Functions called**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal.getExpectedJson`](#ClassWithBigDecimalgetExpectedJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testBadValueForBigDecimalDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testBadValueForBigDecimalDeserialization}} -->
Tests that a `JsonParseException` is thrown when attempting to deserialize a malformed BigDecimal.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check if a `JsonParseException` is thrown.
    - It attempts to deserialize a JSON string with an invalid BigDecimal format.
- **Output**:
    - The method does not return a value; it asserts that an exception is thrown during the deserialization process.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testBigIntegerFieldSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testBigIntegerFieldSerialization}} -->
Tests the serialization of a `ClassWithBigInteger` object to JSON.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `target`: An instance of `ClassWithBigInteger` initialized with a large `BigInteger` value.
- **Control Flow**:
    - Creates an instance of `ClassWithBigInteger` with a specific large integer value.
    - Serializes the `target` object to a JSON string using the `gson` library.
    - Asserts that the serialized JSON string matches the expected JSON representation of the `target` object.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON matches the expected format.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testBigIntegerFieldDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testBigIntegerFieldDeserialization}} -->
Tests the deserialization of a `BigInteger` field from JSON.
- **Inputs**:
    - `expected`: An instance of `ClassWithBigInteger` that contains the expected value.
    - `json`: A JSON string representation of the expected `ClassWithBigInteger` instance.
    - `actual`: An instance of `ClassWithBigInteger` created by deserializing the JSON string.
- **Control Flow**:
    - Creates an instance of `ClassWithBigInteger` with a predefined value to serve as the expected result.
    - Retrieves the expected JSON representation of the `expected` instance.
    - Deserializes the JSON string into an actual `ClassWithBigInteger` instance using `gson.fromJson`.
    - Asserts that the value of the deserialized instance matches the expected value using `assertThat`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized object's value matches the expected value.
- **Functions called**:
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](InheritanceTest.java.driver.md#ClassWithSubInterfacesOfCollectiongetExpectedJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testOverrideBigIntegerTypeAdapter<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testOverrideBigIntegerTypeAdapter}} -->
Tests the serialization and deserialization of `BigInteger` using a custom type adapter.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates a `Gson` instance with a custom type adapter for `BigInteger` that converts it to and from a string.
    - Serializes a `BigInteger` instance with the value of 123 to JSON format and asserts that the output is a string representation of the number.
    - Deserializes a JSON string representation of a `BigInteger` back to a `BigInteger` instance and asserts that it matches the expected value.
- **Output**:
    - The method does not return a value but asserts that the serialization and deserialization processes work correctly.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testOverrideBigDecimalTypeAdapter<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testOverrideBigDecimalTypeAdapter}} -->
Tests the serialization and deserialization of `BigDecimal` using a custom type adapter.
- **Inputs**:
    - `gson`: An instance of `Gson` configured with a custom type adapter for `BigDecimal`.
- **Control Flow**:
    - Creates a `Gson` instance with a registered type adapter for `BigDecimal` that converts it to and from a string.
    - Serializes a `BigDecimal` instance to JSON and asserts that the output is a string representation.
    - Deserializes a JSON string back to a `BigDecimal` and asserts that the result matches the original `BigDecimal`.
- **Output**:
    - The method does not return a value; it asserts that the serialization and deserialization processes work as expected.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testSetSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testSetSerialization}} -->
Tests the serialization of a `HashSet` using the `Gson` library.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `gson`: An instance of `Gson` used for converting Java objects to JSON.
    - `s`: A `HashSet<String>` containing a single string element 'blah'.
    - `json`: A string variable to hold the JSON representation of the `HashSet`.
- **Control Flow**:
    - Creates a new instance of `Gson`.
    - Initializes a `HashSet<String>` and adds the string 'blah' to it.
    - Serializes the `HashSet` to JSON using `gson.toJson(s)` and asserts that the output matches the expected JSON format.
    - Serializes the `HashSet` again using `gson.toJson(s, Set.class)` and asserts that the output matches the expected JSON format.
- **Output**:
    - The method does not return a value but asserts that the JSON representation of the `HashSet` is equal to the expected string '["blah"]'.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testBitSetSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testBitSetSerialization}} -->
Tests the serialization of a `BitSet` object to JSON format.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates an instance of `Gson` for JSON serialization.
    - Initializes a `BitSet` and sets specific bits (1, 3 to 6, and 9).
    - Serializes the `BitSet` to a JSON string using `gson.toJson(bits)`.
    - Asserts that the resulting JSON string matches the expected output.
- **Output**:
    - The method does not return a value but asserts that the serialized JSON string of the `BitSet` matches the expected format '[0,1,0,1,1,1,0,0,0,1]'.
- **Functions called**:
    - [`com.google.gson.JsonArray.set`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testBitSetDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testBitSetDeserialization}} -->
Tests the deserialization of `BitSet` objects from various JSON formats.
- **Inputs**:
    - `none`: This method does not take any input parameters.
- **Control Flow**:
    - Creates an expected `BitSet` instance and sets specific bits.
    - Serializes the `BitSet` to JSON and deserializes it back to verify equality.
    - Tests deserialization from various JSON representations of `BitSet`.
    - Asserts that deserialization from invalid JSON formats throws `JsonSyntaxException` with appropriate messages.
- **Output**:
    - The method does not return a value but asserts conditions to validate the correctness of `BitSet` deserialization.
- **Functions called**:
    - [`com.google.gson.JsonArray.set`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultDateSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateSerialization}} -->
Tests the default serialization of a `Date` object to JSON format.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a new `Date` object initialized to a specific timestamp (1315806903103L).
    - Serializes the `Date` object to a JSON string using the `gson` instance.
    - Asserts that the resulting JSON string matches the expected date format using a regex pattern.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `Date` matches the expected format.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.reflect.TypeToken.matches`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenmatches)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultDateDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateDeserialization}} -->
Tests the deserialization of a date string into a `Date` object.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**:
    - `json`: A string representation of a date in the format 'Dec 13, 2009 07:18:02 AM'.
- **Control Flow**:
    - The method initializes a string `json` with a date representation.
    - It uses the `gson.fromJson` method to convert the JSON string into a `Date` object.
    - The method then calls [`assertEqualsDate`](#DefaultTypeAdaptersTestassertEqualsDate) to verify the year, month, and day of the extracted date.
    - It also calls [`assertEqualsTime`](#DefaultTypeAdaptersTestassertEqualsTime) to verify the hour, minute, and second of the extracted date.
- **Output**:
    - The method does not return a value but asserts that the deserialized `Date` object matches the expected date and time.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsDate`](#DefaultTypeAdaptersTestassertEqualsDate)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsTime`](#DefaultTypeAdaptersTestassertEqualsTime)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.assertEqualsDate<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsDate}} -->
Asserts that a `Date` object matches the specified year, month, and day.
- **Inputs**:
    - `date`: A `Date` object that is to be compared against the specified year, month, and day.
    - `year`: An integer representing the expected year.
    - `month`: An integer representing the expected month (0-based, where January is 0).
    - `day`: An integer representing the expected day of the month.
- **Control Flow**:
    - The method retrieves the year from the `date` object using `getYear()` and compares it to `year - 1900`.
    - It retrieves the month from the `date` object using `getMonth()` and compares it to `month`.
    - It retrieves the day from the `date` object using `getDate()` and compares it to `day`.
- **Output**:
    - The method does not return a value; it throws an assertion error if any of the comparisons fail.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.assertEqualsTime<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.assertEqualsTime}} -->
Asserts that the hours, minutes, and seconds of a given `Date` object match the expected values.
- **Inputs**:
    - `date`: A `Date` object whose time components (hours, minutes, seconds) are to be validated.
    - `hours`: An integer representing the expected hour value.
    - `minutes`: An integer representing the expected minute value.
    - `seconds`: An integer representing the expected second value.
- **Control Flow**:
    - The method retrieves the hours from the `date` using `date.getHours()` and compares it to the `hours` parameter.
    - It retrieves the minutes from the `date` using `date.getMinutes()` and compares it to the `minutes` parameter.
    - It retrieves the seconds from the `date` using `date.getSeconds()` and compares it to the `seconds` parameter.
- **Output**:
    - The method does not return a value; it throws an assertion error if any of the time components do not match the expected values.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultDateSerializationUsingBuilder<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateSerializationUsingBuilder}} -->
Tests the default serialization of a `Date` object using a `GsonBuilder`.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `gson`: An instance of `Gson` created using `GsonBuilder`.
    - `now`: A `Date` object initialized to a specific timestamp.
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder`.
    - A `Date` object is instantiated with a specific timestamp.
    - The `Date` object is serialized to JSON format using `gson.toJson(now)`.
    - The resulting JSON string is validated against a regex pattern to ensure correct formatting.
- **Output**:
    - The method does not return a value but asserts that the JSON representation of the `Date` object matches the expected format.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.reflect.TypeToken.matches`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenmatches)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultDateDeserializationUsingBuilder<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultDateDeserializationUsingBuilder}} -->
Tests the deserialization of a `Date` object using Gson's builder.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder`.
    - A `Date` object representing a specific timestamp is instantiated.
    - The `Date` object is serialized to a JSON string using `gson.toJson()`.
    - The JSON string is deserialized back into a `Date` object using `gson.fromJson()`.
    - An assertion is made to check if the deserialized `Date` object matches the original `Date` object.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `Date` matches the original.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultCalendarSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultCalendarSerialization}} -->
Tests the serialization of the default `Calendar` instance to JSON.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `Gson` using `GsonBuilder`.
    - Serializes the current instance of `Calendar` to a JSON string.
    - Asserts that the resulting JSON string contains keys for 'year', 'month', 'dayOfMonth', 'hourOfDay', 'minute', and 'second'.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `Calendar` instance contains specific time-related fields.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultCalendarDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultCalendarDeserialization}} -->
Tests the deserialization of a JSON string into a `Calendar` object.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a `Gson` instance using `GsonBuilder`.
    - Defines a JSON string representing a date and time.
    - Deserializes the JSON string into a `Calendar` object using `gson.fromJson`.
    - Asserts that the year, month, day, hour, minute, and second of the deserialized `Calendar` object match the expected values.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `Calendar` object has the expected date and time values.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultGregorianCalendarSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultGregorianCalendarSerialization}} -->
Tests the serialization of a `GregorianCalendar` instance to JSON format.
- **Inputs**: None
- **Control Flow**:
    - A `GregorianCalendar` object is created with UTC timezone and US locale.
    - The calendar is cleared and set to a specific date and time (June 25, 2018, 10:20:30).
    - A `Gson` instance is created to handle JSON serialization.
    - The `GregorianCalendar` object is serialized to a JSON string.
    - An assertion checks that the serialized JSON string matches the expected format.
- **Output**:
    - The method outputs a JSON string representation of the `GregorianCalendar` object, which includes year, month, day, hour, minute, and second.
- **Functions called**:
    - [`com.google.gson.JsonArray.set`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDefaultGregorianCalendarDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDefaultGregorianCalendarDeserialization}} -->
Tests the deserialization of a `GregorianCalendar` object from a JSON string.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - Sets the default `TimeZone` to UTC and `Locale` to US for deterministic testing.
    - Creates a `Gson` instance for JSON deserialization.
    - Defines a JSON string representing a date and time.
    - Deserializes the JSON string into a `GregorianCalendar` object.
    - Asserts that the deserialized `GregorianCalendar` object has the expected year, month, day, hour, minute, and second.
    - Asserts that the time in milliseconds of the deserialized calendar matches the expected value.
    - Serializes the `GregorianCalendar` object back to JSON and asserts it matches the original JSON string.
- **Output**:
    - No return value; the method performs assertions to validate the deserialization and serialization process.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDateSerializationWithStyle<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithStyle}} -->
Tests the serialization and deserialization of a `Date` object using various date and time styles.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**:
    - `date`: A `Date` object initialized to the epoch time (0).
    - `styles`: An array of integers representing different date and time styles from `DateFormat`.
- **Control Flow**:
    - Iterates over each combination of date and time styles from the `styles` array.
    - For each combination, formats the `date` using `DateFormat.getDateTimeInstance` to get the expected string representation.
    - Creates a `Gson` instance with the specified date and time styles.
    - Serializes the `date` to JSON and asserts that the output matches the expected formatted string.
    - Deserializes the JSON back to a `Date` object and asserts that the time matches the original `date`.
    - Finally, tests the default date and time styles by creating a new `Gson` instance without specific styles and asserts the output.
- **Output**:
    - The method does not return a value but asserts that the serialized JSON representation of the `Date` matches the expected format and that deserialization returns the original `Date`.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDateSerializationWithDateStyle<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithDateStyle}} -->
Tests the serialization and deserialization of a `Date` object using various date styles.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A `Date` object is created representing the epoch time (0).
    - An array of date styles (FULL, LONG, MEDIUM, SHORT) is defined.
    - A loop iterates over each date style.
    - For each date style, the expected formatted date string is generated using `DateFormat.getDateTimeInstance`.
    - A `Gson` instance is created with the current date style set using `GsonBuilder.setDateFormat`.
    - The `Date` object is serialized to JSON using `gson.toJson`.
    - Assertions are made to check if the serialized JSON matches the expected formatted string.
    - Another assertion checks if deserializing the JSON back to a `Date` object returns the same time as the original `Date` object.
- **Output**:
    - The method does not return a value but asserts that the serialized JSON representation of the `Date` matches the expected format and that deserialization returns the original `Date`.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDateStyleOverwritesPattern<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDateStyleOverwritesPattern}} -->
Tests that setting a date style in `GsonBuilder` overwrites a previously set date format pattern.
- **Inputs**:
    - `pattern`: A string representing the initial date format pattern to be used.
    - `date`: A `Date` object initialized to a specific point in time (epoch time).
    - `gsonBuilder`: An instance of `GsonBuilder` used to configure the date format.
    - `style`: An integer representing the date style to be applied (e.g., `DateFormat.SHORT`).
    - `expectedFormatted`: A string representing the expected formatted date output based on the style.
    - `patternJson`: A JSON string representation of the date formatted using the initial pattern.
    - `styleJson`: A JSON string representation of the date formatted using the new style.
- **Control Flow**:
    - A `GsonBuilder` instance is created with an initial date format pattern.
    - A `Date` object is created representing the epoch time.
    - The date is serialized to JSON using the initial pattern and stored in `patternJson`.
    - The date format is then changed to a short style using `setDateFormat(style, style)`.
    - The date is serialized again to JSON using the new style and stored in `styleJson`.
    - The expected formatted date string is generated using `DateFormat.getDateTimeInstance(style, style, Locale.US).format(date)`.
    - Assertions are made to check that `styleJson` matches the expected formatted string.
    - An additional assertion checks that `styleJson` is not equal to `patternJson`.
- **Output**:
    - The method does not return a value but asserts that the JSON output for the date formatted with the style is correct and different from the output formatted with the pattern.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDateSerializationWithPattern<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithPattern}} -->
Tests the serialization of a `Date` object using a specified date pattern.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `pattern`: A string representing the date format pattern to be used for serialization.
    - `now`: A `Date` object initialized to a specific timestamp (1315806903103L) for testing.
- **Control Flow**:
    - A `Gson` instance is created using `GsonBuilder` with a specified date format pattern.
    - A `Date` object is created with a fixed timestamp.
    - The `Date` object is serialized to JSON using the [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the `Gson` instance.
    - The resulting JSON string is compared to the expected output using an assertion.
- **Output**:
    - The method asserts that the JSON representation of the `Date` object matches the expected string format, which is "2011-09-11".
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDateDeserializationWithPattern<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDateDeserializationWithPattern}} -->
Tests the deserialization of a `Date` object using a specified date pattern.
- **Inputs**:
    - `pattern`: A string representing the date format pattern to be used for deserialization.
    - `gson`: An instance of `Gson` configured with the specified date format.
    - `now`: A `Date` object representing a specific point in time.
    - `json`: A JSON string representation of the `Date` object.
    - `extracted`: A `Date` object obtained by deserializing the JSON string.
- **Control Flow**:
    - A `Gson` instance is created with a custom date format pattern.
    - A `Date` object is created with a specific timestamp.
    - The `Date` object is serialized to a JSON string.
    - The JSON string is deserialized back into a `Date` object.
    - Assertions are made to verify that the year, month, and day of the deserialized `Date` match the original `Date`.
- **Output**:
    - The method does not return a value but asserts that the deserialized `Date` object has the same year, month, and day as the original `Date` object.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDateSerializationWithPatternNotOverridenByTypeAdapter<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationWithPatternNotOverridenByTypeAdapter}} -->
Tests that the date serialization pattern is not overridden by a custom type adapter.
- **Inputs**: None
- **Control Flow**:
    - A `String` variable `pattern` is initialized with the date format 'yyyy-MM-dd'.
    - A `Gson` object is created using `GsonBuilder`, setting the date format to the specified pattern and registering a custom `JsonDeserializer` for `Date` that returns a fixed date.
    - A `Date` object `now` is created with a specific timestamp.
    - The `now` date is serialized to JSON using the `gson.toJson()` method.
    - The resulting JSON string is asserted to be equal to the expected date string formatted according to the specified pattern.
- **Output**:
    - The method outputs a JSON string representation of the `Date` object formatted as '"2011-09-11"'.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testDateSerializationInCollection<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testDateSerializationInCollection}} -->
Tests the serialization and deserialization of a list of `Date` objects using Gson.
- **Modifiers**: `public`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Sets the default time zone to UTC and locale to US for consistent date formatting.
    - Creates a `Gson` instance with a specified date format of 'yyyy-MM-dd'.
    - Serializes a list containing a single `Date` object (representing the epoch time) to JSON.
    - Asserts that the serialized JSON matches the expected output of '1970-01-01'.
    - Deserializes the JSON back into a list of `Date` objects and asserts that the time of the first date equals 0L (epoch time).
    - Restores the original time zone and locale in a finally block to ensure cleanup.
- **Output**:
    - The method does not return a value but asserts that the JSON representation of the date list is correct and that deserialization yields the expected `Date` object.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.GsonBuilder.setDateFormat`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetDateFormat)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonPrimitiveSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonPrimitiveSerialization}} -->
Tests the serialization of various `JsonPrimitive` types to their expected JSON string representations.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify the output of the `gson.toJson` method for different `JsonPrimitive` instances.
    - Each assertion checks that the JSON string produced matches the expected string representation for the given primitive value.
- **Output**:
    - The method does not return a value; it asserts that the serialized output matches expected JSON strings.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonPrimitiveDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonPrimitiveDeserialization}} -->
Tests the deserialization of JSON primitives into `JsonPrimitive` and `JsonElement` types.
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify that the `gson.fromJson` method correctly deserializes various JSON strings into `JsonPrimitive` and `JsonElement` objects.
    - For each test case, it checks both `JsonElement.class` and `JsonPrimitive.class` to ensure that the deserialization works for both types.
- **Output**:
    - The method does not return a value but asserts that the deserialized objects are equal to expected `JsonPrimitive` instances.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonNullSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonNullSerialization}} -->
Tests the serialization of `JsonNull` instances to JSON.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify the output of the `gson.toJson` method.
    - It checks that serializing `JsonNull.INSTANCE` as a `JsonElement` results in the string 'null'.
    - It also checks that serializing `JsonNull.INSTANCE` as a `JsonNull` also results in the string 'null'.
- **Output**:
    - The method does not return a value; it asserts that the output of the serialization is as expected.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testNullJsonElementSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testNullJsonElementSerialization}} -->
Tests the serialization of null values to JSON using Gson.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThat` to verify the output of the `gson.toJson` method.
    - It checks that serializing a null value as a `JsonElement` results in the string 'null'.
    - It also checks that serializing a null value as a `JsonNull` also results in the string 'null'.
- **Output**:
    - The method does not return a value; it asserts that the output of the serialization is equal to the string 'null' for both `JsonElement` and `JsonNull`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonArraySerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonArraySerialization}} -->
Tests the serialization of a `JsonArray` to a JSON string.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` is created.
    - Three `JsonPrimitive` elements (1, 2, and 3) are added to the `JsonArray`.
    - The `gson.toJson` method is called to serialize the `JsonArray` into a JSON string.
    - An assertion checks that the serialized JSON string matches the expected output '[1,2,3]'.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON string of the `JsonArray` is equal to '[1,2,3]'.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonArrayDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonArrayDeserialization}} -->
Tests the deserialization of a JSON array into a `JsonArray` object.
- **Inputs**: None
- **Control Flow**:
    - A `JsonArray` is created and populated with three `JsonPrimitive` integers (1, 2, and 3).
    - A JSON string representing an array of integers is defined as '[1,2,3]'.
    - The method asserts that deserializing the JSON string into a `JsonElement` results in an object equal to the created `JsonArray`.
    - The method also asserts that deserializing the JSON string into a `JsonArray` results in an object equal to the created `JsonArray`.
- **Output**:
    - The method does not return a value but uses assertions to verify that the deserialized objects match the expected `JsonArray`.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonObjectSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonObjectSerialization}} -->
Tests the serialization of a `JsonObject` to a JSON string.
- **Modifiers**: `public`, `test`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonObject` is created.
    - Two `JsonPrimitive` values are added to the `JsonObject` with keys 'foo' and 'bar'.
    - The `gson.toJson` method is called to serialize the `JsonObject` into a JSON string.
    - The resulting JSON string is compared to the expected output using an assertion.
- **Output**:
    - The method does not return a value but asserts that the serialized JSON string matches the expected format.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonObjectDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonObjectDeserialization}} -->
Tests the deserialization of a JSON object into a `JsonObject` using Gson.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - Creates a `JsonObject` and adds two `JsonPrimitive` values to it.
    - Defines a JSON string that represents the same structure as the created `JsonObject`.
    - Deserializes the JSON string into a `JsonElement` and asserts that it equals the created `JsonObject`.
    - Deserializes the JSON string into a `JsonObject` and asserts that it equals the created `JsonObject`.
- **Output**:
    - The method does not return a value; it asserts that the deserialized objects match the expected `JsonObject`.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonNullDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonNullDeserialization}} -->
Tests the deserialization of JSON null values into `JsonElement` and `JsonNull`.
- **Inputs**: None
- **Control Flow**:
    - The method uses assertions to verify that deserializing the string 'null' into `JsonElement` results in `JsonNull.INSTANCE`.
    - It also checks that deserializing the string 'null' into `JsonNull` produces the same `JsonNull.INSTANCE`.
- **Output**:
    - The method does not return a value; it asserts that the deserialization results are as expected.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testJsonElementTypeMismatch<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testJsonElementTypeMismatch}} -->
Tests that a `JsonSyntaxException` is thrown when a JSON string representing a primitive is deserialized into a `JsonObject`.
- **Inputs**: None
- **Control Flow**:
    - The method uses `assertThrows` to check if a `JsonSyntaxException` is thrown when attempting to deserialize a JSON string into a `JsonObject`.
    - The `gson.fromJson` method is called with a JSON string that represents a primitive value ("abc") and the target class (`JsonObject.class`).
    - If the exception is thrown, the test continues to the next assertion.
- **Output**:
    - The method does not return a value but asserts that the exception thrown has a specific message indicating a type mismatch.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testPropertiesSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testPropertiesSerialization}} -->
Tests the serialization of a `Properties` object to JSON.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - Creates a new instance of `Properties`.
    - Sets a property with key 'foo' and value 'bar'.
    - Serializes the `Properties` object to JSON using `gson.toJson()`.
    - Defines the expected JSON string as '{"foo":"bar"}'.
    - Asserts that the serialized JSON matches the expected string.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON representation of the `Properties` object is as expected.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testPropertiesDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testPropertiesDeserialization}} -->
Tests the deserialization of a JSON string into a `Properties` object.
- **Inputs**:
    - `json`: A string representing a JSON object with properties, in this case '{foo:'bar'}'.
- **Control Flow**:
    - The method initializes a string `json` with a JSON representation of a property.
    - It then uses the `gson` object to deserialize the JSON string into a `Properties` object.
    - Finally, it asserts that the value of the property 'foo' in the `Properties` object is equal to 'bar'.
- **Output**:
    - The method does not return a value; it asserts that the deserialized property value matches the expected value.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testTreeSetSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testTreeSetSerialization}} -->
Tests the serialization of a `TreeSet` containing a single string value.
- **Modifiers**: `public`, `void`, `Test`
- **Inputs**: None
- **Control Flow**:
    - A new `TreeSet<String>` is instantiated.
    - The string 'Value1' is added to the `TreeSet`.
    - The `TreeSet` is serialized to JSON format using `gson.toJson()`.
    - The resulting JSON string is asserted to be equal to the expected output '["Value1"]'.
- **Output**:
    - The method does not return a value; it asserts that the serialized JSON representation of the `TreeSet` matches the expected string.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testTreeSetDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testTreeSetDeserialization}} -->
Tests the deserialization of a JSON string into a `TreeSet<String>`.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a `TreeSet` is defined.
    - A `Type` object is created to specify the type of `TreeSet<String>`.
    - The `gson.fromJson` method is called to deserialize the JSON string into a `TreeSet<String>`.
    - An assertion is made to check that the deserialized `TreeSet` contains the expected value.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `TreeSet` contains 'Value1'.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testStringBuilderSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testStringBuilderSerialization}} -->
Tests the serialization of a `StringBuilder` object to JSON.
- **Modifiers**: `public`, `test`
- **Inputs**:
    - `sb`: A `StringBuilder` instance initialized with the string 'abc'.
- **Control Flow**:
    - Creates a new `StringBuilder` instance with the string 'abc'.
    - Serializes the `StringBuilder` instance to JSON using the `gson` object.
    - Asserts that the resulting JSON string is equal to the expected output, which is '"abc"'.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `StringBuilder` is correct.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testStringBuilderDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testStringBuilderDeserialization}} -->
This method tests the deserialization of a `StringBuilder` object from a JSON string.
- **Modifiers**: `public`, `void`
- **Inputs**: None
- **Control Flow**:
    - The method uses the `gson` instance to deserialize a JSON string representation of a `StringBuilder`.
    - It checks if the deserialized `StringBuilder`'s content matches the expected string 'abc' using an assertion.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `StringBuilder` contains the expected string.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testStringBufferSerialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testStringBufferSerialization}} -->
Tests the serialization of a `StringBuffer` object to JSON.
- **Modifiers**: `public`, `Test`, `SuppressWarnings`
- **Inputs**:
    - `sb`: A `StringBuffer` object initialized with the string 'abc'.
- **Control Flow**:
    - Creates a new `StringBuffer` instance with the content 'abc'.
    - Serializes the `StringBuffer` instance to JSON format using the `gson` object.
    - Asserts that the resulting JSON string is equal to the expected output, which is '"abc"'.
- **Output**:
    - The method does not return a value; it asserts that the JSON representation of the `StringBuffer` is correct.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)


---
#### DefaultTypeAdaptersTest\.testStringBufferDeserialization<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.testStringBufferDeserialization}} -->
Tests the deserialization of a `StringBuffer` from JSON using Gson.
- **Inputs**:
    - `gson`: An instance of `Gson` used for JSON deserialization.
    - `json`: A JSON string representing the `StringBuffer` to be deserialized.
- **Control Flow**:
    - The method calls `gson.fromJson` to deserialize the JSON string into a `StringBuffer` object.
    - It then asserts that the string representation of the deserialized `StringBuffer` is equal to the expected value 'abc'.
- **Output**:
    - The method does not return a value; it asserts that the deserialized `StringBuffer` contains the expected string.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest`](#DefaultTypeAdaptersTest)  (Base Class)



---
### ClassWithUrlField<!-- {{#class:com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithUrlField}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithUrlField` is a simple private static class that contains a single field of type `URL`. This class is used to test the serialization and deserialization of URL objects using Gson, a popular JSON library for Java.
- **Fields**:
    - `url`: `URL` A field of type `URL` that holds a URL object.


---
### ClassWithBigDecimal<!-- {{#class:com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithBigDecimal` is a private static class designed to encapsulate a `BigDecimal` value, providing functionality to initialize it from a string and to generate a JSON representation of the value using engineering string notation.
- **Fields**:
    - `value`: `BigDecimal` A `BigDecimal` field that stores the numeric value initialized from a string.
- **Methods**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal.ClassWithBigDecimal`](#ClassWithBigDecimalClassWithBigDecimal)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal.getExpectedJson`](#ClassWithBigDecimalgetExpectedJson)

**Methods**

---
#### ClassWithBigDecimal\.ClassWithBigDecimal<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal.ClassWithBigDecimal}} -->
The constructor `ClassWithBigDecimal` initializes an instance of the class by converting a string input into a `BigDecimal` and assigning it to the `value` field.
- **Inputs**:
    - `value`: A string representation of a number that will be converted into a `BigDecimal`.
- **Control Flow**:
    - The constructor takes a single string argument named `value`.
    - It creates a new `BigDecimal` object using the provided string.
    - The newly created `BigDecimal` object is assigned to the instance variable `value`.
- **Output**:
    - This is a constructor, so it does not return a value, but it initializes the `value` field of the class with a `BigDecimal` object.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal`](#DefaultTypeAdaptersTest.ClassWithBigDecimal)  (Base Class)


---
#### ClassWithBigDecimal\.getExpectedJson<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal.getExpectedJson}} -->
The `getExpectedJson` method returns a JSON string representation of the `value` field in engineering notation.
- **Inputs**: None
- **Control Flow**:
    - The method constructs a JSON string by concatenating a fixed JSON key `"value":` with the `value` field converted to an engineering string using `toEngineeringString()` method.
    - The constructed JSON string is returned.
- **Output**:
    - A JSON string representing the `value` field in engineering notation.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigDecimal`](#DefaultTypeAdaptersTest.ClassWithBigDecimal)  (Base Class)



---
### ClassWithBigInteger<!-- {{#class:com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigInteger}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithBigInteger` class is a simple utility class designed to encapsulate a `BigInteger` value, providing a constructor to initialize the value from a string and a method to return a JSON representation of the object.
- **Fields**:
    - `value`: `BigInteger` A `BigInteger` field that stores the numeric value initialized from a string.
- **Methods**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigInteger.ClassWithBigInteger`](#ClassWithBigIntegerClassWithBigInteger)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigInteger.getExpectedJson`](#ClassWithBigIntegergetExpectedJson)

**Methods**

---
#### ClassWithBigInteger\.ClassWithBigInteger<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigInteger.ClassWithBigInteger}} -->
The constructor `ClassWithBigInteger` initializes an instance of the class by converting a string input into a `BigInteger` and assigning it to the `value` field.
- **Modifiers**: ``
- **Inputs**:
    - `value`: A string representation of a number that will be converted into a `BigInteger`.
- **Control Flow**:
    - The constructor takes a single string argument named `value`.
    - It creates a new `BigInteger` object using the provided string.
    - The newly created `BigInteger` is assigned to the instance variable `value`.
- **Output**:
    - This is a constructor, so it does not return any value, but it initializes the `value` field of the class with a `BigInteger` object.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigInteger`](#DefaultTypeAdaptersTest.ClassWithBigInteger)  (Base Class)


---
#### ClassWithBigInteger\.getExpectedJson<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigInteger.getExpectedJson}} -->
The `getExpectedJson` method returns a JSON string representation of the `value` field in the format `{"value":<value>}`.
- **Modifiers**: ``
- **Inputs**: None
- **Control Flow**:
    - The method constructs a JSON string by concatenating the string `{"value":` with the `value` field and a closing brace `}`.
    - The constructed JSON string is returned as the output of the method.
- **Output**:
    - A JSON string representing the `value` field in the format `{"value":<value>}`.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.ClassWithBigInteger`](#DefaultTypeAdaptersTest.ClassWithBigInteger)  (Base Class)



---
### MyClassTypeAdapter<!-- {{#class:com.google.gson.functional.DefaultTypeAdaptersTest.MyClassTypeAdapter}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `MyClassTypeAdapter` class is a custom implementation of the `TypeAdapter` for the `Class<?>` type, designed to facilitate the serialization and deserialization of Java `Class` objects to and from JSON using the Gson library. It overrides the `write` method to serialize a `Class` object by writing its name to a `JsonWriter`, and the `read` method to deserialize a JSON string back into a `Class` object by attempting to load the class using `Class.forName`. This adapter is useful for handling `Class` objects in JSON, which are not natively supported by Gson.
- **Methods**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.MyClassTypeAdapter.write`](#MyClassTypeAdapterwrite)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.MyClassTypeAdapter.read`](#MyClassTypeAdapterread)

**Methods**

---
#### MyClassTypeAdapter\.write<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.MyClassTypeAdapter.write}} -->
The `write` method serializes a `Class<?>` object to its JSON representation by writing its name to a `JsonWriter`.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write the JSON output.
    - [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `Class<?>` object representing the class to be serialized.
- **Control Flow**:
    - The method calls `value.getName()` to retrieve the name of the class represented by the `Class<?>` object.
    - It then writes this class name as a JSON value using the `JsonWriter`'s [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method.
- **Output**:
    - The method does not return any value; it writes the class name to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.MyClassTypeAdapter`](#DefaultTypeAdaptersTest.MyClassTypeAdapter)  (Base Class)


---
#### MyClassTypeAdapter\.read<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.MyClassTypeAdapter.read}} -->
The `read` method reads a class name from a `JsonReader` and returns the corresponding `Class` object.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the class name is read as a string.
- **Control Flow**:
    - The method reads the next string from the `JsonReader` using `in.nextString()` and assigns it to `className`.
    - It attempts to load the class using `Class.forName(className)` and returns the `Class` object if successful.
    - If a `ClassNotFoundException` is thrown, it catches the exception and throws a new `IOException` with the caught exception as its cause.
- **Output**:
    - The method returns a `Class<?>` object representing the class corresponding to the name read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.MyClassTypeAdapter`](#DefaultTypeAdaptersTest.MyClassTypeAdapter)  (Base Class)



---
### NumberAsStringAdapter<!-- {{#class:com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter}} -->
- **Modifiers**: `static`
- **Description**: The `NumberAsStringAdapter` class is a custom `TypeAdapter` for the Gson library that facilitates the serialization and deserialization of `Number` objects by converting them to and from their string representations. It uses reflection to dynamically create instances of the specified `Number` subclass using a constructor that accepts a `String` argument. This adapter is particularly useful for handling numeric types that need to be represented as strings in JSON, such as `BigDecimal` and `BigInteger`, ensuring that the JSON output is a string rather than a numeric value.
- **Fields**:
    - `constructor`: `Constructor<? extends Number>` A `Constructor` object that is used to create instances of the specified `Number` subclass from a string.
- **Methods**:
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter.NumberAsStringAdapter`](#NumberAsStringAdapterNumberAsStringAdapter)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter.write`](#NumberAsStringAdapterwrite)
    - [`com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter.read`](#NumberAsStringAdapterread)

**Methods**

---
#### NumberAsStringAdapter\.NumberAsStringAdapter<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter.NumberAsStringAdapter}} -->
The `NumberAsStringAdapter` constructor initializes a `NumberAsStringAdapter` instance by obtaining a constructor of a specified `Number` subclass that takes a `String` as an argument.
- **Modifiers**: ``
- **Inputs**:
    - `type`: A `Class` object representing a subclass of `Number` that has a constructor accepting a `String` argument.
- **Control Flow**:
    - The constructor attempts to retrieve a constructor from the provided `type` that accepts a `String` as its parameter.
    - If successful, it assigns this constructor to the `constructor` field of the `NumberAsStringAdapter` instance.
    - If the constructor cannot be found, an `Exception` is thrown.
- **Output**:
    - The method does not return a value, but it initializes the `constructor` field of the `NumberAsStringAdapter` instance.
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter`](#DefaultTypeAdaptersTest.NumberAsStringAdapter)  (Base Class)


---
#### NumberAsStringAdapter\.write<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter.write}} -->
The `write` method writes a `Number` value to a `JsonWriter` as a string representation.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object to which the number will be written.
    - [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue): A `Number` object that represents the value to be written to the `JsonWriter`.
- **Control Flow**:
    - The method calls the [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) method on the `JsonWriter` object `out`, passing the string representation of the `Number` object [`value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue) using `value.toString()` as the argument.
- **Output**:
    - The method does not return any value; it writes the string representation of the `Number` to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter`](#DefaultTypeAdaptersTest.NumberAsStringAdapter)  (Base Class)


---
#### NumberAsStringAdapter\.read<!-- {{#callable:com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter.read}} -->
The `read` method reads a JSON string from a `JsonReader` and constructs a `Number` object using a constructor that takes a string argument.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON string is read.
- **Control Flow**:
    - The method attempts to read the next JSON string from the `JsonReader` using `in.nextString()`.
    - It then tries to create a new instance of `Number` using the `constructor` with the read string as an argument.
    - If an exception occurs during the instantiation, it catches the exception and throws an `AssertionError` with the caught exception as the cause.
- **Output**:
    - Returns a `Number` object created from the JSON string read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.functional.DefaultTypeAdaptersTest.NumberAsStringAdapter`](#DefaultTypeAdaptersTest.NumberAsStringAdapter)  (Base Class)



