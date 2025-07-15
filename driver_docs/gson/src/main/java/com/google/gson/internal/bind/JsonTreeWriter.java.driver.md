# Purpose
The [`JsonTreeWriter`](#JsonTreeWriterJsonTreeWriter) class is a specialized implementation of the `JsonWriter` that constructs a JSON tree structure in memory using Google's Gson library. This class is designed to facilitate the creation of JSON elements such as `JsonObject`, `JsonArray`, `JsonPrimitive`, and `JsonNull` by providing methods to begin and end JSON objects and arrays, as well as to add values of various types (e.g., strings, numbers, booleans) to these structures. The class maintains an internal stack to keep track of the current position within the JSON structure, ensuring that elements are added in a valid hierarchical order. The [`JsonTreeWriter`](#JsonTreeWriterJsonTreeWriter) does not write JSON to an output stream but instead builds a `JsonElement` that represents the entire JSON structure, which can be retrieved using the `get()` method once the writing process is complete.

The class includes several key components, such as a stack to manage the current context within the JSON structure, a `pendingName` to temporarily hold the name of a JSON object property, and a `product` to store the final JSON element. It overrides methods from `JsonWriter` to handle the addition of different data types and to manage the structure of JSON objects and arrays. The class also enforces certain constraints, such as disallowing NaN and infinite values unless the writer is in lenient mode, and it throws exceptions when operations are attempted in an invalid state, such as adding a name without an enclosing object. This implementation provides a robust mechanism for programmatically constructing JSON data in a structured and controlled manner.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.JsonArray`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonNull`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.io.Writer`
- `java.util.ArrayList`
- `java.util.List`
- `java.util.Objects`


# Classes

---
### JsonTreeWriter<!-- {{#class:com.google.gson.internal.bind.JsonTreeWriter}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonTreeWriter` class is a specialized implementation of `JsonWriter` that constructs a JSON tree structure in memory, represented by `JsonElement` objects. It provides methods to begin and end JSON arrays and objects, set names for JSON object members, and add various types of values, including strings, booleans, numbers, and nulls. The class maintains a stack to track the current position in the JSON structure being built, and it throws exceptions for invalid operations, such as attempting to write a name outside of an object context or adding values to a closed writer. The resulting JSON structure can be retrieved using the `get` method once writing is complete.
- **Fields**:
    - `UNWRITABLE_WRITER`: `Writer` A static `Writer` instance that throws an `AssertionError` for all operations, used to initialize the superclass.
    - `SENTINEL_CLOSED`: `JsonPrimitive` A static `JsonPrimitive` used to mark the writer as closed, causing subsequent operations to fail.
    - `stack`: `List<JsonElement>` A list of `JsonElement` objects representing the current state of the JSON structure being built, from outermost to innermost.
    - `pendingName`: `String` A string holding the name for the next JSON object value, if applicable.
    - `product`: `JsonElement` The `JsonElement` representing the complete JSON structure constructed by this writer.
- **Methods**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.write`](#JsonTreeWriterwrite)
    - [`com.google.gson.internal.bind.JsonTreeWriter.flush`](#JsonTreeWriterflush)
    - [`com.google.gson.internal.bind.JsonTreeWriter.close`](#JsonTreeWriterclose)
    - [`com.google.gson.internal.bind.JsonTreeWriter.JsonTreeWriter`](#JsonTreeWriterJsonTreeWriter)
    - [`com.google.gson.internal.bind.JsonTreeWriter.get`](#JsonTreeWriterget)
    - [`com.google.gson.internal.bind.JsonTreeWriter.peek`](#JsonTreeWriterpeek)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginArray`](#JsonTreeWriterbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.endArray`](#JsonTreeWriterendArray)
    - [`com.google.gson.internal.bind.JsonTreeWriter.beginObject`](#JsonTreeWriterbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.endObject`](#JsonTreeWriterendObject)
    - [`com.google.gson.internal.bind.JsonTreeWriter.name`](#JsonTreeWritername)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.value`](#JsonTreeWritervalue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.nullValue`](#JsonTreeWriternullValue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.jsonValue`](#JsonTreeWriterjsonValue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.flush`](#JsonTreeWriterflush)
    - [`com.google.gson.internal.bind.JsonTreeWriter.close`](#JsonTreeWriterclose)
- **Extends/Implements**:
    - [`com.google.gson.stream.JsonWriter`](../../stream/JsonWriter.java.driver.md#JsonWriter)

**Methods**

---
#### JsonTreeWriter\.write<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.write}} -->
The `write` method in `JsonTreeWriter` throws an `AssertionError` when invoked.
- **Modifiers**: `public`
- **Inputs**:
    - `buffer`: A character array intended to be written.
    - `offset`: The starting position in the buffer from which to write.
    - `counter`: The number of characters to write from the buffer.
- **Control Flow**:
    - The method immediately throws an `AssertionError`, indicating that it is not intended to be used.
- **Output**:
    - The method does not return any value as it always throws an `AssertionError`.
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.flush<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.flush}} -->
The `flush` method in `JsonTreeWriter` throws an `AssertionError` when called.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is overridden from a superclass or interface.
    - When invoked, it immediately throws an `AssertionError`, indicating that the method should not be used.
- **Output**:
    - The method does not return any value as it always throws an `AssertionError`.
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.close<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.close}} -->
The `close` method in the `JsonTreeWriter` class throws an `AssertionError` when invoked.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is overridden from a superclass or interface.
    - When the method is called, it immediately throws an `AssertionError`.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.JsonTreeWriter<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.JsonTreeWriter}} -->
The `JsonTreeWriter` constructor initializes a new instance of the `JsonTreeWriter` class by calling the superclass constructor with an unwritable writer.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor calls the superclass `JsonWriter` constructor with a static `UNWRITABLE_WRITER` instance, which is a `Writer` that throws an `AssertionError` on any operation.
- **Output**:
    - A new instance of `JsonTreeWriter` is created.
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.get<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.get}} -->
The `get` method returns the top-level JSON element constructed by the `JsonTreeWriter` if the stack is empty, otherwise it throws an `IllegalStateException`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `stack` is not empty.
    - If the `stack` is not empty, throw an `IllegalStateException` with a message indicating that more than one JSON element was expected.
    - If the `stack` is empty, return the `product`, which is the top-level JSON element.
- **Output**:
    - The method returns a `JsonElement` which is the top-level JSON element constructed by the writer.
- **Functions called**:
    - [`com.google.gson.JsonObject.isEmpty`](../../JsonObject.java.driver.md#JsonObjectisEmpty)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.peek<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.peek}} -->
The `peek` method retrieves the last `JsonElement` from the `stack` list without removing it.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Access the `stack` list, which contains `JsonElement` objects.
    - Retrieve the element at the index `stack.size() - 1`, which is the last element in the list.
- **Output**:
    - The method returns the last `JsonElement` in the `stack` list.
- **Functions called**:
    - [`com.google.gson.JsonArray.get`](../../JsonArray.java.driver.md#JsonArrayget)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.put<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.put}} -->
The `put` method adds a `JsonElement` to the current JSON structure being built, either as a property of a `JsonObject` or as an element of a `JsonArray`, or sets it as the root element if the stack is empty.
- **Modifiers**: `private`
- **Inputs**:
    - `value`: A `JsonElement` to be added to the JSON structure.
- **Control Flow**:
    - Check if `pendingName` is not null, indicating that the current context is a `JsonObject` expecting a property value.
    - If `pendingName` is not null and the `value` is not `JsonNull` or `getSerializeNulls()` returns true, add the `value` to the `JsonObject` at the top of the stack with `pendingName` as the key, then set `pendingName` to null.
    - If `pendingName` is null and the stack is empty, set `product` to the `value`, making it the root element.
    - If `pendingName` is null and the stack is not empty, check the element at the top of the stack.
    - If the top element is a `JsonArray`, add the `value` to this array.
    - If the top element is not a `JsonArray`, throw an `IllegalStateException`.
- **Output**:
    - The method does not return a value; it modifies the JSON structure being built.
- **Functions called**:
    - [`com.google.gson.JsonElement.isJsonNull`](../../JsonElement.java.driver.md#JsonElementisJsonNull)
    - [`com.google.gson.stream.JsonWriter.getSerializeNulls`](../../stream/JsonWriter.java.driver.md#JsonWritergetSerializeNulls)
    - [`com.google.gson.internal.bind.JsonTreeWriter.peek`](#JsonTreeWriterpeek)
    - [`com.google.gson.JsonObject.add`](../../JsonObject.java.driver.md#JsonObjectadd)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.beginArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.beginArray}} -->
The `beginArray` method initializes a new JSON array, adds it to the current JSON structure, and returns the `JsonWriter` instance for chaining.
- **Modifiers**: `public`, `@CanIgnoreReturnValue`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - The [`put`](#JsonTreeWriterput) method is called with the new `JsonArray` to add it to the current JSON structure.
    - The new `JsonArray` is added to the `stack` to keep track of the current position in the JSON structure.
    - The method returns the current instance of `JsonWriter` to allow method chaining.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.endArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.endArray}} -->
The `endArray` method finalizes the current JSON array being constructed by removing it from the stack if it is valid.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Check if the stack is empty or if there is a pending name; if either is true, throw an IllegalStateException.
    - Retrieve the top element from the stack using the [`peek`](#JsonTreeWriterpeek) method.
    - Check if the retrieved element is an instance of `JsonArray`; if true, remove the last element from the stack and return the current `JsonWriter` instance.
    - If the retrieved element is not a `JsonArray`, throw an IllegalStateException.
- **Output**:
    - Returns the current instance of `JsonWriter` if the operation is successful, otherwise throws an exception.
- **Functions called**:
    - [`com.google.gson.JsonObject.isEmpty`](../../JsonObject.java.driver.md#JsonObjectisEmpty)
    - [`com.google.gson.internal.bind.JsonTreeWriter.peek`](#JsonTreeWriterpeek)
    - [`com.google.gson.JsonArray.remove`](../../JsonArray.java.driver.md#JsonArrayremove)
    - [`com.google.gson.JsonObject.size`](../../JsonObject.java.driver.md#JsonObjectsize)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.beginObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.beginObject}} -->
The `beginObject` method initializes a new JSON object, adds it to the current JSON structure, and returns the `JsonWriter` instance for chaining.
- **Modifiers**: `public`, `@CanIgnoreReturnValue`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonObject` instance is created.
    - The [`put`](#JsonTreeWriterput) method is called with the new `JsonObject` to add it to the current JSON structure.
    - The new `JsonObject` is added to the `stack` list to keep track of the current position in the JSON hierarchy.
    - The method returns the current instance of `JsonWriter` (`this`) to allow method chaining.
- **Output**:
    - The method returns the current instance of `JsonWriter` (`this`) to allow for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.endObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.endObject}} -->
The `endObject` method finalizes the current JSON object in the stack if it is valid and returns the `JsonWriter` instance.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Check if the stack is empty or if there is a pending name; if either is true, throw an `IllegalStateException`.
    - Retrieve the top element from the stack using the [`peek`](#JsonTreeWriterpeek) method.
    - Check if the retrieved element is an instance of `JsonObject`; if true, remove the top element from the stack and return the current `JsonWriter` instance.
    - If the retrieved element is not a `JsonObject`, throw an `IllegalStateException`.
- **Output**:
    - Returns the current `JsonWriter` instance if the operation is successful.
- **Functions called**:
    - [`com.google.gson.JsonObject.isEmpty`](../../JsonObject.java.driver.md#JsonObjectisEmpty)
    - [`com.google.gson.internal.bind.JsonTreeWriter.peek`](#JsonTreeWriterpeek)
    - [`com.google.gson.JsonArray.remove`](../../JsonArray.java.driver.md#JsonArrayremove)
    - [`com.google.gson.JsonObject.size`](../../JsonObject.java.driver.md#JsonObjectsize)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.name<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.name}} -->
The `name` method sets the name for the next JSON object value if the current context is a JSON object.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `name`: A `String` representing the name to be set for the next JSON object value.
- **Control Flow**:
    - Check if the `name` parameter is null and throw a `NullPointerException` if it is.
    - Check if the `stack` is empty or if `pendingName` is not null, and throw an `IllegalStateException` if either condition is true.
    - Retrieve the top element of the `stack` using the [`peek`](#JsonTreeWriterpeek) method.
    - Check if the top element is an instance of `JsonObject`.
    - If the top element is a `JsonObject`, set `pendingName` to the provided `name` and return `this`.
    - If the top element is not a `JsonObject`, throw an `IllegalStateException`.
- **Output**:
    - Returns the current instance of `JsonWriter` if the name is successfully set.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.peek`](#JsonTreeWriterpeek)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.value<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.value}} -->
The `value` method writes a string value to the JSON output, handling null values by writing a JSON null instead.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A string value to be written to the JSON output.
- **Control Flow**:
    - Check if the input `value` is null.
    - If `value` is null, call `nullValue()` to write a JSON null and return the current `JsonWriter` instance.
    - If `value` is not null, create a `JsonPrimitive` with the given `value`.
    - Call the [`put`](#JsonTreeWriterput) method to add the `JsonPrimitive` to the current JSON structure.
    - Return the current `JsonWriter` instance.
- **Output**:
    - Returns the current instance of `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.nullValue`](#JsonTreeWriternullValue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.value<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.value}} -->
The `value` method writes a boolean value as a JSON primitive to the current JSON structure and returns the `JsonWriter` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A boolean value to be written as a JSON primitive.
- **Control Flow**:
    - The method creates a new `JsonPrimitive` using the provided boolean value.
    - It calls the [`put`](#JsonTreeWriterput) method to add this `JsonPrimitive` to the current JSON structure.
    - The method returns the current instance of `JsonWriter`.
- **Output**:
    - The method returns the current instance of `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.value<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.value}} -->
The `value` method writes a Boolean value to the JSON output, handling null values by writing a JSON null.
- **Modifiers**: `public`, `@Override`
- **Inputs**:
    - `value`: A Boolean object that represents the value to be written to the JSON output.
- **Control Flow**:
    - Check if the input Boolean value is null.
    - If the value is null, call the `nullValue()` method to write a JSON null and return the current JsonWriter instance.
    - If the value is not null, create a new JsonPrimitive with the Boolean value and pass it to the [`put`](#JsonTreeWriterput) method to add it to the JSON structure.
    - Return the current instance of JsonWriter.
- **Output**:
    - Returns the current instance of JsonWriter, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.nullValue`](#JsonTreeWriternullValue)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.value<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.value}} -->
The `value` method writes a float value to the JSON output, ensuring it is not NaN or infinite unless in lenient mode.
- **Modifiers**: `public`, `@Override`
- **Inputs**:
    - `value`: A float value to be written to the JSON output.
- **Control Flow**:
    - Check if the writer is not in lenient mode and if the float value is NaN or infinite.
    - If the value is NaN or infinite and not in lenient mode, throw an IllegalArgumentException.
    - Create a new JsonPrimitive with the float value and pass it to the [`put`](#JsonTreeWriterput) method to add it to the JSON structure.
    - Return the current instance of JsonWriter.
- **Output**:
    - Returns the current instance of JsonWriter, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.isLenient`](../../stream/JsonWriter.java.driver.md#JsonWriterisLenient)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.value<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.value}} -->
The `value` method writes a double value to the JSON output, ensuring it is not NaN or infinite unless in lenient mode.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `value`: A double value to be written to the JSON output.
- **Control Flow**:
    - Check if the writer is not in lenient mode and if the value is NaN or infinite.
    - If the value is NaN or infinite and not in lenient mode, throw an IllegalArgumentException.
    - Create a new JsonPrimitive with the given double value and pass it to the [`put`](#JsonTreeWriterput) method.
    - Return the current instance of JsonWriter.
- **Output**:
    - Returns the current instance of JsonWriter after writing the double value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.isLenient`](../../stream/JsonWriter.java.driver.md#JsonWriterisLenient)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.value<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.value}} -->
The `value` method writes a long value as a JSON primitive to the current JSON structure and returns the `JsonWriter` instance.
- **Modifiers**: `public`, `@CanIgnoreReturnValue`, `@Override`
- **Inputs**:
    - `value`: A long value to be written as a JSON primitive.
- **Control Flow**:
    - The method creates a new `JsonPrimitive` using the provided long value.
    - It calls the [`put`](#JsonTreeWriterput) method to add this `JsonPrimitive` to the current JSON structure.
    - The method returns the current instance of `JsonWriter`.
- **Output**:
    - The method returns the current instance of `JsonWriter`, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.value<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.value}} -->
The `value` method writes a `Number` value to the JSON output, handling nulls and checking for NaN or infinite values when not in lenient mode.
- **Modifiers**: `public`, `@CanIgnoreReturnValue`, `@Override`
- **Inputs**:
    - `value`: A `Number` object to be written to the JSON output.
- **Control Flow**:
    - Check if the input `value` is null; if so, call `nullValue()` and return its result.
    - If the writer is not in lenient mode, convert the `Number` to a double and check if it is NaN or infinite; if so, throw an `IllegalArgumentException`.
    - Create a new `JsonPrimitive` with the `value` and pass it to the [`put`](#JsonTreeWriterput) method to add it to the JSON structure.
    - Return the current instance of `JsonWriter`.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.nullValue`](#JsonTreeWriternullValue)
    - [`com.google.gson.stream.JsonWriter.isLenient`](../../stream/JsonWriter.java.driver.md#JsonWriterisLenient)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.nullValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.nullValue}} -->
The `nullValue` method writes a JSON null value to the current JSON structure and returns the `JsonWriter` instance.
- **Modifiers**: `public`, `@CanIgnoreReturnValue`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Calls the [`put`](#JsonTreeWriterput) method with `JsonNull.INSTANCE` to add a JSON null value to the current JSON structure.
    - Returns the current instance of `JsonWriter` for method chaining.
- **Output**:
    - The method returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.jsonValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.jsonValue}} -->
The `jsonValue` method is intended to write a JSON value from a string but currently throws an `UnsupportedOperationException`.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A string representing the JSON value to be written.
- **Control Flow**:
    - The method immediately throws an `UnsupportedOperationException`, indicating that the operation is not supported.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.flush<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.flush}} -->
The `flush` method is an overridden method that does nothing in this implementation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is overridden from a superclass or interface.
    - The method is empty and does not perform any operations.
- **Output**:
    - The method does not return any value or perform any actions.
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)


---
#### JsonTreeWriter\.close<!-- {{#callable:com.google.gson.internal.bind.JsonTreeWriter.close}} -->
The `close` method finalizes the JSON writing process by ensuring the document is complete and marking the writer as closed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if the `stack` is not empty, indicating an incomplete document.
    - If the `stack` is not empty, throw an `IOException` with the message 'Incomplete document'.
    - If the `stack` is empty, add the `SENTINEL_CLOSED` marker to the `stack` to indicate the writer is closed.
- **Output**:
    - The method does not return any value but may throw an `IOException` if the document is incomplete.
- **See also**: [`com.google.gson.internal.bind.JsonTreeWriter`](#JsonTreeWriter)  (Base Class)



