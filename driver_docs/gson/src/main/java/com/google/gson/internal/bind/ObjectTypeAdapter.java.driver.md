# Purpose
The [`ObjectTypeAdapter`](#ObjectTypeAdapterObjectTypeAdapter) class is a specialized component within the Gson library, designed to handle the serialization and deserialization of JSON data where the static type is `Object`. This class provides a broad functionality by adapting various JSON structures, such as arrays and objects, into Java's `List` and `Map` structures, respectively. It leverages the Gson framework's capabilities to dynamically determine the appropriate type during serialization using the `getClass()` method and employs a `ToNumberStrategy` to handle numeric conversions during deserialization. The class is structured to handle both nested and terminal JSON elements, ensuring that complex JSON structures can be accurately represented in Java.

The class defines a public API through its static method [`getFactory`](#ObjectTypeAdaptergetFactory), which provides a `TypeAdapterFactory` for creating instances of [`ObjectTypeAdapter`](#ObjectTypeAdapterObjectTypeAdapter) based on a specified `ToNumberStrategy`. This factory pattern allows for flexible integration with the Gson library, enabling users to customize how numbers are handled during JSON parsing. The [`ObjectTypeAdapter`](#ObjectTypeAdapterObjectTypeAdapter) class is a crucial component for scenarios where JSON data is not strictly typed, providing a robust mechanism to handle dynamic and polymorphic JSON content. Its implementation includes methods for reading and writing JSON, ensuring that both serialization and deserialization processes are efficiently managed.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.gson.Gson`
- `com.google.gson.ToNumberPolicy`
- `com.google.gson.ToNumberStrategy`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.internal.LinkedTreeMap`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.util.ArrayDeque`
- `java.util.ArrayList`
- `java.util.Deque`
- `java.util.List`
- `java.util.Map`


# Classes

---
### ObjectTypeAdapter<!-- {{#class:com.google.gson.internal.bind.ObjectTypeAdapter}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `ObjectTypeAdapter` class is a specialized `TypeAdapter` for handling JSON serialization and deserialization of objects whose static type is `Object`. It uses the Gson library to adapt these objects by determining their actual runtime type during serialization and by using a primitive, Map, or List during deserialization. The class supports different number strategies through the `ToNumberStrategy` interface, allowing for flexible handling of numeric values. It also provides a factory method to create instances of `ObjectTypeAdapter` based on the specified number strategy.
- **Fields**:
    - `DOUBLE_FACTORY`: `TypeAdapterFactory` A static final field that holds a default TypeAdapterFactory using the ToNumberPolicy.DOUBLE.
    - `gson`: `Gson` A final field that holds a reference to the Gson instance used for serialization and deserialization.
    - `toNumberStrategy`: `ToNumberStrategy` A final field that holds the strategy for reading numbers from JSON.
- **Methods**:
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.ObjectTypeAdapter`](#ObjectTypeAdapterObjectTypeAdapter)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.newFactory`](#ObjectTypeAdapternewFactory)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.getFactory`](#ObjectTypeAdaptergetFactory)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.tryBeginNesting`](#ObjectTypeAdaptertryBeginNesting)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.readTerminal`](#ObjectTypeAdapterreadTerminal)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.read`](#ObjectTypeAdapterread)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.write`](#ObjectTypeAdapterwrite)

**Methods**

---
#### ObjectTypeAdapter\.ObjectTypeAdapter<!-- {{#callable:com.google.gson.internal.bind.ObjectTypeAdapter.ObjectTypeAdapter}} -->
The `ObjectTypeAdapter` constructor initializes an instance with a specified `Gson` object and `ToNumberStrategy`.
- **Modifiers**: `private`
- **Inputs**:
    - `gson`: An instance of the `Gson` class used for JSON serialization and deserialization.
    - `toNumberStrategy`: An instance of `ToNumberStrategy` that defines how numbers are read from JSON.
- **Control Flow**:
    - Assigns the provided `gson` parameter to the instance variable `this.gson`.
    - Assigns the provided `toNumberStrategy` parameter to the instance variable `this.toNumberStrategy`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of `ObjectTypeAdapter`.
- **See also**: [`com.google.gson.internal.bind.ObjectTypeAdapter`](#ObjectTypeAdapter)  (Base Class)


---
#### ObjectTypeAdapter\.newFactory<!-- {{#callable:com.google.gson.internal.bind.ObjectTypeAdapter.newFactory}} -->
The `newFactory` method creates a new `TypeAdapterFactory` that can produce `ObjectTypeAdapter` instances for `Object` types using a specified `ToNumberStrategy`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `toNumberStrategy`: A `ToNumberStrategy` instance that defines how numbers should be handled during deserialization.
- **Control Flow**:
    - The method returns an anonymous implementation of `TypeAdapterFactory`.
    - Within the `create` method of this factory, it checks if the raw type of the provided `TypeToken` is `Object`.
    - If the type is `Object`, it returns a new `ObjectTypeAdapter` initialized with the provided `Gson` instance and `toNumberStrategy`.
    - If the type is not `Object`, it returns `null`.
- **Output**:
    - The method returns a `TypeAdapterFactory` that can create `ObjectTypeAdapter` instances for `Object` types.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.internal.bind.ObjectTypeAdapter`](#ObjectTypeAdapter)  (Base Class)


---
#### ObjectTypeAdapter\.getFactory<!-- {{#callable:com.google.gson.internal.bind.ObjectTypeAdapter.getFactory}} -->
The `getFactory` method returns a `TypeAdapterFactory` based on the provided `ToNumberStrategy`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `toNumberStrategy`: A `ToNumberStrategy` object that determines the strategy for number conversion.
- **Control Flow**:
    - Check if the `toNumberStrategy` is equal to `ToNumberPolicy.DOUBLE`.
    - If true, return the `DOUBLE_FACTORY` which is a pre-defined `TypeAdapterFactory` using `ToNumberPolicy.DOUBLE`.
    - If false, call and return the result of `newFactory(toNumberStrategy)` which creates a new `TypeAdapterFactory` based on the provided `toNumberStrategy`.
- **Output**:
    - Returns a `TypeAdapterFactory` that is either the `DOUBLE_FACTORY` or a new factory created with the given `toNumberStrategy`.
- **Functions called**:
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.newFactory`](#ObjectTypeAdapternewFactory)
- **See also**: [`com.google.gson.internal.bind.ObjectTypeAdapter`](#ObjectTypeAdapter)  (Base Class)


---
#### ObjectTypeAdapter\.tryBeginNesting<!-- {{#callable:com.google.gson.internal.bind.ObjectTypeAdapter.tryBeginNesting}} -->
The `tryBeginNesting` method attempts to start reading a JSON array or object and returns a corresponding data structure or null if neither is found.
- **Modifiers**: `private`
- **Inputs**:
    - `in`: A `JsonReader` object used to read the JSON input.
    - `peeked`: A `JsonToken` representing the current token in the JSON input.
- **Control Flow**:
    - The method uses a switch statement to check the value of the `peeked` token.
    - If `peeked` is `BEGIN_ARRAY`, it calls `in.beginArray()` and returns a new `ArrayList`.
    - If `peeked` is `BEGIN_OBJECT`, it calls `in.beginObject()` and returns a new `LinkedTreeMap`.
    - If `peeked` is neither `BEGIN_ARRAY` nor `BEGIN_OBJECT`, it returns null.
- **Output**:
    - Returns an `ArrayList` if a JSON array is started, a `LinkedTreeMap` if a JSON object is started, or null if neither is applicable.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.beginArray`](../../stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../stream/JsonReader.java.driver.md#JsonReaderbeginObject)
- **See also**: [`com.google.gson.internal.bind.ObjectTypeAdapter`](#ObjectTypeAdapter)  (Base Class)


---
#### ObjectTypeAdapter\.readTerminal<!-- {{#callable:com.google.gson.internal.bind.ObjectTypeAdapter.readTerminal}} -->
The `readTerminal` method reads a terminal JSON token from a `JsonReader` and returns its corresponding Java object representation.
- **Modifiers**: `private`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON token is read.
    - `peeked`: A `JsonToken` representing the type of the next token in the `JsonReader`.
- **Control Flow**:
    - The method uses a switch statement to determine the type of the `peeked` token.
    - If the token is a `STRING`, it reads and returns the next string from the `JsonReader`.
    - If the token is a `NUMBER`, it uses the `toNumberStrategy` to read and return the number.
    - If the token is a `BOOLEAN`, it reads and returns the next boolean value from the `JsonReader`.
    - If the token is `NULL`, it reads the null value and returns `null`.
    - If the token is none of the above, it throws an `IllegalStateException` indicating an unexpected token.
- **Output**:
    - The method returns an `Object` that represents the value of the terminal JSON token read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.ToNumberStrategy.readNumber`](../../ToNumberStrategy.java.driver.md#ToNumberStrategyreadNumber)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
- **See also**: [`com.google.gson.internal.bind.ObjectTypeAdapter`](#ObjectTypeAdapter)  (Base Class)


---
#### ObjectTypeAdapter\.read<!-- {{#callable:com.google.gson.internal.bind.ObjectTypeAdapter.read}} -->
The `read` method deserializes JSON data from a `JsonReader` into a Java `Object`, which can be a `List`, `Map`, or a terminal value.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which JSON data is read.
- **Control Flow**:
    - Peek the next JSON token from the `JsonReader`.
    - Attempt to begin reading a JSON array or object using [`tryBeginNesting`](#ObjectTypeAdaptertryBeginNesting); if unsuccessful, read a terminal value using [`readTerminal`](#ObjectTypeAdapterreadTerminal).
    - Initialize a stack to manage nested JSON structures.
    - Enter a loop to process JSON elements while there are more tokens to read.
    - If the current object is a `Map`, read the next name for the JSON object member.
    - Peek the next token and attempt to begin a new nested structure; if unsuccessful, read a terminal value.
    - Add the read value to the current `List` or `Map` based on its type.
    - If a new nested structure was started, push the current object onto the stack and set the current object to the new nested structure.
    - End the current JSON array or object when no more tokens are available.
    - If the stack is empty, return the current object; otherwise, pop the last object from the stack and continue processing.
- **Output**:
    - The method returns a deserialized Java `Object` representing the JSON data, which can be a `List`, `Map`, or a terminal value such as a `String`, `Number`, `Boolean`, or `null`.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](JsonTreeReader.java.driver.md#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.tryBeginNesting`](#ObjectTypeAdaptertryBeginNesting)
    - [`com.google.gson.internal.bind.ObjectTypeAdapter.readTerminal`](#ObjectTypeAdapterreadTerminal)
    - [`com.google.gson.internal.bind.JsonTreeReader.hasNext`](JsonTreeReader.java.driver.md#JsonTreeReaderhasNext)
    - [`com.google.gson.stream.JsonReader.nextName`](../../stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.internal.LinkedTreeMap.put`](../LinkedTreeMap.java.driver.md#LinkedTreeMapput)
    - [`com.google.gson.stream.JsonReader.endArray`](../../stream/JsonReader.java.driver.md#JsonReaderendArray)
    - [`com.google.gson.stream.JsonReader.endObject`](../../stream/JsonReader.java.driver.md#JsonReaderendObject)
- **See also**: [`com.google.gson.internal.bind.ObjectTypeAdapter`](#ObjectTypeAdapter)  (Base Class)


---
#### ObjectTypeAdapter\.write<!-- {{#callable:com.google.gson.internal.bind.ObjectTypeAdapter.write}} -->
The [`write`](../../TypeAdapter.java.driver.md#TypeAdapterwrite) method serializes an object to JSON using a `JsonWriter`, handling null values and delegating to a specific `TypeAdapter` for non-null objects.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` instance used to write the JSON output.
    - `value`: The object to be serialized into JSON.
- **Control Flow**:
    - Check if the `value` is null; if so, write a null value to the `JsonWriter` and return.
    - Retrieve the `TypeAdapter` for the class of the `value` using the `gson` instance.
    - Check if the retrieved `TypeAdapter` is an instance of `ObjectTypeAdapter`; if so, write an empty JSON object to the `JsonWriter` and return.
    - Otherwise, use the retrieved `TypeAdapter` to write the `value` to the `JsonWriter`.
- **Output**:
    - The method does not return a value; it writes the serialized JSON representation of the object to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.Gson.getAdapter`](../../Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../stream/JsonWriter.java.driver.md#JsonWriterendObject)
    - [`com.google.gson.TypeAdapter.write`](../../TypeAdapter.java.driver.md#TypeAdapterwrite)
- **See also**: [`com.google.gson.internal.bind.ObjectTypeAdapter`](#ObjectTypeAdapter)  (Base Class)



