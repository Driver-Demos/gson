# Purpose
The provided Java source code file is part of the Gson library, specifically within the `com.google.gson.internal.bind` package. It defines a collection of `TypeAdapter` and `TypeAdapterFactory` instances for various basic data types, such as `Class`, `BitSet`, `Boolean`, `Number` (including `Byte`, `Short`, `Integer`, `Long`, `Float`, `Double`), `Character`, `String`, `BigDecimal`, `BigInteger`, `AtomicInteger`, `AtomicBoolean`, `AtomicIntegerArray`, `URL`, `URI`, `InetAddress`, `UUID`, `Currency`, `Calendar`, `Locale`, and `JsonElement`. These adapters are responsible for serializing and deserializing these types to and from JSON, providing a mechanism to handle JSON data in a type-safe manner. The file also includes factory methods to create `TypeAdapterFactory` instances, which are used to register these adapters with a `Gson` instance.

The primary purpose of this file is to provide a comprehensive set of type adapters that facilitate the conversion between Java objects and their JSON representations. This is crucial for the Gson library, which is widely used for JSON parsing and serialization in Java applications. The file ensures that common data types are supported out-of-the-box, allowing developers to easily integrate JSON processing into their applications without needing to implement custom serialization logic for these types. Additionally, the file includes error handling and validation to ensure that the JSON data conforms to expected formats, throwing exceptions when invalid data is encountered. This robust handling of various data types and the provision of factory methods for adapter creation are key technical components that enhance the flexibility and usability of the Gson library.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.gson.Gson`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonIOException`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.internal.LazilyParsedNumber`
- `com.google.gson.internal.NumberLimits`
- `com.google.gson.internal.TroubleshootingGuide`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `java.net.InetAddress`
- `java.net.URI`
- `java.net.URISyntaxException`
- `java.net.URL`
- `java.util.ArrayList`
- `java.util.BitSet`
- `java.util.Calendar`
- `java.util.Currency`
- `java.util.GregorianCalendar`
- `java.util.List`
- `java.util.Locale`
- `java.util.StringTokenizer`
- `java.util.UUID`
- `java.util.concurrent.atomic.AtomicBoolean`
- `java.util.concurrent.atomic.AtomicInteger`
- `java.util.concurrent.atomic.AtomicIntegerArray`


# Classes

---
### TypeAdapters<!-- {{#class:com.google.gson.internal.bind.TypeAdapters}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `TypeAdapters` class provides a collection of static `TypeAdapter` and `TypeAdapterFactory` instances for various basic data types, facilitating the serialization and deserialization of these types using the Gson library. It includes adapters for primitive types, collections, and other common Java classes, ensuring compatibility and handling of special cases such as null values and type mismatches. The class is designed to be non-instantiable, as indicated by its private constructor, and it throws an `UnsupportedOperationException` if instantiation is attempted.
- **Fields**:
    - `CLASS`: `TypeAdapter<Class>` A `TypeAdapter` for the `Class` type that throws an `UnsupportedOperationException` for both serialization and deserialization.
    - `CLASS_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for the `Class` type using the `CLASS` adapter.
    - `BIT_SET`: `TypeAdapter<BitSet>` A `TypeAdapter` for `BitSet` that reads and writes JSON arrays of 0s and 1s.
    - `BIT_SET_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `BitSet` using the `BIT_SET` adapter.
    - `BOOLEAN`: `TypeAdapter<Boolean>` A `TypeAdapter` for `Boolean` that supports reading from strings for compatibility.
    - `BOOLEAN_AS_STRING`: `TypeAdapter<Boolean>` A `TypeAdapter` for `Boolean` that writes booleans as strings, useful for map keys.
    - `BOOLEAN_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Boolean` using the `BOOLEAN` adapter.
    - `BYTE`: `TypeAdapter<Number>` A `TypeAdapter` for `Byte` that supports unsigned values up to 255.
    - `BYTE_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Byte` using the `BYTE` adapter.
    - `SHORT`: `TypeAdapter<Number>` A `TypeAdapter` for `Short` that supports unsigned values up to 65535.
    - `SHORT_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Short` using the `SHORT` adapter.
    - `INTEGER`: `TypeAdapter<Number>` A `TypeAdapter` for `Integer` that reads and writes JSON numbers.
    - `INTEGER_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Integer` using the `INTEGER` adapter.
    - `ATOMIC_INTEGER`: `TypeAdapter<AtomicInteger>` A `TypeAdapter` for `AtomicInteger` that reads and writes JSON numbers.
    - `ATOMIC_INTEGER_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `AtomicInteger` using the `ATOMIC_INTEGER` adapter.
    - `ATOMIC_BOOLEAN`: `TypeAdapter<AtomicBoolean>` A `TypeAdapter` for `AtomicBoolean` that reads and writes JSON booleans.
    - `ATOMIC_BOOLEAN_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `AtomicBoolean` using the `ATOMIC_BOOLEAN` adapter.
    - `ATOMIC_INTEGER_ARRAY`: `TypeAdapter<AtomicIntegerArray>` A `TypeAdapter` for `AtomicIntegerArray` that reads and writes JSON arrays of integers.
    - `ATOMIC_INTEGER_ARRAY_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `AtomicIntegerArray` using the `ATOMIC_INTEGER_ARRAY` adapter.
    - `LONG`: `TypeAdapter<Number>` A `TypeAdapter` for `Long` that reads and writes JSON numbers.
    - `FLOAT`: `TypeAdapter<Number>` A `TypeAdapter` for `Float` that reads and writes JSON numbers, ensuring backward compatibility.
    - `DOUBLE`: `TypeAdapter<Number>` A `TypeAdapter` for `Double` that reads and writes JSON numbers.
    - `CHARACTER`: `TypeAdapter<Character>` A `TypeAdapter` for `Character` that reads and writes single-character strings.
    - `CHARACTER_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Character` using the `CHARACTER` adapter.
    - `STRING`: `TypeAdapter<String>` A `TypeAdapter` for `String` that reads and writes JSON strings, coercing booleans to strings for compatibility.
    - `BIG_DECIMAL`: `TypeAdapter<BigDecimal>` A `TypeAdapter` for `BigDecimal` that reads and writes JSON strings as `BigDecimal` values.
    - `BIG_INTEGER`: `TypeAdapter<BigInteger>` A `TypeAdapter` for `BigInteger` that reads and writes JSON strings as `BigInteger` values.
    - `LAZILY_PARSED_NUMBER`: `TypeAdapter<LazilyParsedNumber>` A `TypeAdapter` for `LazilyParsedNumber` that reads and writes JSON strings as `LazilyParsedNumber` values.
    - `STRING_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `String` using the `STRING` adapter.
    - `STRING_BUILDER`: `TypeAdapter<StringBuilder>` A `TypeAdapter` for `StringBuilder` that reads and writes JSON strings as `StringBuilder` values.
    - `STRING_BUILDER_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `StringBuilder` using the `STRING_BUILDER` adapter.
    - `STRING_BUFFER`: `TypeAdapter<StringBuffer>` A `TypeAdapter` for `StringBuffer` that reads and writes JSON strings as `StringBuffer` values.
    - `STRING_BUFFER_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `StringBuffer` using the `STRING_BUFFER` adapter.
    - `URL`: `TypeAdapter<URL>` A `TypeAdapter` for `URL` that reads and writes JSON strings as `URL` values.
    - `URL_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `URL` using the `URL` adapter.
    - `URI`: `TypeAdapter<URI>` A `TypeAdapter` for `URI` that reads and writes JSON strings as `URI` values.
    - `URI_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `URI` using the `URI` adapter.
    - `INET_ADDRESS`: `TypeAdapter<InetAddress>` A `TypeAdapter` for `InetAddress` that reads and writes JSON strings as `InetAddress` values.
    - `INET_ADDRESS_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `InetAddress` using the `INET_ADDRESS` adapter.
    - `UUID`: `TypeAdapter<UUID>` A `TypeAdapter` for `UUID` that reads and writes JSON strings as `UUID` values.
    - `UUID_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `UUID` using the `UUID` adapter.
    - `CURRENCY`: `TypeAdapter<Currency>` A `TypeAdapter` for `Currency` that reads and writes JSON strings as `Currency` values.
    - `CURRENCY_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Currency` using the `CURRENCY` adapter.
    - `CALENDAR`: `TypeAdapter<Calendar>` A `TypeAdapter` for `Calendar` that reads and writes JSON objects as `Calendar` values.
    - `CALENDAR_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Calendar` using the `CALENDAR` adapter.
    - `LOCALE`: `TypeAdapter<Locale>` A `TypeAdapter` for `Locale` that reads and writes JSON strings as `Locale` values.
    - `LOCALE_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `Locale` using the `LOCALE` adapter.
    - `JSON_ELEMENT`: `TypeAdapter<JsonElement>` A `TypeAdapter` for `JsonElement` that reads and writes JSON elements.
    - `JSON_ELEMENT_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for `JsonElement` using the `JSON_ELEMENT` adapter.
    - `ENUM_FACTORY`: `TypeAdapterFactory` A `TypeAdapterFactory` for enums using the `EnumTypeAdapter` factory.
- **Methods**:
    - [`com.google.gson.internal.bind.TypeAdapters.TypeAdapters`](#TypeAdaptersTypeAdapters)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.read`](#TypeAdaptersread)
    - [`com.google.gson.internal.bind.TypeAdapters.write`](#TypeAdapterswrite)
    - [`com.google.gson.internal.bind.TypeAdapters.newFactory`](#TypeAdaptersnewFactory)
    - [`com.google.gson.internal.bind.TypeAdapters.newFactory`](#TypeAdaptersnewFactory)
    - [`com.google.gson.internal.bind.TypeAdapters.newFactory`](#TypeAdaptersnewFactory)
    - [`com.google.gson.internal.bind.TypeAdapters.newFactoryForMultipleTypes`](#TypeAdaptersnewFactoryForMultipleTypes)
    - [`com.google.gson.internal.bind.TypeAdapters.newTypeHierarchyFactory`](#TypeAdaptersnewTypeHierarchyFactory)

**Methods**

---
#### TypeAdapters\.TypeAdapters<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.TypeAdapters}} -->
The `TypeAdapters` constructor is a private method that throws an `UnsupportedOperationException` when invoked.
- **Modifiers**: `private`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method is invoked without any parameters.
    - Upon invocation, it immediately throws an `UnsupportedOperationException`.
- **Output**:
    - The method does not return any value; it only throws an exception.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
This method throws an exception when attempting to serialize a `java.lang.Class` object.
- **Inputs**:
    - `out`: A `JsonWriter` instance used to write JSON data.
    - `value`: A `Class` object that is intended to be serialized.
- **Control Flow**:
    - The method immediately throws an `UnsupportedOperationException`.
    - The exception message indicates that serialization of `java.lang.Class` is not supported and suggests registering a type adapter.
- **Output**:
    - The method does not produce a return value; instead, it throws an exception indicating that serialization is unsupported.
- **Functions called**:
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
This method attempts to deserialize a `java.lang.Class` from a `JsonReader`, but throws an `UnsupportedOperationException` indicating that a type adapter needs to be registered.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `java.lang.Class` is to be deserialized.
- **Control Flow**:
    - The method begins by checking the input `JsonReader` for the expected format.
    - If the method is called, it immediately throws an `UnsupportedOperationException` with a message indicating that a type adapter for `java.lang.Class` is not registered.
- **Output**:
    - The method does not return a value; instead, it throws an exception indicating that deserialization is unsupported.
- **Functions called**:
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `BitSet` from a JSON array representation.
- **Inputs**:
    - `in`: A `JsonReader` instance that reads JSON data.
- **Control Flow**:
    - Begins reading a JSON array using `in.beginArray()`.
    - Initializes a `BitSet` and an index `i` to track the position of bits.
    - Enters a loop that continues until the end of the JSON array is reached.
    - Peeks at the next token type in the JSON input.
    - Uses a switch statement to handle different token types: NUMBER, STRING, and BOOLEAN.
    - For NUMBER and STRING, reads an integer value and determines if it corresponds to a bit being set (1) or not (0).
    - Throws a `JsonSyntaxException` if the integer value is not 0 or 1.
    - For BOOLEAN, directly reads the boolean value.
    - Sets the corresponding bit in the `BitSet` if the value is true.
    - Increments the index `i` for the next bit position.
    - Ends the loop when the end of the array is reached and calls `in.endArray()`.
- **Output**:
    - Returns the populated `BitSet` representing the bits read from the JSON array.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.beginArray`](../../stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.getPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.endArray`](../../stream/JsonReader.java.driver.md#JsonReaderendArray)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the contents of a `BitSet` to a `JsonWriter` as a JSON array.
- **Inputs**:
    - `out`: A `JsonWriter` instance used to write the JSON output.
    - `src`: A `BitSet` instance containing the bits to be written as JSON values.
- **Control Flow**:
    - Begins writing a JSON array using `out.beginArray()`.
    - Iterates over the length of the `BitSet` using a for loop.
    - For each index, retrieves the bit value from `src` using `src.get(i)` and converts it to an integer (1 for true, 0 for false).
    - Writes the integer value to the `JsonWriter` using `out.value(value)`.
    - Ends the JSON array with `out.endArray()`.
- **Output**:
    - The method does not return a value; it writes the JSON representation of the `BitSet` directly to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Boolean` value from a `JsonReader`, handling nulls and string representations.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the Boolean value is read.
- **Control Flow**:
    - Checks the next token in the `JsonReader` using `peek()`.
    - If the token is `NULL`, it reads the null value and returns null.
    - If the token is `STRING`, it reads the string and parses it as a Boolean.
    - If the token is neither NULL nor STRING, it reads the Boolean value directly.
- **Output**:
    - Returns a `Boolean` object, which can be null if the JSON token was NULL, or the parsed Boolean value.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a Boolean value to a `JsonWriter`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `out`: A `JsonWriter` instance where the Boolean value will be written.
    - `value`: The Boolean value to be written to the `JsonWriter`.
- **Control Flow**:
    - The method calls `out.value(value)` to write the Boolean value to the `JsonWriter`.
    - If the `value` is null, it will be written as a null value in the JSON output.
- **Output**:
    - The method does not return a value; it writes the Boolean directly to the `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Boolean` value from a `JsonReader`, handling null values appropriately.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `Boolean` value will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it consumes the null token and returns `null`.
    - If the token is not `NULL`, it reads the next string from the `JsonReader` and converts it to a `Boolean` using `Boolean.valueOf()`.
- **Output**:
    - Returns a `Boolean` object representing the value read from the `JsonReader`, or `null` if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a Boolean value as a string representation to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the Boolean value will be written.
    - `value`: A `Boolean` value that will be converted to a string and written; can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, writes the string 'null' to the `JsonWriter`.
    - If `value` is not null, converts it to a string using `toString()` and writes that string to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes the string representation of the Boolean to the `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `byte` value from a `JsonReader`, handling nulls and ensuring the value is within valid byte range.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the byte value will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is NULL; if so, it reads the null and returns null.
    - Attempts to read the next integer from the `JsonReader`.
    - Catches `NumberFormatException` and throws a `JsonSyntaxException` if the integer cannot be parsed.
    - Validates that the integer is within the range of a byte (0 to 255) and throws a `JsonSyntaxException` if it is not.
    - Returns the integer cast to a byte if all checks pass.
- **Output**:
    - Returns the read byte value as a `Number`, or null if the input was NULL.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Number` value to a `JsonWriter`, converting it to a byte if not null.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the value will be written.
    - `value`: A `Number` instance that will be converted to a byte and written to the `JsonWriter`. It can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, it calls `out.nullValue()` to write a null representation.
    - If `value` is not null, it converts the `value` to a byte using `value.byteValue()` and writes it to the `JsonWriter` using `out.value()`.
- **Output**:
    - This method does not return a value; it writes directly to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `short` value from a `JsonReader`, handling nulls and ensuring the value is within valid range.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `short` value will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`; if so, it reads the null and returns null.
    - Attempts to read the next integer from the `JsonReader`.
    - Catches `NumberFormatException` and throws a `JsonSyntaxException` if the integer cannot be parsed.
    - Validates that the integer is within the range of a `short` (between `Short.MIN_VALUE` and 65535); throws a `JsonSyntaxException` if it is not.
    - Returns the integer cast to a `short`.
- **Output**:
    - Returns the read `short` value or null if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Number` value to a `JsonWriter`, handling null values appropriately.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `Number` value will be written.
    - `value`: A `Number` object that will be written to the `JsonWriter`. It can be null.
- **Control Flow**:
    - The method first checks if the `value` is null.
    - If `value` is null, it calls `out.nullValue()` to write a null representation in JSON.
    - If `value` is not null, it converts the `value` to a short and writes it using `out.value(value.shortValue())`.
- **Output**:
    - This method does not return a value; it writes directly to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Number` from a `JsonReader`, handling null values and number format exceptions.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `Number` will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it reads the null value and returns `null`.
    - Attempts to read the next integer from the `JsonReader`.
    - If a `NumberFormatException` occurs during reading, it throws a `JsonSyntaxException` with the caught exception.
- **Output**:
    - Returns a `Number` read from the `JsonReader`, or `null` if the next token is `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Number` value to a `JsonWriter`, handling null values appropriately.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `Number` value will be written.
    - `value`: A `Number` object that will be written to the `JsonWriter`. It can be null.
- **Control Flow**:
    - The method first checks if the `value` is null.
    - If `value` is null, it calls `out.nullValue()` to write a null representation in JSON.
    - If `value` is not null, it converts the `Number` to an integer using `value.intValue()` and writes it to the `JsonWriter` using `out.value()`.
- **Output**:
    - This method does not return a value; it writes directly to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.LazilyParsedNumber.intValue`](../LazilyParsedNumber.java.driver.md#LazilyParsedNumberintValue)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads an integer from a `JsonReader` and returns it as an `AtomicInteger`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the integer value will be read.
- **Control Flow**:
    - The method attempts to read the next integer from the `JsonReader` using `in.nextInt()`.
    - If the integer is successfully read, it is wrapped in an `AtomicInteger` and returned.
    - If a `NumberFormatException` occurs during the reading process, a `JsonSyntaxException` is thrown, wrapping the original exception.
- **Output**:
    - Returns an `AtomicInteger` containing the integer read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextInt`](../../stream/JsonReader.java.driver.md#JsonReadernextInt)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the integer value from an `AtomicInteger` to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the integer value will be written.
    - `value`: An `AtomicInteger` instance whose integer value will be written to the `JsonWriter`.
- **Control Flow**:
    - The method retrieves the integer value from the `AtomicInteger` using `value.get()`.
    - It then writes this integer value to the provided `JsonWriter` instance using `out.value(...)`.
- **Output**:
    - This method does not return a value; it writes the integer directly to the `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a boolean value from a `JsonReader` and returns it as an `AtomicBoolean`.
- **Inputs**:
    - `in`: A `JsonReader` instance from which the boolean value will be read.
- **Control Flow**:
    - The method calls `in.nextBoolean()` to read the next boolean value from the `JsonReader`.
    - It then wraps the boolean value in an `AtomicBoolean` and returns it.
- **Output**:
    - Returns an `AtomicBoolean` containing the boolean value read from the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../stream/JsonReader.java.driver.md#JsonReadernextBoolean)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the boolean value of an `AtomicBoolean` to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the boolean value will be written.
    - `value`: An `AtomicBoolean` instance whose boolean value will be written to the `JsonWriter`.
- **Control Flow**:
    - The method retrieves the boolean value from the `AtomicBoolean` using `value.get()`.
    - It then writes this boolean value to the provided `JsonWriter` using `out.value(...)`.
- **Output**:
    - This method does not return a value; it writes the boolean directly to the `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads an array of integers from a `JsonReader` and returns it as an `AtomicIntegerArray`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance that reads JSON data, expected to contain an array of integers.
- **Control Flow**:
    - Begins reading an array from the `JsonReader`.
    - Iterates through the elements of the array while there are more elements.
    - Attempts to read each element as an integer and adds it to a list.
    - Catches `NumberFormatException` and throws a `JsonSyntaxException` if the format is invalid.
    - Ends the array reading once all elements are processed.
    - Creates an `AtomicIntegerArray` of the size of the list.
    - Populates the `AtomicIntegerArray` with the integers from the list.
- **Output**:
    - Returns an `AtomicIntegerArray` containing the integers read from the JSON array.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.beginArray`](../../stream/JsonReader.java.driver.md#JsonReaderbeginArray)
    - [`com.google.gson.stream.JsonReader.hasNext`](../../stream/JsonReader.java.driver.md#JsonReaderhasNext)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.stream.JsonReader.endArray`](../../stream/JsonReader.java.driver.md#JsonReaderendArray)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the contents of an `AtomicIntegerArray` to a `JsonWriter` as a JSON array.
- **Inputs**:
    - `out`: A `JsonWriter` instance used to write the JSON output.
    - `value`: An `AtomicIntegerArray` containing the integers to be written to the JSON output.
- **Control Flow**:
    - Begins writing a JSON array by calling `out.beginArray()`.
    - Iterates over each element in the `AtomicIntegerArray` using a for loop.
    - For each index, retrieves the integer value using `value.get(i)` and writes it to the `JsonWriter` using `out.value(...)`.
    - Ends the JSON array by calling `out.endArray()`.
- **Output**:
    - The method does not return a value; it writes the JSON representation of the `AtomicIntegerArray` directly to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beginArray`](../../stream/JsonWriter.java.driver.md#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](../../stream/JsonWriter.java.driver.md#JsonWriterendArray)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Number` from a `JsonReader`, handling null values and number format exceptions.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `Number` will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it reads the null value and returns `null`.
    - If the token is not `NULL`, it attempts to read the next long value.
    - If a `NumberFormatException` occurs during reading, it throws a `JsonSyntaxException`.
- **Output**:
    - Returns a `Number` read from the `JsonReader`, or `null` if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextLong`](../../stream/JsonReader.java.driver.md#JsonReadernextLong)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Number` value to a `JsonWriter`, handling null values appropriately.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `Number` value will be written.
    - `value`: A `Number` object that will be written to the `JsonWriter`. It can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, calls `out.nullValue()` to write a null representation.
    - If `value` is not null, converts it to a long using `value.longValue()` and writes it to the `JsonWriter` using `out.value()`.
- **Output**:
    - This method does not return a value; it writes directly to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.LazilyParsedNumber.longValue`](../LazilyParsedNumber.java.driver.md#LazilyParsedNumberlongValue)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `float` value from a `JsonReader`, returning `null` if the JSON token is `NULL`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the float value is read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL` using `in.peek()`.
    - If the token is `NULL`, it calls `in.nextNull()` and returns `null`.
    - If the token is not `NULL`, it reads the next double value using `in.nextDouble()` and casts it to a float before returning.
- **Output**:
    - Returns a `Number` representing the float value read from the `JsonReader`, or `null` if the token was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../stream/JsonReader.java.driver.md#JsonReadernextDouble)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Number` value to a `JsonWriter`, handling null values and ensuring backward compatibility.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `Number` value will be written.
    - `value`: A `Number` object that represents the value to be written; can be null.
- **Control Flow**:
    - Checks if the `value` is null; if so, it calls `out.nullValue()` to write a null representation.
    - If `value` is not null, it checks if `value` is an instance of `Float`; if not, it converts it to a float using `value.floatValue()`.
    - Finally, it writes the float value to the `JsonWriter` using `out.value(floatNumber)`.
- **Output**:
    - This method does not return a value; it writes the `Number` to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.LazilyParsedNumber.floatValue`](../LazilyParsedNumber.java.driver.md#LazilyParsedNumberfloatValue)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Number` from a `JsonReader`, returning null if the JSON token is null.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `Number` will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it calls `nextNull()` on the `JsonReader` and returns `null`.
    - If it is not `NULL`, it reads the next double value from the `JsonReader` and returns it.
- **Output**:
    - Returns a `Number` representing the double value read from the `JsonReader`, or `null` if the token was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextDouble`](../../stream/JsonReader.java.driver.md#JsonReadernextDouble)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Number` value to a `JsonWriter`, handling null values appropriately.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `Number` value will be written.
    - `value`: A `Number` object that represents the value to be written; can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, calls `out.nullValue()` to write a null representation.
    - If `value` is not null, converts it to a double and writes it to `out` using `out.value(value.doubleValue())`.
- **Output**:
    - This method does not return a value; it writes the `Number` to the `JsonWriter` directly.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.LazilyParsedNumber.doubleValue`](../LazilyParsedNumber.java.driver.md#LazilyParsedNumberdoubleValue)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Character` from a `JsonReader`, ensuring it is a single character string.
- **Inputs**:
    - `in`: A `JsonReader` instance from which the character will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`; if so, it reads the null value and returns null.
    - Reads the next string from the `JsonReader` and checks if its length is exactly 1.
    - If the string length is not 1, it throws a `JsonSyntaxException` with an error message indicating the issue.
    - If the string is valid, it returns the first character of the string.
- **Output**:
    - Returns the `Character` read from the `JsonReader`, or null if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Character` value to a `JsonWriter` as a string.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the character value will be written.
    - `value`: A `Character` object that represents the character to be written.
- **Control Flow**:
    - Checks if the `value` is `null`.
    - If `value` is `null`, writes `null` to the `JsonWriter`.
    - If `value` is not `null`, converts it to a string using `String.valueOf(value)` and writes it to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes the character representation directly to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a value from a `JsonReader`, handling nulls and coercing booleans to strings.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the JSON value will be read.
- **Control Flow**:
    - Checks the next token in the `JsonReader` using `peek()`.
    - If the token is `NULL`, it reads the null value and returns null.
    - If the token is `BOOLEAN`, it reads the boolean value and converts it to a string.
    - For any other token type, it reads the string value directly from the `JsonReader`.
- **Output**:
    - Returns a `String` representation of the value read from the `JsonReader`, or null if the value was null.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextBoolean`](../../stream/JsonReader.java.driver.md#JsonReadernextBoolean)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a string value to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the string value will be written.
    - `value`: The string value to be written to the `JsonWriter`.
- **Control Flow**:
    - The method calls the `value` method on the `JsonWriter` instance, passing the string value as an argument.
    - If the `JsonWriter` encounters an issue while writing, it throws an `IOException`.
- **Output**:
    - This method does not return a value; it writes the string directly to the `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `BigDecimal` value from a `JsonReader`, handling nulls and parsing errors.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `BigDecimal` value will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is NULL; if so, it reads the null and returns null.
    - If the token is not NULL, it reads the next string from the `JsonReader`.
    - Attempts to parse the string into a `BigDecimal` using `NumberLimits.parseBigDecimal`.
    - If parsing fails due to a `NumberFormatException`, it throws a `JsonSyntaxException` with a descriptive error message.
- **Output**:
    - Returns the parsed `BigDecimal` value or null if the input was NULL.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.internal.NumberLimits.parseBigDecimal`](../NumberLimits.java.driver.md#NumberLimitsparseBigDecimal)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `BigDecimal` value to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `BigDecimal` value will be written.
    - `value`: The `BigDecimal` value to be written to the `JsonWriter`.
- **Control Flow**:
    - The method calls `out.value(value)` to write the `BigDecimal` value directly to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes the `BigDecimal` to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `BigInteger` from a `JsonReader`, handling null values and parsing errors.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `BigInteger` value will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it reads the null value and returns null.
    - If not `NULL`, it reads the next string from the `JsonReader`.
    - Attempts to parse the string into a `BigInteger` using `NumberLimits.parseBigInteger(s)`.
    - If parsing fails, it throws a `JsonSyntaxException` with a descriptive error message.
- **Output**:
    - Returns the parsed `BigInteger` or null if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.internal.NumberLimits.parseBigInteger`](../NumberLimits.java.driver.md#NumberLimitsparseBigInteger)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `BigInteger` value to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `BigInteger` value will be written.
    - `value`: The `BigInteger` value to be written to the `JsonWriter`.
- **Control Flow**:
    - The method directly calls the `value` method of the `JsonWriter` instance, passing the `BigInteger` value as an argument.
- **Output**:
    - This method does not return a value; it writes the `BigInteger` to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `LazilyParsedNumber` from a `JsonReader`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the number will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it reads the null value and returns null.
    - If it is not `NULL`, it reads the next string from the `JsonReader` and creates a new `LazilyParsedNumber` instance with that string.
- **Output**:
    - Returns a `LazilyParsedNumber` object if a valid number string is read, or null if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `LazilyParsedNumber` value to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the value will be written.
    - `value`: A `LazilyParsedNumber` instance that represents the number to be written.
- **Control Flow**:
    - The method directly calls the `value` method of the `JsonWriter` instance, passing the `LazilyParsedNumber` as an argument.
- **Output**:
    - This method does not return a value; it writes the `LazilyParsedNumber` to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `String` from a `JsonReader` and returns it as a `StringBuilder`.
- **Inputs**:
    - `in`: A `JsonReader` instance from which the method reads the JSON data.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it consumes the `NULL` token and returns `null`.
    - If it is not `NULL`, it reads the next string from the `JsonReader` and returns it wrapped in a `StringBuilder`.
- **Output**:
    - Returns a `StringBuilder` containing the read string, or `null` if the next token was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the string representation of a `StringBuilder` to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the string value will be written.
    - `value`: A `StringBuilder` instance whose string representation will be written to the `JsonWriter`.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, writes a null value to the `JsonWriter`.
    - If `value` is not null, converts it to a string and writes it to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes directly to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `StringBuffer` from a `JsonReader` based on the JSON input.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance that provides the JSON input to read from.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it consumes the `NULL` token and returns `null`.
    - If it is not `NULL`, it reads the next string from the `JsonReader` and returns it wrapped in a `StringBuffer`.
- **Output**:
    - Returns a `StringBuffer` containing the next string from the `JsonReader`, or `null` if the next token is `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the string representation of a `StringBuffer` to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the string representation will be written.
    - `value`: A `StringBuffer` object whose string representation is to be written; can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, writes a null value to the `JsonWriter`.
    - If `value` is not null, converts it to a string and writes it to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes the string representation of the `StringBuffer` to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `URL` from a `JsonReader`, returning null for JSON null values.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `URL` is read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it reads the null value and returns null.
    - If not, it reads the next string from the `JsonReader`.
    - If the string equals 'null', it returns null.
    - Otherwise, it creates and returns a new `URL` object from the string.
- **Output**:
    - Returns a `URL` object created from the string read from the `JsonReader`, or null if the input was null or the string was 'null'.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `URL` value to a `JsonWriter` in its external form.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `URL` value will be written.
    - `value`: A `URL` object that needs to be serialized; can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, writes a null value to the `JsonWriter`.
    - If `value` is not null, converts it to its external form using `toExternalForm()` and writes it to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes the serialized representation of the `URL` to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `URI` from a `JsonReader`, handling null values and URI syntax exceptions.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `URI` will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it reads the null value and returns `null`.
    - If not `NULL`, it reads the next string from the `JsonReader`.
    - If the string is 'null', it returns `null`.
    - Otherwise, it attempts to create a new `URI` from the string.
    - If a `URISyntaxException` occurs, it throws a `JsonIOException`.
- **Output**:
    - Returns a `URI` object created from the string read from the `JsonReader`, or `null` if the input was `NULL` or the string was 'null'.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `URI` value to a `JsonWriter` as an ASCII string.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `URI` value will be written.
    - `value`: A `URI` object that needs to be serialized; can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, writes a null value to the `JsonWriter`.
    - If `value` is not null, converts it to its ASCII string representation using `toASCIIString()` and writes it to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes the serialized representation of the `URI` to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads an `InetAddress` from a `JsonReader`.
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `InetAddress` will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it consumes the `NULL` token and returns `null`.
    - If it is not `NULL`, it reads the next string from the `JsonReader`.
    - Uses `InetAddress.getByName` to convert the string to an `InetAddress` object.
    - Returns the created `InetAddress` object.
- **Output**:
    - Returns the `InetAddress` object corresponding to the string read from the `JsonReader`, or `null` if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the string representation of an `InetAddress` to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `InetAddress` value will be written.
    - `value`: An `InetAddress` object that represents an IP address, which can be null.
- **Control Flow**:
    - Checks if the `value` is null.
    - If `value` is null, writes a null value to the `JsonWriter`.
    - If `value` is not null, retrieves the host address string using `value.getHostAddress()` and writes it to the `JsonWriter`.
- **Output**:
    - The method does not return a value; it writes the host address of the `InetAddress` to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `UUID` from a `JsonReader` and handles potential parsing errors.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the `UUID` will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is `NULL`.
    - If it is `NULL`, it reads the null value and returns `null`.
    - If not `NULL`, it reads the next string from the `JsonReader`.
    - Attempts to convert the string to a `UUID` using `UUID.fromString(s)`.
    - If the string is not a valid UUID format, it catches the `IllegalArgumentException` and throws a `JsonSyntaxException` with a descriptive error message.
- **Output**:
    - Returns the parsed `UUID` or `null` if the input was `NULL`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `UUID` value to a `JsonWriter` as a string.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `UUID` value will be written.
    - `value`: A `UUID` object that needs to be serialized; can be null.
- **Control Flow**:
    - The method checks if the `value` is null.
    - If `value` is null, it writes a null value to the `JsonWriter`.
    - If `value` is not null, it converts the `UUID` to a string using `toString()` and writes it to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes the `UUID` representation directly to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Currency` object from a JSON input using a `JsonReader`.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance that reads JSON input.
- **Control Flow**:
    - Calls `in.nextString()` to read the next string from the JSON input.
    - Attempts to convert the string to a `Currency` instance using `Currency.getInstance(s)`.
    - Catches `IllegalArgumentException` if the string does not represent a valid currency code.
    - Throws a `JsonSyntaxException` with a descriptive error message if the conversion fails.
- **Output**:
    - Returns a `Currency` object corresponding to the string read from the JSON input, or throws a `JsonSyntaxException` if the string is not a valid currency code.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the currency code of a `Currency` object to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the currency code will be written.
    - `value`: A `Currency` object whose currency code is to be written.
- **Control Flow**:
    - The method calls `out.value()` to write the currency code obtained from `value.getCurrencyCode()`.
    - If the `value` is null, the method will not write anything, as it is expected to be null-safe.
- **Output**:
    - This method does not return a value; it writes the currency code directly to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Calendar` object from a JSON representation.
- **Inputs**:
    - `in`: A `JsonReader` instance that reads the JSON input.
- **Control Flow**:
    - Checks if the next token is NULL; if so, it reads the null and returns null.
    - Begins reading a JSON object.
    - Initializes variables for year, month, day, hour, minute, and second.
    - Enters a loop that continues until the end of the JSON object is reached.
    - Reads the name of each property and its corresponding integer value.
    - Uses a switch statement to assign values to the respective variables based on the property name.
    - Ends the JSON object reading.
    - Creates and returns a new `GregorianCalendar` instance using the collected values.
- **Output**:
    - Returns a `GregorianCalendar` object initialized with the parsed year, month, day, hour, minute, and second, or null if the input was NULL.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../stream/JsonReader.java.driver.md#JsonReaderbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.stream.JsonReader.nextInt`](../../stream/JsonReader.java.driver.md#JsonReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes a `Calendar` object to a `JsonWriter` in JSON format.
- **Inputs**:
    - `out`: A `JsonWriter` instance used to write the JSON output.
    - `value`: A `Calendar` object that contains the date and time information to be written.
- **Control Flow**:
    - Checks if the `value` is null; if so, it writes a null value to the `JsonWriter` and returns.
    - Begins writing a JSON object.
    - Writes the year, month, day of the month, hour of the day, minute, and second from the `Calendar` object to the `JsonWriter` as key-value pairs.
    - Ends the JSON object.
- **Output**:
    - The method does not return a value; it writes the serialized representation of the `Calendar` object directly to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.stream.JsonWriter.name`](../../stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.read<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.read}} -->
Reads a `Locale` from a `JsonReader` by parsing a string representation of the locale.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `in`: A `JsonReader` instance from which the locale string will be read.
- **Control Flow**:
    - Checks if the next token in the `JsonReader` is NULL; if so, it reads the null value and returns null.
    - Reads the next string from the `JsonReader`, which is expected to be a locale string.
    - Uses a `StringTokenizer` to split the locale string into language, country, and variant components.
    - Constructs and returns a new `Locale` object based on the parsed components, handling cases where country or variant may be absent.
- **Output**:
    - Returns a `Locale` object constructed from the parsed language, country, and variant, or null if the input was NULL.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.stream.JsonReader.nextNull`](../../stream/JsonReader.java.driver.md#JsonReadernextNull)
    - [`com.google.gson.stream.JsonReader.nextString`](../../stream/JsonReader.java.driver.md#JsonReadernextString)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.write<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.write}} -->
Writes the string representation of a `Locale` object to a `JsonWriter`.
- **Inputs**:
    - `out`: A `JsonWriter` instance where the `Locale` value will be written.
    - `value`: A `Locale` object that needs to be serialized; can be null.
- **Control Flow**:
    - The method checks if the `value` is null.
    - If `value` is null, it writes a null value to the `JsonWriter`.
    - If `value` is not null, it converts the `Locale` to its string representation using `toString()` and writes it to the `JsonWriter`.
- **Output**:
    - This method does not return a value; it writes directly to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.newFactory<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.newFactory}} -->
Creates a new `TypeAdapterFactory` that produces a specific `TypeAdapter` for a given type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `type`: A `TypeToken` representing the type for which the `TypeAdapter` is created.
    - `typeAdapter`: A `TypeAdapter` instance that will be used to serialize and deserialize the specified type.
- **Control Flow**:
    - The method defines and returns an anonymous inner class that implements the `TypeAdapterFactory` interface.
    - Inside the `create` method of the factory, it checks if the provided `typeToken` matches the specified `type`.
    - If they match, it returns the `typeAdapter` cast to the appropriate type; otherwise, it returns null.
- **Output**:
    - Returns a `TypeAdapterFactory` that can create a `TypeAdapter` for the specified type.
- **Functions called**:
    - [`com.google.gson.internal.LazilyParsedNumber.equals`](../LazilyParsedNumber.java.driver.md#LazilyParsedNumberequals)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.newFactory<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.newFactory}} -->
Creates a new `TypeAdapterFactory` that produces a specific `TypeAdapter` for a given type.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `type`: A `Class<TT>` object representing the type for which the `TypeAdapter` is created.
    - `typeAdapter`: A `TypeAdapter<TT>` instance that defines how to serialize and deserialize the specified type.
- **Control Flow**:
    - The method returns a new instance of an anonymous class that implements `TypeAdapterFactory`.
    - Inside the `create` method of the factory, it checks if the raw type of the provided `TypeToken<T>` matches the specified `type`.
    - If the types match, it casts and returns the provided `typeAdapter`; otherwise, it returns null.
    - The `toString` method provides a string representation of the factory, including the type and adapter information.
- **Output**:
    - Returns a `TypeAdapterFactory` that can create `TypeAdapter` instances for the specified type, or null if the type does not match.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.newFactory<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.newFactory}} -->
Creates a `TypeAdapterFactory` for a specified unboxed and boxed type with a given `TypeAdapter`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `unboxed`: A `Class` object representing the unboxed type.
    - `boxed`: A `Class` object representing the boxed type.
    - `typeAdapter`: A `TypeAdapter` instance that handles serialization and deserialization for the specified type.
- **Control Flow**:
    - Defines an anonymous inner class that implements `TypeAdapterFactory`.
    - Overrides the `create` method to check if the raw type of the provided `TypeToken` matches either the unboxed or boxed class.
    - If a match is found, it returns the provided `typeAdapter`, otherwise it returns null.
    - Overrides the `toString` method to provide a string representation of the factory.
- **Output**:
    - Returns a `TypeAdapterFactory` that can create `TypeAdapter` instances for the specified unboxed and boxed types.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.newFactoryForMultipleTypes<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.newFactoryForMultipleTypes}} -->
Creates a `TypeAdapterFactory` for a base type and its subclass, using a specified `TypeAdapter`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `base`: The base class type for which the factory is created.
    - `sub`: A subclass of the base class.
    - `typeAdapter`: The `TypeAdapter` to be used for serialization and deserialization.
- **Control Flow**:
    - The method defines an anonymous inner class that implements `TypeAdapterFactory`.
    - The `create` method checks if the raw type of the provided `TypeToken` matches either the base class or the subclass.
    - If there is a match, it returns the provided `TypeAdapter`, otherwise it returns null.
- **Output**:
    - Returns a `TypeAdapterFactory` that can create `TypeAdapter` instances for the specified base and subclass types.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)


---
#### TypeAdapters\.newTypeHierarchyFactory<!-- {{#callable:com.google.gson.internal.bind.TypeAdapters.newTypeHierarchyFactory}} -->
Creates a `TypeAdapterFactory` that can handle all subtypes of a specified class using a provided `TypeAdapter`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `clazz`: The class type for which the factory will create type adapters.
    - `typeAdapter`: The `TypeAdapter` instance that will be used for serialization and deserialization.
- **Control Flow**:
    - The method defines an anonymous inner class that implements `TypeAdapterFactory`.
    - The `create` method checks if the requested type is assignable from the specified class.
    - If the type is not assignable, it returns null.
    - If it is assignable, it creates and returns a new `TypeAdapter` that uses the provided `typeAdapter` for reading and writing.
    - The [`read`](../../TypeAdapter.java.driver.md#TypeAdapterread) method of the inner `TypeAdapter` checks if the result is an instance of the requested type and throws a `JsonSyntaxException` if it is not.
- **Output**:
    - Returns a `TypeAdapterFactory` that can create `TypeAdapter` instances for all subtypes of the specified class.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.reflect.TypeToken.isAssignableFrom`](../../reflect/TypeToken.java.driver.md#TypeTokenisAssignableFrom)
    - [`com.google.gson.TypeAdapter.write`](../../TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.TypeAdapter.read`](../../TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
- **See also**: [`com.google.gson.internal.bind.TypeAdapters`](#TypeAdapters)  (Base Class)



