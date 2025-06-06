# Purpose
The provided Java source code file is part of the Google Gson library, specifically within the `com.google.gson.internal` package. It defines a utility class named [`Streams`](#StreamsStreams) that facilitates reading and writing JSON data using streams. The class is designed to handle JSON parse trees, providing methods to parse JSON data from a `JsonReader` into a `JsonElement` and to write a `JsonElement` to a `JsonWriter`. The [`parse`](#Streamsparse) method is robust, handling various exceptions such as `EOFException`, `MalformedJsonException`, and `IOException`, and it returns a `JsonNull` for empty documents to maintain compatibility with earlier JSON versions. The [`write`](#Streamswrite) method recursively writes JSON elements, ensuring that complex JSON structures are correctly serialized.

Additionally, the [`Streams`](#StreamsStreams) class includes a nested static class [`AppendableWriter`](#AppendableWriterAppendableWriter), which adapts an `Appendable` object to be used as a `Writer`. This is particularly useful for scenarios where an `Appendable` needs to be passed to APIs expecting a `Writer`. The [`AppendableWriter`](#AppendableWriterAppendableWriter) class optimizes performance by overriding methods to avoid unnecessary creation of strings or character arrays, and it includes a private static class `CurrentWrite` to manage mutable character sequences. Overall, the [`Streams`](#StreamsStreams) class provides essential functionality for JSON stream processing within the Gson library, focusing on efficient and error-tolerant JSON parsing and writing.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonIOException`
- `com.google.gson.JsonNull`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.internal.bind.TypeAdapters`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.EOFException`
- `java.io.IOException`
- `java.io.Writer`
- `java.util.Objects`


# Classes

---
### Streams<!-- {{#class:com.google.gson.internal.Streams}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `Streams` class is a utility class in the Gson library that provides static methods for parsing JSON data from a `JsonReader` into a `JsonElement` and writing a `JsonElement` to a `JsonWriter`. It also includes a method to adapt an `Appendable` to a `Writer` using an inner class `AppendableWriter`, which optimizes writing operations by avoiding unnecessary creation of strings or character arrays. The class is designed to be non-instantiable, as indicated by its private constructor that throws an `UnsupportedOperationException`.
- **Methods**:
    - [`com.google.gson.internal.Streams.Streams`](#StreamsStreams)
    - [`com.google.gson.internal.Streams.parse`](#Streamsparse)
    - [`com.google.gson.internal.Streams.write`](#Streamswrite)
    - [`com.google.gson.internal.Streams.writerForAppendable`](#StreamswriterForAppendable)

**Methods**

---
#### Streams\.Streams<!-- {{#callable:com.google.gson.internal.Streams.Streams}} -->
The `Streams` constructor is private and throws an `UnsupportedOperationException` to prevent instantiation of the class.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The constructor is defined as private, which restricts its access to within the class itself.
    - Upon invocation, the constructor immediately throws an `UnsupportedOperationException`.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.internal.Streams`](#Streams)  (Base Class)


---
#### Streams\.parse<!-- {{#callable:com.google.gson.internal.Streams.parse}} -->
The `parse` method reads a JSON element from a `JsonReader` and returns it as a `JsonElement`, handling various exceptions that may occur during parsing.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `reader`: A `JsonReader` object from which the JSON element is to be read.
- **Control Flow**:
    - Initialize a boolean variable `isEmpty` to true to track if the document is empty.
    - Attempt to peek at the next token in the `JsonReader` to check if the document is empty, setting `isEmpty` to false if successful.
    - Use `TypeAdapters.JSON_ELEMENT.read(reader)` to read and return the JSON element from the `JsonReader`.
    - Catch `EOFException` to handle empty documents by returning `JsonNull.INSTANCE` if `isEmpty` is true, otherwise throw a `JsonSyntaxException`.
    - Catch `MalformedJsonException` and throw a `JsonSyntaxException`.
    - Catch `IOException` and throw a `JsonIOException`.
    - Catch `NumberFormatException` and throw a `JsonSyntaxException`.
- **Output**:
    - Returns a `JsonElement` representing the parsed JSON data, or `JsonNull.INSTANCE` if the document is empty.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.internal.Excluder.create.read`](Excluder.java.driver.md#createread)
- **See also**: [`com.google.gson.internal.Streams`](#Streams)  (Base Class)


---
#### Streams\.write<!-- {{#callable:com.google.gson.internal.Streams.write}} -->
The [`write`](Excluder.java.driver.md#createwrite) method serializes a `JsonElement` to a `JsonWriter` using a type adapter.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `element`: The `JsonElement` to be serialized and written to the `JsonWriter`.
    - `writer`: The `JsonWriter` to which the `JsonElement` will be written.
- **Control Flow**:
    - The method calls `TypeAdapters.JSON_ELEMENT.write` with the provided `writer` and `element` as arguments.
- **Output**:
    - The method does not return any value; it writes the serialized JSON representation of the `JsonElement` to the `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.create.write`](Excluder.java.driver.md#createwrite)
- **See also**: [`com.google.gson.internal.Streams`](#Streams)  (Base Class)


---
#### Streams\.writerForAppendable<!-- {{#callable:com.google.gson.internal.Streams.writerForAppendable}} -->
The `writerForAppendable` method returns a `Writer` for a given `Appendable`, either by casting it if it's already a `Writer` or by wrapping it in an `AppendableWriter`.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `appendable`: An instance of `Appendable` that needs to be adapted to a `Writer`.
- **Control Flow**:
    - Check if the `appendable` is an instance of `Writer`.
    - If true, cast the `appendable` to `Writer` and return it.
    - If false, create a new `AppendableWriter` with the `appendable` and return it.
- **Output**:
    - A `Writer` instance that corresponds to the provided `Appendable`.
- **See also**: [`com.google.gson.internal.Streams`](#Streams)  (Base Class)



---
### AppendableWriter<!-- {{#class:com.google.gson.internal.Streams.AppendableWriter}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `AppendableWriter` class is a private static final class within the `Streams` class that adapts an `Appendable` object to be used as a `Writer`. It overrides several methods from the `Writer` class to provide efficient writing operations by directly appending characters, strings, and character sequences to the underlying `Appendable` without unnecessary conversions. The class also includes an inner static class `CurrentWrite` that implements `CharSequence` to manage a mutable character array, optimizing the writing process by avoiding the creation of new strings or character arrays.
- **Fields**:
    - `appendable`: `Appendable` A final field that holds the `Appendable` object to which data is written.
    - `currentWrite`: `CurrentWrite` An instance of `CurrentWrite` used to manage the current character array being written.
- **Methods**:
    - [`com.google.gson.internal.Streams.AppendableWriter.AppendableWriter`](#AppendableWriterAppendableWriter)
    - [`com.google.gson.internal.Streams.AppendableWriter.write`](#AppendableWriterwrite)
    - [`com.google.gson.internal.Streams.AppendableWriter.flush`](#AppendableWriterflush)
    - [`com.google.gson.internal.Streams.AppendableWriter.close`](#AppendableWriterclose)
    - [`com.google.gson.internal.Streams.AppendableWriter.write`](#AppendableWriterwrite)
    - [`com.google.gson.internal.Streams.AppendableWriter.write`](#AppendableWriterwrite)
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](#AppendableWriterappend)
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](#AppendableWriterappend)
- **Extends/Implements**:
    - `Writer`

**Methods**

---
#### AppendableWriter\.AppendableWriter<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.AppendableWriter}} -->
The `AppendableWriter` constructor initializes a new instance of the `AppendableWriter` class with a specified `Appendable` object.
- **Inputs**:
    - `appendable`: An `Appendable` object that the `AppendableWriter` will use to perform write operations.
- **Control Flow**:
    - The constructor takes an `Appendable` object as a parameter.
    - It assigns the provided `Appendable` object to the instance variable `appendable`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `AppendableWriter` class.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)


---
#### AppendableWriter\.write<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.write}} -->
The `write` method writes a portion of a character array to an `Appendable` object using specified offset and length.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `chars`: The character array containing the data to be written.
    - `offset`: The starting position in the character array from which to begin writing.
    - `length`: The number of characters to write from the character array.
- **Control Flow**:
    - The method sets the character array `chars` to the `currentWrite` object using [`setChars`](#CurrentWritesetChars) method.
    - It then appends the specified portion of the character array to the `appendable` object using the [`append`](#AppendableWriterappend) method, with the range defined by `offset` and `offset + length`.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.setChars`](#CurrentWritesetChars)
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](#AppendableWriterappend)
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)


---
#### AppendableWriter\.flush<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.flush}} -->
The `flush` method in `AppendableWriter` is an overridden method that performs no operation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is overridden from the `Writer` class.
    - It contains an empty body, meaning it does not perform any actions when called.
- **Output**:
    - The method does not return any value or perform any operations.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)


---
#### AppendableWriter\.close<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.close}} -->
The `close` method is an overridden method that performs no operations when called.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is defined as an override, indicating it is implementing or modifying behavior from a superclass or interface.
    - The method body is empty, meaning it does not perform any actions or operations when invoked.
- **Output**:
    - The method does not return any value or perform any actions.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)


---
#### AppendableWriter\.write<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.write}} -->
The `write` method appends a single character, represented by an integer, to an `Appendable` object.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `i`: An integer representing the character to be appended, which is cast to a char.
- **Control Flow**:
    - The method casts the integer input `i` to a character.
    - It appends this character to the `appendable` object using the [`append`](#AppendableWriterappend) method.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](#AppendableWriterappend)
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)


---
#### AppendableWriter\.write<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.write}} -->
The `write` method writes a substring of the given string to an `Appendable` object, ensuring the string is not null.
- **Modifiers**: `public`, `void`
- **Inputs**:
    - `str`: The string to be written to the appendable object.
    - `off`: The starting offset in the string from which to begin writing.
    - `len`: The number of characters to write from the string.
- **Control Flow**:
    - The method first checks that the input string `str` is not null using `Objects.requireNonNull(str)`, which throws a `NullPointerException` if `str` is null.
    - It then appends the substring of `str` from index `off` to `off + len` to the `appendable` object.
- **Output**:
    - This method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](#AppendableWriterappend)
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)


---
#### AppendableWriter\.append<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.append}} -->
The [`append`](#AppendableWriterappend) method appends a given `CharSequence` to an `Appendable` and returns the current `Writer` instance.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `csq`: A `CharSequence` to be appended to the `Appendable`.
- **Control Flow**:
    - The method calls the [`append`](#AppendableWriterappend) method on the `appendable` object, passing the `csq` parameter.
    - The method returns the current instance of `Writer` (i.e., `this`).
- **Output**:
    - The method returns the current `Writer` instance after appending the `CharSequence`.
- **Functions called**:
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](#AppendableWriterappend)
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)


---
#### AppendableWriter\.append<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.append}} -->
The [`append`](#AppendableWriterappend) method appends a subsequence of a given `CharSequence` to an `Appendable` and returns the current `Writer` instance.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `csq`: The `CharSequence` from which a subsequence will be appended.
    - `start`: The starting index (inclusive) of the subsequence to be appended.
    - `end`: The ending index (exclusive) of the subsequence to be appended.
- **Control Flow**:
    - The method calls the [`append`](#AppendableWriterappend) method on the `appendable` object, passing the `csq`, `start`, and `end` parameters to append the specified subsequence.
    - The method then returns the current instance of `Writer`.
- **Output**:
    - The method returns the current `Writer` instance after appending the specified subsequence.
- **Functions called**:
    - [`com.google.gson.internal.Streams.AppendableWriter.append`](#AppendableWriterappend)
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter`](#Streams.AppendableWriter)  (Base Class)



---
### CurrentWrite<!-- {{#class:com.google.gson.internal.Streams.AppendableWriter.CurrentWrite}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `CurrentWrite` class is a private static inner class that implements the `CharSequence` interface, providing a mutable character sequence that points to a single `char[]`. It is used within the `AppendableWriter` class to efficiently handle character sequences without unnecessary creation of strings or character arrays, optimizing performance for writing operations.
- **Fields**:
    - `chars`: `char[]` A character array that holds the current sequence of characters.
    - `cachedString`: `String` A cached string representation of the character array to optimize repeated calls to `toString()`.
- **Methods**:
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.setChars`](#CurrentWritesetChars)
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.length`](#CurrentWritelength)
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.charAt`](#CurrentWritecharAt)
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.subSequence`](#CurrentWritesubSequence)
    - [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.toString`](#CurrentWritetoString)
- **Extends/Implements**:
    - `CharSequence`

**Methods**

---
#### CurrentWrite\.setChars<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.setChars}} -->
The `setChars` method assigns a new character array to the `chars` field and resets the `cachedString` field to null.
- **Inputs**:
    - `chars`: A character array to be assigned to the `chars` field.
- **Control Flow**:
    - Assigns the input character array `chars` to the instance variable `this.chars`.
    - Sets the `cachedString` field to null, indicating that any cached string representation is invalidated.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite`](#Streams.AppendableWriter.CurrentWrite)  (Base Class)


---
#### CurrentWrite\.length<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.length}} -->
The `length` method returns the length of the `chars` array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly accesses the `chars` array and returns its length using the `length` property of the array.
- **Output**:
    - The method returns an integer representing the number of elements in the `chars` array.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite`](#Streams.AppendableWriter.CurrentWrite)  (Base Class)


---
#### CurrentWrite\.charAt<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.charAt}} -->
The `charAt` method returns the character at a specified index from a character array.
- **Modifiers**: `public`
- **Inputs**:
    - `i`: The index of the character to be returned from the character array.
- **Control Flow**:
    - Access the character at the specified index `i` from the `chars` array.
    - Return the character at the specified index.
- **Output**:
    - The method returns the character located at the specified index `i` in the `chars` array.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite`](#Streams.AppendableWriter.CurrentWrite)  (Base Class)


---
#### CurrentWrite\.subSequence<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.subSequence}} -->
The `subSequence` method returns a new `CharSequence` that is a subsequence of the current character array from the specified start index to the end index.
- **Modifiers**: `public`
- **Inputs**:
    - `start`: The starting index of the subsequence, inclusive.
    - `end`: The ending index of the subsequence, exclusive.
- **Control Flow**:
    - The method creates a new `String` object using the `chars` array, starting from the `start` index and spanning `end - start` characters.
- **Output**:
    - A `CharSequence` representing the specified subsequence of the character array.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite`](#Streams.AppendableWriter.CurrentWrite)  (Base Class)


---
#### CurrentWrite\.toString<!-- {{#callable:com.google.gson.internal.Streams.AppendableWriter.CurrentWrite.toString}} -->
The `toString` method returns a string representation of the current character sequence, caching the result for future calls.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if `cachedString` is null.
    - If `cachedString` is null, create a new `String` from the `chars` array and assign it to `cachedString`.
    - Return the `cachedString`.
- **Output**:
    - A `String` that represents the current character sequence.
- **See also**: [`com.google.gson.internal.Streams.AppendableWriter.CurrentWrite`](#Streams.AppendableWriter.CurrentWrite)  (Base Class)



