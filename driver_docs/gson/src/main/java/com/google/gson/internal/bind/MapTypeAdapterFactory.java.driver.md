# Purpose
The provided Java source code defines a [`MapTypeAdapterFactory`](#MapTypeAdapterFactoryMapTypeAdapterFactory) class, which is part of the Gson library's internal binding package. This class is responsible for adapting Java `Map` objects to JSON representations and vice versa. It provides a mechanism to serialize and deserialize maps in two different formats: as JSON objects or as JSON arrays. The choice between these formats is determined by the `complexMapKeySerialization` flag. When this flag is set to false, maps are serialized as JSON objects, which requires that map keys can be converted to strings. If the flag is true, maps are serialized as arrays of map entries, allowing for more complex key types but requiring the receiver to understand this format.

The [`MapTypeAdapterFactory`](#MapTypeAdapterFactoryMapTypeAdapterFactory) class implements the `TypeAdapterFactory` interface, which is a part of the Gson library's type adapter mechanism. The class includes an inner [`Adapter`](#AdapterAdapter) class that extends `TypeAdapter<Map<K, V>>`, providing the actual logic for reading and writing JSON. The [`Adapter`](#AdapterAdapter) class handles the serialization and deserialization processes, checking for JSON tokens to determine the structure of the input or output JSON. It uses `TypeAdapter` instances for both keys and values, allowing for flexible handling of different data types. The factory pattern used here allows for the dynamic creation of type adapters based on the specific map types encountered during JSON processing, making this code a crucial component for handling complex data structures in JSON with Gson.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.gson.Gson`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.internal.ConstructorConstructor`
- `com.google.gson.internal.GsonTypes`
- `com.google.gson.internal.JsonReaderInternalAccess`
- `com.google.gson.internal.ObjectConstructor`
- `com.google.gson.internal.Streams`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.Type`
- `java.util.ArrayList`
- `java.util.List`
- `java.util.Map`


# Classes

---
### MapTypeAdapterFactory<!-- {{#class:com.google.gson.internal.bind.MapTypeAdapterFactory}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `MapTypeAdapterFactory` class is a final implementation of the `TypeAdapterFactory` interface in the Gson library, designed to handle the serialization and deserialization of Java `Map` objects to and from JSON. It supports two modes of serialization: as JSON objects for primitive keys or when complex map key serialization is disabled, and as JSON arrays of map entries when complex map key serialization is enabled. This flexibility allows for the handling of complex key types that cannot be serialized as strings. The class uses a `ConstructorConstructor` to create instances of maps and provides a nested `Adapter` class to perform the actual read and write operations for map entries, ensuring that duplicate keys are not allowed during deserialization.
- **Fields**:
    - `constructorConstructor`: `ConstructorConstructor` A `ConstructorConstructor` instance used to create map instances.
    - `complexMapKeySerialization`: `boolean` A boolean flag indicating whether complex map key serialization is enabled.
- **Methods**:
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.MapTypeAdapterFactory`](#MapTypeAdapterFactoryMapTypeAdapterFactory)
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.create`](#MapTypeAdapterFactorycreate)
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.getKeyAdapter`](#MapTypeAdapterFactorygetKeyAdapter)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### MapTypeAdapterFactory\.MapTypeAdapterFactory<!-- {{#callable:com.google.gson.internal.bind.MapTypeAdapterFactory.MapTypeAdapterFactory}} -->
The `MapTypeAdapterFactory` constructor initializes a new instance with a `ConstructorConstructor` and a flag for complex map key serialization.
- **Modifiers**: `public`
- **Inputs**:
    - `constructorConstructor`: An instance of `ConstructorConstructor` used to create new instances of objects.
    - `complexMapKeySerialization`: A boolean flag indicating whether complex map key serialization is enabled.
- **Control Flow**:
    - Assigns the provided `constructorConstructor` to the instance variable `this.constructorConstructor`.
    - Assigns the provided `complexMapKeySerialization` to the instance variable `this.complexMapKeySerialization`.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of `MapTypeAdapterFactory`.
- **See also**: [`com.google.gson.internal.bind.MapTypeAdapterFactory`](#MapTypeAdapterFactory)  (Base Class)


---
#### MapTypeAdapterFactory\.create<!-- {{#callable:com.google.gson.internal.bind.MapTypeAdapterFactory.create}} -->
The `create` method generates a `TypeAdapter` for a given `TypeToken` if it represents a `Map`, otherwise it returns null.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of `Gson` used to obtain type adapters.
    - `typeToken`: A `TypeToken` representing the type for which a `TypeAdapter` is to be created.
- **Control Flow**:
    - Retrieve the `Type` from the `typeToken`.
    - Get the raw class type from the `typeToken`.
    - Check if the raw type is assignable from `Map`; if not, return null.
    - Extract key and value types from the map type using `GsonTypes.getMapKeyAndValueTypes`.
    - Obtain a `TypeAdapter` for the key type using [`getKeyAdapter`](#MapTypeAdapterFactorygetKeyAdapter) and wrap it with `TypeAdapterRuntimeTypeWrapper`.
    - Obtain a `TypeAdapter` for the value type using `gson.getAdapter` and wrap it with `TypeAdapterRuntimeTypeWrapper`.
    - Create an `ObjectConstructor` for the map type using `constructorConstructor.get` with `allowUnsafe` set to false.
    - Instantiate a new `Adapter` with the wrapped key and value adapters and the constructor, and return it.
- **Output**:
    - A `TypeAdapter<T>` for the specified `TypeToken` if it represents a `Map`, otherwise null.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.internal.GsonTypes.getMapKeyAndValueTypes`](../GsonTypes.java.driver.md#GsonTypesgetMapKeyAndValueTypes)
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.getKeyAdapter`](#MapTypeAdapterFactorygetKeyAdapter)
    - [`com.google.gson.Gson.getAdapter`](../../Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.reflect.TypeToken.get`](../../reflect/TypeToken.java.driver.md#TypeTokenget)
- **See also**: [`com.google.gson.internal.bind.MapTypeAdapterFactory`](#MapTypeAdapterFactory)  (Base Class)


---
#### MapTypeAdapterFactory\.getKeyAdapter<!-- {{#callable:com.google.gson.internal.bind.MapTypeAdapterFactory.getKeyAdapter}} -->
The `getKeyAdapter` method returns a `TypeAdapter` for a given key type, using a special adapter for boolean types.
- **Modifiers**: `private`
- **Inputs**:
    - `context`: An instance of `Gson` used to obtain the appropriate `TypeAdapter`.
    - `keyType`: The `Type` of the key for which a `TypeAdapter` is needed.
- **Control Flow**:
    - Check if the `keyType` is either `boolean.class` or `Boolean.class`.
    - If true, return `TypeAdapters.BOOLEAN_AS_STRING`.
    - Otherwise, use the `context` to get a `TypeAdapter` for the `keyType` using `TypeToken.get(keyType)`.
- **Output**:
    - Returns a `TypeAdapter<?>` that is appropriate for the given key type, with special handling for boolean types.
- **Functions called**:
    - [`com.google.gson.Gson.getAdapter`](../../Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.reflect.TypeToken.get`](../../reflect/TypeToken.java.driver.md#TypeTokenget)
- **See also**: [`com.google.gson.internal.bind.MapTypeAdapterFactory`](#MapTypeAdapterFactory)  (Base Class)



---
### Adapter<!-- {{#class:com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter}} -->
- **Modifiers**: `private`, `final`
- **Description**: The `Adapter` class is a private final inner class extending `TypeAdapter` for `Map<K, V>`, designed to handle the serialization and deserialization of maps to and from JSON, either as JSON objects or JSON arrays, depending on the complexity of the map keys. It uses specific `TypeAdapter` instances for the keys and values, and an `ObjectConstructor` to create map instances. The class ensures that duplicate keys are not allowed during deserialization and provides a mechanism to handle complex map key serialization.
- **Fields**:
    - `keyTypeAdapter`: `TypeAdapter<K>` A `TypeAdapter` for serializing and deserializing the map's keys.
    - `valueTypeAdapter`: `TypeAdapter<V>` A `TypeAdapter` for serializing and deserializing the map's values.
    - `constructor`: `ObjectConstructor<? extends Map<K, V>>` An `ObjectConstructor` used to create instances of the map.
- **Methods**:
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.Adapter`](#AdapterAdapter)
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.read`](#Adapterread)
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.write`](#Adapterwrite)
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.keyToString`](#AdapterkeyToString)

**Methods**

---
#### Adapter\.Adapter<!-- {{#callable:com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.Adapter}} -->
The `Adapter` constructor initializes an instance of the `Adapter` class with specified key and value type adapters and a map constructor.
- **Modifiers**: `public`
- **Inputs**:
    - `keyTypeAdapter`: A `TypeAdapter` for the map's key type, used to serialize and deserialize keys.
    - `valueTypeAdapter`: A `TypeAdapter` for the map's value type, used to serialize and deserialize values.
    - `constructor`: An `ObjectConstructor` that constructs instances of the map.
- **Control Flow**:
    - The constructor assigns the provided `keyTypeAdapter` to the instance variable `this.keyTypeAdapter`.
    - The constructor assigns the provided `valueTypeAdapter` to the instance variable `this.valueTypeAdapter`.
    - The constructor assigns the provided `constructor` to the instance variable `this.constructor`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `Adapter` class.
- **See also**: [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter`](#MapTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.read<!-- {{#callable:com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.read}} -->
The [`read`](../../TypeAdapter.java.driver.md#TypeAdapterread) method deserializes a JSON input into a Map object, handling both JSON objects and arrays, while checking for duplicate keys.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A JsonReader object that provides the JSON input to be deserialized.
- **Control Flow**:
    - The method starts by peeking at the next JSON token from the input.
    - If the token is NULL, it reads the null value and returns null.
    - It constructs a new Map instance using the provided constructor.
    - If the token indicates the beginning of an array, it enters a loop to read each entry as a key-value pair from nested arrays, adding them to the map.
    - If a duplicate key is detected during insertion, a JsonSyntaxException is thrown.
    - If the token indicates the beginning of an object, it enters a loop to read each key-value pair, promoting the name to a value, and adding them to the map.
    - Again, if a duplicate key is detected, a JsonSyntaxException is thrown.
    - The method returns the constructed map after processing all entries.
- **Output**:
    - The method returns a Map<K, V> object populated with the deserialized key-value pairs from the JSON input, or null if the input is a JSON null.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.internal.ObjectConstructor.construct`](../ObjectConstructor.java.driver.md#ObjectConstructorconstruct)
    - [`com.google.gson.stream.JsonReader.beginArray`](../../stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.hasNext`](../../stream/JsonReader.java.driver.md#JsonReaderhasNext)
    - [`com.google.gson.TypeAdapter.read`](../../TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](JsonTreeWriter.java.driver.md#JsonTreeWriterput)
    - [`com.google.gson.stream.JsonReader.endArray`](../../stream/JsonReader.java.driver.md#JsonReaderendArray)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../stream/JsonReader.java.driver.md#JsonReaderbeginObject)
    - [`com.google.gson.internal.JsonReaderInternalAccess.promoteNameToValue`](../JsonReaderInternalAccess.java.driver.md#JsonReaderInternalAccesspromoteNameToValue)
    - [`com.google.gson.stream.JsonReader.endObject`](../../stream/JsonReader.java.driver.md#JsonReaderendObject)
- **See also**: [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter`](#MapTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.write<!-- {{#callable:com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.write}} -->
The [`write`](../../TypeAdapter.java.driver.md#TypeAdapterwrite) method serializes a given map into JSON format using a `JsonWriter`, handling both simple and complex map key serialization.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write the JSON output.
    - `map`: A `Map<K, V>` object representing the map to be serialized into JSON.
- **Control Flow**:
    - Check if the map is null; if so, write a null value to the `JsonWriter` and return.
    - If `complexMapKeySerialization` is false, begin writing a JSON object, iterate over the map entries, write each key as a string and its corresponding value using `valueTypeAdapter`, then end the JSON object.
    - If `complexMapKeySerialization` is true, initialize lists to store keys and values, and a boolean to track if there are complex keys.
    - Iterate over the map entries, convert each key to a `JsonElement` using `keyTypeAdapter`, add the key and value to their respective lists, and update the boolean if the key is a JSON array or object.
    - If complex keys are present, begin writing a JSON array, iterate over the keys and values, write each as a JSON array entry using `Streams.write` for keys and `valueTypeAdapter` for values, then end the JSON array.
    - If no complex keys are present, begin writing a JSON object, iterate over the keys and values, convert each key to a string using [`keyToString`](#AdapterkeyToString), write the key and its corresponding value using `valueTypeAdapter`, then end the JSON object.
- **Output**:
    - The method does not return a value; it writes the serialized JSON representation of the map to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.TypeAdapter.write`](../../TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.TypeAdapter.toJsonTree`](../../TypeAdapter.java.driver.md#TypeAdaptertoJsonTree)
    - [`com.google.gson.JsonElement.isJsonArray`](../../JsonElement.java.driver.md#JsonElementisJsonArray)
    - [`com.google.gson.JsonElement.isJsonObject`](../../JsonElement.java.driver.md#JsonElementisJsonObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../stream/JsonWriter.java.driver.md#JsonWriterendArray)
    - [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.keyToString`](#AdapterkeyToString)
- **See also**: [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter`](#MapTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.keyToString<!-- {{#callable:com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter.keyToString}} -->
The `keyToString` method converts a `JsonElement` key into its string representation based on its type.
- **Modifiers**: `private`
- **Inputs**:
    - `keyElement`: A `JsonElement` representing the key to be converted to a string.
- **Control Flow**:
    - Check if `keyElement` is a JSON primitive.
    - If it is a number, convert it to a string using `getAsNumber()`.
    - If it is a boolean, convert it to a string using `getAsBoolean()`.
    - If it is a string, return it directly using `getAsString()`.
    - If none of the above, throw an `AssertionError`.
    - If `keyElement` is JSON null, return the string "null".
    - If `keyElement` is neither a JSON primitive nor null, throw an `AssertionError`.
- **Output**:
    - A string representation of the `JsonElement` key.
- **Functions called**:
    - [`com.google.gson.JsonElement.isJsonPrimitive`](../../JsonElement.java.driver.md#JsonElementisJsonPrimitive)
    - [`com.google.gson.JsonElement.getAsJsonPrimitive`](../../JsonElement.java.driver.md#JsonElementgetAsJsonPrimitive)
    - [`com.google.gson.JsonPrimitive.isNumber`](../../JsonPrimitive.java.driver.md#JsonPrimitiveisNumber)
    - [`com.google.gson.JsonPrimitive.getAsNumber`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsNumber)
    - [`com.google.gson.JsonPrimitive.isBoolean`](../../JsonPrimitive.java.driver.md#JsonPrimitiveisBoolean)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
    - [`com.google.gson.JsonElement.getAsBoolean`](../../JsonElement.java.driver.md#JsonElementgetAsBoolean)
    - [`com.google.gson.JsonPrimitive.isString`](../../JsonPrimitive.java.driver.md#JsonPrimitiveisString)
    - [`com.google.gson.JsonElement.getAsString`](../../JsonElement.java.driver.md#JsonElementgetAsString)
    - [`com.google.gson.JsonElement.isJsonNull`](../../JsonElement.java.driver.md#JsonElementisJsonNull)
- **See also**: [`com.google.gson.internal.bind.MapTypeAdapterFactory.Adapter`](#MapTypeAdapterFactory.Adapter)  (Base Class)



