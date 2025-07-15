# Purpose
The [`NumberTypeAdapter`](#NumberTypeAdapterNumberTypeAdapter) class in the provided Java source code is a specialized component within the Gson library, designed to handle the serialization and deserialization of `Number` objects in JSON data. This class extends the `TypeAdapter<Number>` and provides a concrete implementation for reading and writing `Number` types using a `JsonReader` and `JsonWriter`, respectively. The primary functionality of this class is to convert JSON tokens into Java `Number` objects and vice versa, utilizing a strategy pattern through the `ToNumberStrategy` interface. This allows for flexible handling of number parsing, accommodating different policies such as lazy parsing, which is encapsulated in the `ToNumberPolicy.LAZILY_PARSED_NUMBER`.

The class also defines a static factory method, [`getFactory`](#NumberTypeAdaptergetFactory), which returns a `TypeAdapterFactory` based on the specified `ToNumberStrategy`. This factory method ensures that the appropriate [`NumberTypeAdapter`](#NumberTypeAdapterNumberTypeAdapter) is used depending on the parsing strategy, providing a mechanism for integrating this adapter into the broader Gson serialization framework. The [`NumberTypeAdapter`](#NumberTypeAdapterNumberTypeAdapter) is a focused component, providing narrow functionality specifically for number handling within JSON, and it does not define public APIs or external interfaces beyond its role in the Gson library's internal binding mechanisms.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.gson.Gson`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.ToNumberPolicy`
- `com.google.gson.ToNumberStrategy`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`


# Classes

---
### NumberTypeAdapter<!-- {{#class:com.google.gson.internal.bind.NumberTypeAdapter}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `NumberTypeAdapter` class is a specialized `TypeAdapter` for handling JSON serialization and deserialization of `Number` objects in the Gson library. It utilizes a `ToNumberStrategy` to determine how numbers are parsed from JSON, supporting both lazy parsing and other strategies. The class provides a factory method to create instances of `TypeAdapterFactory` based on the specified `ToNumberStrategy`, allowing for flexible number parsing policies. It overrides the `read` and `write` methods to handle JSON tokens appropriately, ensuring that numbers are correctly interpreted and serialized.
- **Fields**:
    - `LAZILY_PARSED_NUMBER_FACTORY`: `TypeAdapterFactory` A static final field that holds a TypeAdapterFactory using the LAZILY_PARSED_NUMBER policy.
    - `toNumberStrategy`: `ToNumberStrategy` A final field that holds the strategy for parsing numbers from JSON.
- **Methods**:
    - [`com.google.gson.internal.bind.NumberTypeAdapter.NumberTypeAdapter`](#NumberTypeAdapterNumberTypeAdapter)
    - [`com.google.gson.internal.bind.NumberTypeAdapter.newFactory`](#NumberTypeAdapternewFactory)
    - [`com.google.gson.internal.bind.NumberTypeAdapter.getFactory`](#NumberTypeAdaptergetFactory)
    - [`com.google.gson.internal.bind.NumberTypeAdapter.read`](#NumberTypeAdapterread)
    - [`com.google.gson.internal.bind.NumberTypeAdapter.write`](#NumberTypeAdapterwrite)

**Methods**

---
#### NumberTypeAdapter\.NumberTypeAdapter<!-- {{#callable:com.google.gson.internal.bind.NumberTypeAdapter.NumberTypeAdapter}} -->
The constructor initializes a NumberTypeAdapter with a specified ToNumberStrategy.
- **Modifiers**: `private`
- **Inputs**:
    - `toNumberStrategy`: An instance of ToNumberStrategy that defines how numbers should be parsed from JSON.
- **Control Flow**:
    - Assigns the provided ToNumberStrategy instance to the class's toNumberStrategy field.
- **Output**:
    - This constructor does not return a value as it is a constructor.
- **See also**: [`com.google.gson.internal.bind.NumberTypeAdapter`](#NumberTypeAdapter)  (Base Class)


---
#### NumberTypeAdapter\.newFactory<!-- {{#callable:com.google.gson.internal.bind.NumberTypeAdapter.newFactory}} -->
The `newFactory` method creates a `TypeAdapterFactory` for `Number` types using a specified `ToNumberStrategy`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `toNumberStrategy`: An instance of `ToNumberStrategy` that defines how numbers should be parsed.
- **Control Flow**:
    - Instantiate a `NumberTypeAdapter` using the provided `toNumberStrategy`.
    - Return a new `TypeAdapterFactory` that overrides the `create` method.
    - In the `create` method, check if the raw type of the provided `TypeToken` is `Number`.
    - If the type is `Number`, return the `NumberTypeAdapter` cast to the appropriate type; otherwise, return `null`.
- **Output**:
    - A `TypeAdapterFactory` that can create a `TypeAdapter` for `Number` types using the specified `ToNumberStrategy`.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.internal.bind.NumberTypeAdapter`](#NumberTypeAdapter)  (Base Class)


---
#### NumberTypeAdapter\.getFactory<!-- {{#callable:com.google.gson.internal.bind.NumberTypeAdapter.getFactory}} -->
The `getFactory` method returns a `TypeAdapterFactory` based on the provided `ToNumberStrategy`, using a predefined factory for `LAZILY_PARSED_NUMBER` or creating a new one otherwise.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `toNumberStrategy`: An instance of `ToNumberStrategy` that determines how numbers should be parsed.
- **Control Flow**:
    - Check if the `toNumberStrategy` is equal to `ToNumberPolicy.LAZILY_PARSED_NUMBER`.
    - If true, return the predefined `LAZILY_PARSED_NUMBER_FACTORY`.
    - If false, call [`newFactory`](#NumberTypeAdapternewFactory) with the provided `toNumberStrategy` to create and return a new `TypeAdapterFactory`.
- **Output**:
    - Returns a `TypeAdapterFactory` that corresponds to the given `ToNumberStrategy`.
- **Functions called**:
    - [`com.google.gson.internal.bind.NumberTypeAdapter.newFactory`](#NumberTypeAdapternewFactory)
- **See also**: [`com.google.gson.internal.bind.NumberTypeAdapter`](#NumberTypeAdapter)  (Base Class)


---
#### NumberTypeAdapter\.read<!-- {{#callable:com.google.gson.internal.bind.NumberTypeAdapter.read}} -->
The `read` method reads a JSON token from the `JsonReader` and returns it as a `Number` if it is a number or string, or throws an exception if it is not.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON token is read.
- **Control Flow**:
    - Peek at the next JSON token using `in.peek()` and store it in `jsonToken`.
    - Use a switch statement to handle different types of `jsonToken`.
    - If `jsonToken` is `NULL`, call `in.nextNull()` to consume the null token and return `null`.
    - If `jsonToken` is `NUMBER` or `STRING`, use `toNumberStrategy.readNumber(in)` to read and return the number.
    - For any other `jsonToken`, throw a `JsonSyntaxException` indicating an unexpected token type.
- **Output**:
    - Returns a `Number` object if the JSON token is a number or string, or `null` if the token is null.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.ToNumberStrategy.readNumber`](../../ToNumberStrategy.java.driver.md#ToNumberStrategyreadNumber)
    - [`com.google.gson.stream.JsonReader.getPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPath)
- **See also**: [`com.google.gson.internal.bind.NumberTypeAdapter`](#NumberTypeAdapter)  (Base Class)


---
#### NumberTypeAdapter\.write<!-- {{#callable:com.google.gson.internal.bind.NumberTypeAdapter.write}} -->
The `write` method writes a `Number` value to a `JsonWriter`.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object to which the number will be written.
    - [`value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue): A `Number` object representing the value to be written to the `JsonWriter`.
- **Control Flow**:
    - The method calls the [`value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue) method on the `JsonWriter` object `out`, passing the `Number` object [`value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue) as an argument.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.internal.bind.NumberTypeAdapter`](#NumberTypeAdapter)  (Base Class)



