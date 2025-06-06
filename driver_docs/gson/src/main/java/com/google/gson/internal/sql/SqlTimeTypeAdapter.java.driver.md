# Purpose
The provided Java source code defines a class [`SqlTimeTypeAdapter`](#SqlTimeTypeAdapterSqlTimeTypeAdapter) that extends `TypeAdapter<Time>`, specifically designed to handle the serialization and deserialization of `java.sql.Time` objects using the Gson library. This class is part of the `com.google.gson.internal.sql` package and provides a narrow functionality focused on converting `Time` objects to and from their JSON representation. The class includes a `TypeAdapterFactory` named `FACTORY` that facilitates the creation of [`SqlTimeTypeAdapter`](#SqlTimeTypeAdapterSqlTimeTypeAdapter) instances when the `TypeToken` corresponds to `Time.class`. This ensures that the adapter is only applied to `Time` objects, maintaining type safety and consistency within the Gson framework.

The [`SqlTimeTypeAdapter`](#SqlTimeTypeAdapterSqlTimeTypeAdapter) class is not thread-safe due to its use of `DateFormat`, which captures the time zone and locale upon creation and is inherently stateful. To address this, the class synchronizes its [`read`](#SqlTimeTypeAdapterread) and [`write`](#SqlTimeTypeAdapterwrite) methods to ensure thread safety during JSON parsing and formatting operations. The [`read`](#SqlTimeTypeAdapterread) method parses a JSON string into a `Time` object, handling potential `ParseException` by throwing a `JsonSyntaxException` with detailed error information. Conversely, the [`write`](#SqlTimeTypeAdapterwrite) method converts a `Time` object into its JSON string representation. This class is a specialized component within the Gson library, providing a crucial bridge between SQL time representations and JSON, ensuring accurate and reliable data interchange.
# Imports and Dependencies

---
- `com.google.gson.internal.sql`
- `com.google.gson.Gson`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.sql.Time`
- `java.text.DateFormat`
- `java.text.ParseException`
- `java.text.SimpleDateFormat`
- `java.util.Date`
- `java.util.TimeZone`


# Classes

---
### SqlTimeTypeAdapter<!-- {{#class:com.google.gson.internal.sql.SqlTimeTypeAdapter}} -->
- **Modifiers**: `final`
- **Description**: The `SqlTimeTypeAdapter` class is a custom Gson `TypeAdapter` for serializing and deserializing `java.sql.Time` objects to and from JSON. It uses a `SimpleDateFormat` to format the time as a string in the "hh:mm:ss a" format and handles the conversion of JSON strings to `Time` objects. The class is designed to be thread-safe by synchronizing access to the `DateFormat` object, which is not inherently thread-safe. It also includes a static `TypeAdapterFactory` to facilitate the creation of this adapter for `Time` objects.
- **Fields**:
    - `FACTORY`: `TypeAdapterFactory` A static `TypeAdapterFactory` that creates instances of `SqlTimeTypeAdapter` for `Time` objects.
    - `format`: `DateFormat` A `DateFormat` object used to format and parse time strings in the "hh:mm:ss a" format.
- **Methods**:
    - [`com.google.gson.internal.sql.SqlTimeTypeAdapter.create`](#SqlTimeTypeAdaptercreate)
    - [`com.google.gson.internal.sql.SqlTimeTypeAdapter.SqlTimeTypeAdapter`](#SqlTimeTypeAdapterSqlTimeTypeAdapter)
    - [`com.google.gson.internal.sql.SqlTimeTypeAdapter.read`](#SqlTimeTypeAdapterread)
    - [`com.google.gson.internal.sql.SqlTimeTypeAdapter.write`](#SqlTimeTypeAdapterwrite)

**Methods**

---
#### SqlTimeTypeAdapter\.create<!-- {{#callable:com.google.gson.internal.sql.SqlTimeTypeAdapter.create}} -->
The `create` method returns a `SqlTimeTypeAdapter` if the provided `TypeToken` represents a `Time` class, otherwise it returns null.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class, used for JSON serialization and deserialization.
    - `typeToken`: A `TypeToken` representing the type for which a `TypeAdapter` is requested.
- **Control Flow**:
    - Check if the raw type of `typeToken` is `Time.class`.
    - If true, cast a new instance of `SqlTimeTypeAdapter` to `TypeAdapter<T>` and return it.
    - If false, return null.
- **Output**:
    - Returns a `TypeAdapter<T>` for `Time` if the `typeToken` is of type `Time`, otherwise returns null.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.internal.sql.SqlTimeTypeAdapter`](#SqlTimeTypeAdapter)  (Base Class)


---
#### SqlTimeTypeAdapter\.SqlTimeTypeAdapter<!-- {{#callable:com.google.gson.internal.sql.SqlTimeTypeAdapter.SqlTimeTypeAdapter}} -->
The `SqlTimeTypeAdapter` constructor is a private method that initializes an instance of the `SqlTimeTypeAdapter` class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is private, meaning it cannot be accessed outside the class, ensuring that instances of `SqlTimeTypeAdapter` can only be created within the class itself.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.internal.sql.SqlTimeTypeAdapter`](#SqlTimeTypeAdapter)  (Base Class)


---
#### SqlTimeTypeAdapter\.read<!-- {{#callable:com.google.gson.internal.sql.SqlTimeTypeAdapter.read}} -->
The `read` method reads a JSON token from a `JsonReader` and converts it into a `Time` object, handling null values and parsing exceptions.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON token is read.
- **Control Flow**:
    - Check if the next JSON token is `NULL`; if so, consume it and return `null`.
    - Read the next JSON token as a string.
    - Synchronize on `this` to ensure thread safety when accessing the `DateFormat` object.
    - Save the original time zone of the `DateFormat` object.
    - Attempt to parse the string into a `Date` object using the `DateFormat` object.
    - If parsing is successful, return a new `Time` object initialized with the time from the `Date` object.
    - If a `ParseException` occurs, throw a `JsonSyntaxException` with details of the failure.
    - Finally, restore the original time zone of the `DateFormat` object.
- **Output**:
    - Returns a `Time` object representing the parsed time, or `null` if the JSON token was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.sql.SqlTimeTypeAdapter`](#SqlTimeTypeAdapter)  (Base Class)


---
#### SqlTimeTypeAdapter\.write<!-- {{#callable:com.google.gson.internal.sql.SqlTimeTypeAdapter.write}} -->
The `write` method serializes a `Time` object into its JSON representation using a `JsonWriter`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write the JSON output.
    - [`value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue): A `Time` object that is to be serialized into JSON.
- **Control Flow**:
    - Check if the [`value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue) is `null`; if so, write a `null` value to the `JsonWriter` and return.
    - If [`value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue) is not `null`, synchronize on `this` to ensure thread safety when formatting the `Time` object.
    - Format the `Time` object into a string using the `DateFormat` instance.
    - Write the formatted time string to the `JsonWriter`.
- **Output**:
    - The method writes the JSON representation of the `Time` object to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.value`](../../stream/JsonWriter.java.driver.md#JsonWritervalue)
- **See also**: [`com.google.gson.internal.sql.SqlTimeTypeAdapter`](#SqlTimeTypeAdapter)  (Base Class)



