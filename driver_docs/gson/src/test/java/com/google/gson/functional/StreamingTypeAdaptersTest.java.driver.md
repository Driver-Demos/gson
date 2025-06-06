# Purpose
The `StreamingTypeAdaptersTest` Java class is a comprehensive test suite designed to validate the functionality of custom type adapters in the Gson library, which is used for converting Java objects to JSON and vice versa. This class specifically focuses on testing serialization and deserialization processes for various data structures, including custom objects like `Truck`, [`Person`](#PersonPerson), and [`Node`](#NodeNode), as well as standard data structures like maps and arrays. The tests ensure that the Gson library correctly handles these conversions, even when dealing with null values or custom serialization logic. The class employs JUnit testing framework annotations to define test cases, and it uses assertions from the Google Truth library to verify expected outcomes.

The class defines several test methods that cover a range of scenarios, such as handling null fields, using custom type adapters, and dealing with recursive data structures. A notable feature is the use of a custom `TypeAdapter` for the [`Person`](#PersonPerson) class, which demonstrates how to customize the serialization and deserialization process for specific object types. Additionally, the class includes tests for ensuring that the Gson library's null safety features are correctly implemented. By providing a detailed set of test cases, this class serves as a robust validation tool for developers working with Gson to ensure that their JSON processing logic is accurate and reliable.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.common.base.Splitter`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.JsonArray`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.TypeAdapter`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.util.ArrayList`
- `java.util.Arrays`
- `java.util.Collections`
- `java.util.LinkedHashMap`
- `java.util.List`
- `java.util.Map`
- `org.junit.Test`


# Classes

---
### StreamingTypeAdaptersTest<!-- {{#class:com.google.gson.functional.StreamingTypeAdaptersTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `StreamingTypeAdaptersTest` class is a comprehensive test suite designed to validate the serialization and deserialization capabilities of the Gson library, specifically focusing on custom type adapters for various data structures such as `Truck`, `Map`, and arrays. It includes tests for handling null values, custom serialization logic, and recursive data structures, ensuring that the Gson library can accurately convert Java objects to JSON and vice versa. The class also demonstrates the use of custom type adapters to modify the default serialization behavior, such as adapting the `Person` class to serialize only names.
- **Fields**:
    - `miniGson`: `Gson` An instance of Gson used for creating type adapters.
    - `truckAdapter`: `TypeAdapter<Truck>` A TypeAdapter for serializing and deserializing Truck objects.
    - `mapAdapter`: `TypeAdapter<Map<String, Double>>` A TypeAdapter for serializing and deserializing Map<String, Double> objects.
- **Methods**:
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerialize`](#StreamingTypeAdaptersTesttestSerialize)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testDeserialize`](#StreamingTypeAdaptersTesttestDeserialize)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeNullField`](#StreamingTypeAdaptersTesttestSerializeNullField)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeNullField`](#StreamingTypeAdaptersTesttestDeserializeNullField)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeNullObject`](#StreamingTypeAdaptersTesttestSerializeNullObject)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeNullObject`](#StreamingTypeAdaptersTesttestDeserializeNullObject)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeWithCustomTypeAdapter`](#StreamingTypeAdaptersTesttestSerializeWithCustomTypeAdapter)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeWithCustomTypeAdapter`](#StreamingTypeAdaptersTesttestDeserializeWithCustomTypeAdapter)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.usePersonNameAdapter`](#StreamingTypeAdaptersTestusePersonNameAdapter)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeMap`](#StreamingTypeAdaptersTesttestSerializeMap)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeMap`](#StreamingTypeAdaptersTesttestDeserializeMap)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerialize1dArray`](#StreamingTypeAdaptersTesttestSerialize1dArray)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testDeserialize1dArray`](#StreamingTypeAdaptersTesttestDeserialize1dArray)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerialize2dArray`](#StreamingTypeAdaptersTesttestSerialize2dArray)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testDeserialize2dArray`](#StreamingTypeAdaptersTesttestDeserialize2dArray)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testNullSafe`](#StreamingTypeAdaptersTesttestNullSafe)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeRecursive`](#StreamingTypeAdaptersTesttestSerializeRecursive)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.testFromJsonTree`](#StreamingTypeAdaptersTesttestFromJsonTree)

**Methods**

---
#### StreamingTypeAdaptersTest\.testSerialize<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerialize}} -->
The `testSerialize` method tests the serialization of a `Truck` object into a JSON string and verifies its correctness.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Truck` object is instantiated.
    - The `passengers` field of the `Truck` object is set to a list containing two `Person` objects, 'Jesse' and 'Jodie', both aged 29.
    - The `horsePower` field of the `Truck` object is set to 300.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of `truckAdapter` is called to serialize the `Truck` object into a JSON string, and all double quotes in the resulting JSON string are replaced with single quotes.
    - The `assertThat` method is used to assert that the serialized JSON string matches the expected JSON string representation of the `Truck` object.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testDeserialize<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testDeserialize}} -->
The `testDeserialize` method tests the deserialization of a JSON string into a `Truck` object and verifies the correctness of the deserialized data.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a `Truck` object with specific attributes is defined.
    - The JSON string's single quotes are replaced with double quotes to make it valid JSON.
    - The `truckAdapter` is used to deserialize the JSON string into a `Truck` object.
    - Assertions are made to verify that the `horsePower` of the deserialized `Truck` is 300.0.
    - Assertions are made to verify that the `passengers` list of the deserialized `Truck` contains two `Person` objects with the expected names and ages.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testSerializeNullField<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeNullField}} -->
The `testSerializeNullField` method tests the serialization of a `Truck` object with a null `passengers` field to ensure it correctly outputs a JSON string with the `passengers` field set to null.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Truck` object is instantiated.
    - The `passengers` field of the `Truck` object is explicitly set to null.
    - The `truckAdapter` is used to serialize the `Truck` object to a JSON string, replacing double quotes with single quotes for comparison.
    - An assertion is made to check that the serialized JSON string matches the expected string with `passengers` set to null.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the JSON serialization output.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testDeserializeNullField<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeNullField}} -->
The `testDeserializeNullField` method tests the deserialization of a JSON string with a null field into a `Truck` object and verifies that the `passengers` field is null.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a `Truck` object with a `horsePower` of 0.0 and `passengers` set to null is created and the single quotes are replaced with double quotes.
    - The [`fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson) method of `truckAdapter` is called with the JSON string to deserialize it into a `Truck` object.
    - An assertion is made using `assertThat` to verify that the `passengers` field of the deserialized `Truck` object is null.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the deserialization behavior.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testSerializeNullObject<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeNullObject}} -->
The `testSerializeNullObject` method tests the serialization of a `Truck` object containing a null `Person` in its passengers list to JSON format.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `Truck` object is instantiated.
    - The `passengers` field of the `Truck` object is set to a list containing a single null `Person` object.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of `truckAdapter` is called to serialize the `Truck` object to a JSON string, with double quotes replaced by single quotes.
    - An assertion is made to check that the resulting JSON string is equal to the expected JSON string "{'horsePower':0.0,'passengers':[null]}".
- **Output**:
    - The method does not return any value; it performs an assertion to validate the JSON serialization of a `Truck` object with a null passenger.
- **Functions called**:
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testDeserializeNullObject<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeNullObject}} -->
The `testDeserializeNullObject` method tests the deserialization of a JSON string into a `Truck` object where the passengers list contains a null value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by deserializing a JSON string representing a `Truck` object with a `horsePower` of 0.0 and a `passengers` list containing a single null value.
    - The JSON string uses single quotes, which are replaced with double quotes to conform to JSON standards before deserialization.
    - The [`fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson) method of `truckAdapter` is used to convert the JSON string into a `Truck` object.
    - An assertion is made to verify that the `passengers` list of the deserialized `Truck` object is equal to a list containing a single null `Person` object.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testSerializeWithCustomTypeAdapter<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeWithCustomTypeAdapter}} -->
The `testSerializeWithCustomTypeAdapter` method tests the serialization of a `Truck` object using a custom `TypeAdapter` for `Person` that only serializes the name.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Invoke `usePersonNameAdapter()` to register a custom `TypeAdapter` for `Person` that serializes only the name.
    - Create a `Truck` object and set its `passengers` field to a list containing two `Person` objects with names 'Jesse' and 'Jodie'.
    - Serialize the `Truck` object to JSON using the `truckAdapter` and replace double quotes with single quotes in the resulting JSON string.
    - Assert that the serialized JSON string is equal to the expected JSON string "{'horsePower':0.0,'passengers':['Jesse','Jodie']}".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.usePersonNameAdapter`](#StreamingTypeAdaptersTestusePersonNameAdapter)
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testDeserializeWithCustomTypeAdapter<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeWithCustomTypeAdapter}} -->
The method `testDeserializeWithCustomTypeAdapter` tests the deserialization of a JSON string into a `Truck` object using a custom type adapter for `Person` objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by calling `usePersonNameAdapter()` to register a custom type adapter for `Person` objects that only considers the name and sets the age to -1.
    - It then deserializes a JSON string representing a `Truck` object with a list of passenger names using the `truckAdapter`.
    - The JSON string is converted to use double quotes instead of single quotes for valid JSON syntax.
    - The deserialized `Truck` object is expected to have passengers with names 'Jesse' and 'Jodie', both with an age of -1.
    - An assertion checks that the deserialized `Truck` object's passengers match the expected list of `Person` objects.
- **Output**:
    - The method does not return a value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.usePersonNameAdapter`](#StreamingTypeAdaptersTestusePersonNameAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.usePersonNameAdapter<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.usePersonNameAdapter}} -->
The `usePersonNameAdapter` method configures a custom `TypeAdapter` for the `Person` class to serialize and deserialize only the name of a `Person` object, ignoring the age.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapter` for the `Person` class is created with overridden `read` and `write` methods.
    - The `read` method reads a `String` from the `JsonReader` and returns a new `Person` object with the name set to the read string and age set to -1.
    - The `write` method writes the `name` of the `Person` object to the `JsonWriter`.
    - A new `Gson` instance is created with the custom `TypeAdapter` registered for the `Person` class.
    - The `truckAdapter` is updated to use the new `Gson` instance to get the adapter for the `Truck` class.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testSerializeMap<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeMap}} -->
The `testSerializeMap` method tests the serialization of a `Map<String, Double>` to a JSON string using a `TypeAdapter`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `LinkedHashMap` is instantiated and populated with two key-value pairs: "a" mapped to 5.0 and "b" mapped to 10.0.
    - The `mapAdapter` is used to convert the map to a JSON string, and the double quotes in the JSON string are replaced with single quotes.
    - An assertion checks that the resulting JSON string is equal to "{'a':5.0,'b':10.0}".
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the map serialization.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testDeserializeMap<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testDeserializeMap}} -->
The `testDeserializeMap` method tests the deserialization of a JSON string into a `Map<String, Double>` using a `TypeAdapter` and verifies the result against an expected map.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `LinkedHashMap` is created and populated with two key-value pairs: 'a' mapped to 5.0 and 'b' mapped to 10.0.
    - The JSON string "{'a':5.0,'b':10.0}" is deserialized into a `Map<String, Double>` using the `mapAdapter` after replacing single quotes with double quotes.
    - An assertion is made to check if the deserialized map is equal to the expected map.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testSerialize1dArray<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerialize1dArray}} -->
The `testSerialize1dArray` method tests the serialization of a one-dimensional array of doubles into a JSON string using a TypeAdapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A TypeAdapter for a double array is obtained using `miniGson.getAdapter` with a `TypeToken` for `double[]`.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the `arrayAdapter` is called with a double array `{1.0, 2.0, 3.0}` to serialize it into a JSON string.
    - An assertion is made using `assertThat` to check if the serialized JSON string is equal to the expected string `"[1.0,2.0,3.0]"`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testDeserialize1dArray<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testDeserialize1dArray}} -->
The `testDeserialize1dArray` method tests the deserialization of a JSON string into a one-dimensional array of doubles using a Gson TypeAdapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A TypeAdapter for a double array is obtained using the miniGson instance and a TypeToken for double[].
    - The JSON string '[1.0,2.0,3.0]' is deserialized into a double array using the TypeAdapter's fromJson method.
    - An assertion is made to check that the deserialized array is equal to a new double array {1.0, 2.0, 3.0}.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that the deserialized array matches the expected array.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testSerialize2dArray<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerialize2dArray}} -->
The `testSerialize2dArray` method tests the serialization of a 2D array of doubles into a JSON string using a Gson TypeAdapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A TypeAdapter for a 2D array of doubles is obtained using `miniGson.getAdapter` with a `TypeToken` for `double[][]`.
    - A 2D array of doubles is initialized with the values `{{1.0, 2.0}, {3.0}}`.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the TypeAdapter is called to serialize the 2D array into a JSON string.
    - An assertion is made to check that the serialized JSON string is equal to the expected string `"[[1.0,2.0],[3.0]]"`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testDeserialize2dArray<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testDeserialize2dArray}} -->
The `testDeserialize2dArray` method tests the deserialization of a JSON string into a 2D array of doubles using a TypeAdapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A TypeAdapter for a 2D array of doubles is obtained using `miniGson.getAdapter` with a `TypeToken` for `double[][]`.
    - The JSON string `"[[1.0,2.0],[3.0]]"` is deserialized into a 2D array of doubles using the [`fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson) method of the TypeAdapter.
    - An expected 2D array `{{1.0, 2.0}, {3.0}}` is defined for comparison.
    - The deserialized array is compared to the expected array using `assertThat` to ensure they are equal.
- **Output**:
    - The method does not return any value; it asserts that the deserialized array matches the expected array.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testNullSafe<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testNullSafe}} -->
The `testNullSafe` method tests the behavior of a custom `TypeAdapter` for `Person` objects when handling null values during JSON serialization and deserialization using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A custom `TypeAdapter` for `Person` is defined with `read` and `write` methods to handle JSON conversion.
    - A `Gson` instance is created with the custom `TypeAdapter` registered for `Person` class.
    - A `Truck` object is created with a `horsePower` of 1.0 and a `passengers` list containing a null and a `Person` object.
    - The method asserts that serializing the `Truck` object with the non-null-safe `TypeAdapter` throws a `NullPointerException`.
    - A JSON string representing a `Truck` with a null passenger is defined.
    - The method asserts that deserializing this JSON string with the non-null-safe `TypeAdapter` throws a `JsonSyntaxException` with a specific error message.
    - A second `Gson` instance is created with the [`nullSafe`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapternullSafe) version of the `TypeAdapter`.
    - The method asserts that serializing the `Truck` object with the null-safe `TypeAdapter` produces the expected JSON string.
    - The method asserts that deserializing the JSON string with the null-safe `TypeAdapter` correctly reconstructs the `Truck` object with the expected properties.
- **Output**:
    - The method does not return a value; it uses assertions to verify the expected behavior of JSON serialization and deserialization with null-safe and non-null-safe type adapters.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonWriter.value`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritervalue)
    - [`com.google.gson.GsonBuilder.registerTypeAdapter`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuilderregisterTypeAdapter)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](RuntimeTypeAdapterFactoryFunctionalTest.java.driver.md#RuntimeTypeAdapterFactorycreate)
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
    - [`com.google.gson.TypeAdapter.fromJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJson)
    - [`com.google.gson.TypeAdapter.nullSafe`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapternullSafe)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testSerializeRecursive<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testSerializeRecursive}} -->
The `testSerializeRecursive` method tests the serialization of a binary tree structure into JSON format using a custom `TypeAdapter` for the `Node` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `TypeAdapter` for the `Node` class is retrieved using `miniGson.getAdapter(Node.class)`.
    - A root `Node` object is created with the label 'root'.
    - Two child `Node` objects are created with labels 'left' and 'right' and assigned to the `left` and `right` properties of the root node, respectively.
    - The [`toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson) method of the `nodeAdapter` is called to serialize the root node into a JSON string, with double quotes replaced by single quotes.
    - An assertion is made to check if the serialized JSON string matches the expected JSON structure representing the binary tree.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the JSON serialization.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)


---
#### StreamingTypeAdaptersTest\.testFromJsonTree<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.testFromJsonTree}} -->
The `testFromJsonTree` method tests the deserialization of a `JsonObject` into a `Truck` object using a `TypeAdapter`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonObject` named `truckObject` is created and a `horsePower` field with a value of 300 is added to it.
    - A `JsonArray` named `passengersArray` is created to hold passenger data.
    - A `JsonObject` named `jesseObject` is created with fields `age` set to 30 and `name` set to 'Jesse', and it is added to `passengersArray`.
    - The `passengersArray` is added to the `truckObject` under the key `passengers`.
    - The `truckObject` is deserialized into a `Truck` object using the `truckAdapter`'s [`fromJsonTree`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJsonTree) method.
    - Assertions are made to verify that the `horsePower` of the deserialized `Truck` is 300.0 and that the `passengers` list contains a `Person` object with the name 'Jesse' and age 30.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.TypeAdapter.fromJsonTree`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJsonTree)
    - [`com.google.gson.JsonArray.asList`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest`](#StreamingTypeAdaptersTest)  (Base Class)



---
### Truck<!-- {{#class:com.google.gson.functional.StreamingTypeAdaptersTest.Truck}} -->
- **Modifiers**: `static`
- **Description**: The `Truck` class represents a vehicle with a specified horsepower and a list of passengers, where each passenger is represented by a `Person` object. It is used in the context of serialization and deserialization tests within the `StreamingTypeAdaptersTest` class, demonstrating how to handle JSON data with Gson.
- **Fields**:
    - `horsePower`: `double` Represents the power of the truck's engine in horsepower.
    - `passengers`: `List<Person>` A list of `Person` objects representing the passengers in the truck, initialized to an empty list by default.


---
### Person<!-- {{#class:com.google.gson.functional.StreamingTypeAdaptersTest.Person}} -->
- **Modifiers**: `static`
- **Description**: The `Person` class represents an individual with a name and age, providing methods to compare instances and generate hash codes based on these attributes.
- **Fields**:
    - `age`: `int` An integer representing the age of the person.
    - `name`: `String` A string representing the name of the person.
- **Methods**:
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.Person.Person`](#PersonPerson)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.Person.equals`](#Personequals)
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.Person.hashCode`](#PersonhashCode)

**Methods**

---
#### Person\.Person<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.Person.Person}} -->
The `Person` constructor initializes a new `Person` object with a specified name and age.
- **Inputs**:
    - `name`: A `String` representing the name of the person.
    - `age`: An `int` representing the age of the person.
- **Control Flow**:
    - Assigns the provided `name` to the `name` field of the `Person` object.
    - Assigns the provided `age` to the `age` field of the `Person` object.
- **Output**:
    - This constructor does not return a value; it initializes the fields of a `Person` object.
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest.Person`](#StreamingTypeAdaptersTest.Person)  (Base Class)


---
#### Person\.equals<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.Person.equals}} -->
The [`equals`](MapTest.java.driver.md#Pointequals) method checks if a given object is a `Person` and has the same name and age as the current `Person` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: An object to be compared with the current `Person` instance.
- **Control Flow**:
    - Check if the input object `o` is an instance of `Person`.
    - If `o` is a `Person`, cast it to `Person` and compare its `name` field with the current instance's `name` field using the [`equals`](MapTest.java.driver.md#Pointequals) method.
    - Also, compare the `age` field of the casted `Person` object with the current instance's `age` field using the `==` operator.
    - Return `true` if both the `name` and `age` fields match; otherwise, return `false`.
- **Output**:
    - A boolean value indicating whether the input object is a `Person` with the same name and age as the current instance.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.Point.equals`](MapTest.java.driver.md#Pointequals)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest.Person`](#StreamingTypeAdaptersTest.Person)  (Base Class)


---
#### Person\.hashCode<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.Person.hashCode}} -->
The [`hashCode`](MapTest.java.driver.md#PointhashCode) method computes a hash code for a `Person` object by combining the hash code of the `name` field with the `age` field using a bitwise XOR operation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method retrieves the hash code of the `name` field, which is a `String`, using its [`hashCode`](MapTest.java.driver.md#PointhashCode) method.
    - It then performs a bitwise XOR operation between the hash code of the `name` and the `age` field, which is an `int`.
    - The result of the XOR operation is returned as the hash code for the `Person` object.
- **Output**:
    - An integer representing the hash code of the `Person` object.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.Point.hashCode`](MapTest.java.driver.md#PointhashCode)
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest.Person`](#StreamingTypeAdaptersTest.Person)  (Base Class)



---
### Node<!-- {{#class:com.google.gson.functional.StreamingTypeAdaptersTest.Node}} -->
- **Modifiers**: `static`
- **Description**: The `Node` class represents a basic structure for a binary tree node, containing a label and references to left and right child nodes.
- **Fields**:
    - `label`: `String` A string representing the label or value of the node.
    - `left`: `Node` A reference to the left child node, which is also of type Node.
    - `right`: `Node` A reference to the right child node, which is also of type Node.
- **Methods**:
    - [`com.google.gson.functional.StreamingTypeAdaptersTest.Node.Node`](#NodeNode)

**Methods**

---
#### Node\.Node<!-- {{#callable:com.google.gson.functional.StreamingTypeAdaptersTest.Node.Node}} -->
The `Node` constructor initializes a new `Node` object with a specified label.
- **Inputs**:
    - `label`: A `String` representing the label of the node.
- **Control Flow**:
    - Assigns the provided `label` to the `label` field of the `Node` instance.
- **Output**:
    - A new instance of the `Node` class with its `label` field set to the provided argument.
- **See also**: [`com.google.gson.functional.StreamingTypeAdaptersTest.Node`](#StreamingTypeAdaptersTest.Node)  (Base Class)



