# Purpose
The [`JsonTreeReader`](#JsonTreeReaderJsonTreeReader) class is a specialized implementation of the `JsonReader` that navigates through a `JsonElement` structure as if it were reading from a character stream. This class is part of the internal binding package of the Gson library, which is used for converting Java objects to JSON and vice versa. The primary function of [`JsonTreeReader`](#JsonTreeReaderJsonTreeReader) is to traverse a JSON tree structure, allowing for operations such as beginning and ending arrays and objects, reading JSON tokens, and retrieving values like strings, numbers, booleans, and nulls. It maintains a stack to keep track of the current position within the JSON structure, which is crucial for correctly navigating nested objects and arrays.

The class is designed to handle various JSON elements, including `JsonObject`, `JsonArray`, `JsonPrimitive`, and `JsonNull`, and provides methods to read and skip values, manage the stack, and track the path within the JSON structure. It uses a manual array for the stack to optimize performance and includes methods to handle JSON tokens, such as [`beginArray`](#JsonTreeReaderbeginArray), [`endArray`](#JsonTreeReaderendArray), [`beginObject`](#JsonTreeReaderbeginObject), [`endObject`](#JsonTreeReaderendObject), and [`hasNext`](#JsonTreeReaderhasNext). The class also provides utility methods like [`getPath`](#JsonTreeReadergetPath) and [`getPreviousPath`](#JsonTreeReadergetPreviousPath) to return the current and previous paths within the JSON structure, respectively. This implementation is crucial for applications that require efficient and precise navigation and manipulation of JSON data structures.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.JsonArray`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonNull`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.MalformedJsonException`
- `java.io.IOException`
- `java.io.Reader`
- `java.util.Arrays`
- `java.util.Iterator`
- `java.util.Map`


# Classes

---
### JsonTreeReader<!-- {{#class:com.google.gson.internal.bind.JsonTreeReader}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonTreeReader` class is a specialized implementation of `JsonReader` that traverses a `JsonElement` as if it were reading from a character stream, allowing for JSON parsing without the need for an actual I/O source. It maintains a stack to track the current position within the JSON structure, supporting operations such as beginning and ending arrays and objects, and retrieving values like strings, numbers, booleans, and nulls. The class also provides methods to skip values, promote names to values, and track the current path within the JSON structure.
- **Fields**:
    - `UNREADABLE_READER`: `Reader` A static final `Reader` instance that throws an `AssertionError` on any read or close operation.
    - `SENTINEL_CLOSED`: `Object` A static final `Object` used as a sentinel to indicate that the reader is closed.
    - `stack`: `Object[]` An array of `Object` used to maintain the current position within the JSON structure.
    - `stackSize`: `int` An integer representing the current size of the stack, indicating the depth of the JSON structure being traversed.
    - `pathNames`: `String[]` An array of `String` used to store the names of the current path within the JSON object structure.
    - `pathIndices`: `int[]` An array of `int` used to store the indices of the current path within the JSON array structure.
- **Methods**:
    - [`com.google.gson.internal.bind.JsonTreeReader.read`](#JsonTreeReaderread)
    - [`com.google.gson.internal.bind.JsonTreeReader.close`](#JsonTreeReaderclose)
    - [`com.google.gson.internal.bind.JsonTreeReader.JsonTreeReader`](#JsonTreeReaderJsonTreeReader)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.hasNext`](#JsonTreeReaderhasNext)
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](#JsonTreeReadernextString)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextBoolean`](#JsonTreeReadernextBoolean)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextNull`](#JsonTreeReadernextNull)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextDouble`](#JsonTreeReadernextDouble)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextLong`](#JsonTreeReadernextLong)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextJsonElement`](#JsonTreeReadernextJsonElement)
    - [`com.google.gson.internal.bind.JsonTreeReader.close`](#JsonTreeReaderclose)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.toString`](#JsonTreeReadertoString)
    - [`com.google.gson.internal.bind.JsonTreeReader.promoteNameToValue`](#JsonTreeReaderpromoteNameToValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.push`](#JsonTreeReaderpush)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.locationString`](#JsonTreeReaderlocationString)
- **Extends/Implements**:
    - [`com.google.gson.stream.JsonReader`](../../stream/JsonReader.java.driver.md#JsonReader)

**Methods**

---
#### JsonTreeReader\.read<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.read}} -->
The `read` method in the `JsonTreeReader` class is overridden to always throw an `AssertionError`.
- **Modifiers**: `public`, `int`
- **Inputs**:
    - `buffer`: A character array intended to store the read characters.
    - `offset`: The starting position in the buffer to begin storing the read characters.
    - `count`: The maximum number of characters to read.
- **Control Flow**:
    - The method is overridden from a superclass or interface.
    - Upon invocation, the method immediately throws an `AssertionError`, indicating that it is not intended to be used.
- **Output**:
    - The method does not return any value as it always throws an `AssertionError`.
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.close<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.close}} -->
The `close` method overrides the `close` method in the `Reader` class to throw an `AssertionError`, indicating that the method should not be called.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is overridden from the `Reader` class.
    - When called, it immediately throws an `AssertionError`.
- **Output**:
    - The method does not return any value as it throws an exception.
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.JsonTreeReader<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.JsonTreeReader}} -->
The `JsonTreeReader` constructor initializes a new instance of the `JsonTreeReader` class with a given `JsonElement` and pushes it onto the stack.
- **Modifiers**: `public`
- **Inputs**:
    - `element`: A `JsonElement` object that represents the JSON data to be read by the `JsonTreeReader`.
- **Control Flow**:
    - The constructor calls the superclass constructor `JsonReader` with a static `UNREADABLE_READER` to initialize the reader.
    - It then calls the [`push`](#JsonTreeReaderpush) method with the provided `JsonElement` to add it to the internal stack for processing.
- **Output**:
    - This constructor does not return a value as it is used to instantiate an object of the `JsonTreeReader` class.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.push`](#JsonTreeReaderpush)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.beginArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.beginArray}} -->
The `beginArray` method initializes the reading of a JSON array by setting up the necessary stack and path index.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method first calls [`expect`](#JsonTreeReaderexpect) with `JsonToken.BEGIN_ARRAY` to ensure the current token is the start of an array.
    - It retrieves the current top of the stack, which should be a `JsonArray`, using [`peekStack`](#JsonTreeReaderpeekStack).
    - The method then pushes an iterator of the `JsonArray` onto the stack to facilitate iteration over the array elements.
    - Finally, it sets the current path index for the array to 0, indicating the start of the array.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.push`](#JsonTreeReaderpush)
    - [`com.google.gson.JsonArray.iterator`](../../JsonArray.java.driver.md#JsonArrayiterator)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.endArray<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.endArray}} -->
The `endArray` method finalizes the reading of a JSON array by verifying the expected token, updating the stack, and adjusting the path index.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by calling `expect(JsonToken.END_ARRAY)` to ensure the current token is an end array token, throwing an exception if not.
    - It then calls `popStack()` twice to remove the empty iterator and the array from the stack.
    - If the stack size is greater than zero after popping, it increments the path index at the current stack level.
- **Output**:
    - The method does not return any value but modifies the internal state of the `JsonTreeReader` by updating the stack and path indices.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.beginObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.beginObject}} -->
The `beginObject` method prepares the `JsonTreeReader` to read a JSON object by expecting a `BEGIN_OBJECT` token and pushing an iterator of the object's entries onto the stack.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method first calls `expect(JsonToken.BEGIN_OBJECT)` to ensure that the next token is a `BEGIN_OBJECT` token, throwing an exception if it is not.
    - It retrieves the current object from the top of the stack using `peekStack()` and casts it to a `JsonObject`.
    - An iterator over the entry set of the `JsonObject` is created and pushed onto the stack using the [`push`](#JsonTreeReaderpush) method.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.push`](#JsonTreeReaderpush)
    - [`com.google.gson.JsonObject.entrySet`](../../JsonObject.java.driver.md#JsonObjectentrySet)
    - [`com.google.gson.JsonArray.iterator`](../../JsonArray.java.driver.md#JsonArrayiterator)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.endObject<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.endObject}} -->
The `endObject` method finalizes the reading of a JSON object by ensuring the expected token is present, cleaning up the stack, and updating path indices.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method first calls `expect(JsonToken.END_OBJECT)` to ensure the current token is an end object token.
    - It sets the last path name in `pathNames` to `null` to allow garbage collection.
    - The method calls `popStack()` twice to remove the empty iterator and the object from the stack.
    - If the `stackSize` is greater than 0, it increments the path index of the current stack level.
- **Output**:
    - The method does not return any value but modifies the internal state of the `JsonTreeReader` object.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.hasNext<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.hasNext}} -->
The `hasNext` method checks if there are more elements to read in the JSON structure by verifying the current token is not an end token.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Call the [`peek`](#JsonTreeReaderpeek) method to get the current `JsonToken`.
    - Check if the token is not `JsonToken.END_OBJECT`, `JsonToken.END_ARRAY`, or `JsonToken.END_DOCUMENT`.
    - Return `true` if the token is not one of the end tokens, otherwise return `false`.
- **Output**:
    - A boolean value indicating whether there are more elements to read in the JSON structure.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.peek<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.peek}} -->
The [`peek`](JsonTreeWriter.java.driver.md#JsonTreeWriterpeek) method returns the next `JsonToken` type from the JSON structure without advancing the reader.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Check if `stackSize` is 0; if true, return `JsonToken.END_DOCUMENT`.
    - Retrieve the top object from the stack using `peekStack()`.
    - If the object is an `Iterator`, determine if it is iterating over a `JsonObject` or `JsonArray`.
    - If the iterator has a next element, return `JsonToken.NAME` for `JsonObject` or push the next element and recursively call [`peek`](JsonTreeWriter.java.driver.md#JsonTreeWriterpeek) for `JsonArray`.
    - If the iterator has no next element, return `JsonToken.END_OBJECT` for `JsonObject` or `JsonToken.END_ARRAY` for `JsonArray`.
    - If the object is a `JsonObject`, return `JsonToken.BEGIN_OBJECT`.
    - If the object is a `JsonArray`, return `JsonToken.BEGIN_ARRAY`.
    - If the object is a `JsonPrimitive`, determine its type and return the corresponding `JsonToken` (`STRING`, `BOOLEAN`, or `NUMBER`).
    - If the object is a `JsonNull`, return `JsonToken.NULL`.
    - If the object is `SENTINEL_CLOSED`, throw an `IllegalStateException`.
    - If the object is of an unsupported type, throw a `MalformedJsonException`.
- **Output**:
    - The method returns a `JsonToken` representing the type of the next element in the JSON structure.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.push`](#JsonTreeReaderpush)
    - [`com.google.gson.internal.bind.JsonTreeWriter.peek`](JsonTreeWriter.java.driver.md#JsonTreeWriterpeek)
    - [`com.google.gson.JsonPrimitive.isString`](../../JsonPrimitive.java.driver.md#JsonPrimitiveisString)
    - [`com.google.gson.JsonPrimitive.isBoolean`](../../JsonPrimitive.java.driver.md#JsonPrimitiveisBoolean)
    - [`com.google.gson.JsonPrimitive.isNumber`](../../JsonPrimitive.java.driver.md#JsonPrimitiveisNumber)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.peekStack<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.peekStack}} -->
The `peekStack` method returns the top element of the stack without removing it.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Accesses the `stack` array using the index `stackSize - 1` to retrieve the top element.
- **Output**:
    - Returns the object at the top of the stack, which is the last element added to the stack.
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.popStack<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.popStack}} -->
The `popStack` method removes and returns the top element from the stack, while also nullifying the reference to it in the stack array.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Decrement the `stackSize` by one to point to the current top element of the stack.
    - Retrieve the element at the new top position of the stack and store it in the `result` variable.
    - Set the stack position at the new top to `null` to remove the reference to the popped element.
    - Return the `result` which is the element that was at the top of the stack.
- **Output**:
    - The method returns the object that was at the top of the stack before it was removed.
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.expect<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.expect}} -->
The `expect` method checks if the current JSON token matches the expected token and throws an exception if it does not.
- **Modifiers**: `private`
- **Inputs**:
    - `expected`: The `JsonToken` that is expected to be the current token.
- **Control Flow**:
    - Call the [`peek`](#JsonTreeReaderpeek) method to get the current JSON token.
    - Compare the current token with the `expected` token.
    - If the current token does not match the `expected` token, throw an `IllegalStateException` with a message indicating the mismatch and the current location in the JSON structure.
- **Output**:
    - The method does not return any value; it either completes successfully or throws an exception if the expectation is not met.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.locationString`](#JsonTreeReaderlocationString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextName<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextName}} -->
The `nextName` method retrieves the next JSON object's key name from the current position in the JSON structure, optionally skipping the name in the path tracking.
- **Modifiers**: `private`
- **Inputs**:
    - `skipName`: A boolean flag indicating whether to skip storing the name in the path tracking array.
- **Control Flow**:
    - The method first checks if the current token is a JSON object name using the [`expect`](#JsonTreeReaderexpect) method with `JsonToken.NAME`.
    - It retrieves the current iterator from the stack using [`peekStack`](#JsonTreeReaderpeekStack) and casts it to an `Iterator`.
    - The method then gets the next entry from the iterator, which is a `Map.Entry`, and extracts the key as a `String`.
    - If `skipName` is true, it stores "<skipped>" in the `pathNames` array at the current stack level; otherwise, it stores the actual key name.
    - The value associated with the key is pushed onto the stack using the [`push`](#JsonTreeReaderpush) method.
    - Finally, the method returns the key name as a `String`.
- **Output**:
    - The method returns the key name of the current JSON object entry as a `String`.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.push`](#JsonTreeReaderpush)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextName<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextName}} -->
The [`nextName`](#JsonTreeReadernextName) method retrieves the next JSON property name from the JSON structure being read.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls `nextName(false)` to retrieve the next property name without skipping it.
- **Output**:
    - Returns a `String` representing the next JSON property name.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](#JsonTreeReadernextName)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextString<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextString}} -->
The `nextString` method retrieves the next JSON string or number from the JSON stream, converting it to a string, and updates the path index.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Invoke the [`peek`](#JsonTreeReaderpeek) method to determine the type of the next JSON token.
    - Check if the token is not a `STRING` or `NUMBER`; if so, throw an `IllegalStateException`.
    - Pop the top element from the stack, which is expected to be a `JsonPrimitive`, and convert it to a string.
    - If the stack size is greater than zero, increment the last path index in `pathIndices`.
    - Return the resulting string.
- **Output**:
    - Returns the next JSON string or number as a string.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.locationString`](#JsonTreeReaderlocationString)
    - [`com.google.gson.JsonPrimitive.getAsString`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsString)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextBoolean<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextBoolean}} -->
The `nextBoolean` method reads the next JSON token as a boolean value from the JSON element stack.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method first calls `expect(JsonToken.BOOLEAN)` to ensure the next token is a boolean.
    - It then pops the top element from the stack using `popStack()` and casts it to `JsonPrimitive` to retrieve its boolean value using `getAsBoolean()`.
    - If the stack size is greater than zero, it increments the last index in the `pathIndices` array to reflect the traversal of the JSON structure.
    - Finally, it returns the boolean value obtained from the JSON primitive.
- **Output**:
    - The method returns a boolean value representing the next JSON token as a boolean.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.JsonPrimitive.getAsBoolean`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextNull<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextNull}} -->
The `nextNull` method processes the next JSON token, expecting it to be a null value, and updates the internal stack and path indices accordingly.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method first calls `expect(JsonToken.NULL)` to ensure the next token is a null value, throwing an exception if it is not.
    - It then calls `popStack()` to remove the current top element from the stack, which is expected to be a null value.
    - If the stack size is greater than zero after popping, it increments the last element of the `pathIndices` array to reflect the advancement in the JSON structure.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextDouble<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextDouble}} -->
The `nextDouble` method reads the next JSON token as a double value, ensuring it is a valid number or string and not NaN or infinite if lenient mode is off.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method starts by calling `peek()` to check the next JSON token.
    - If the token is neither a `NUMBER` nor a `STRING`, it throws an `IllegalStateException`.
    - It retrieves the double value from the current JSON element using `getAsDouble()`.
    - If the reader is not in lenient mode and the result is NaN or infinite, it throws a `MalformedJsonException`.
    - The method then calls `popStack()` to remove the current element from the stack.
    - If there are more elements in the stack, it increments the index of the current path.
    - Finally, it returns the double value.
- **Output**:
    - The method returns a `double` value representing the next JSON token interpreted as a number.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.locationString`](#JsonTreeReaderlocationString)
    - [`com.google.gson.JsonPrimitive.getAsDouble`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsDouble)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.stream.JsonReader.isLenient`](../../stream/JsonReader.java.driver.md#JsonReaderisLenient)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextLong<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextLong}} -->
The `nextLong` method retrieves the next JSON element as a long value, ensuring it is either a number or a string, and updates the reader's state accordingly.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Invoke the [`peek`](#JsonTreeReaderpeek) method to determine the type of the next JSON token.
    - Check if the token is neither a `JsonToken.NUMBER` nor a `JsonToken.STRING`; if so, throw an `IllegalStateException`.
    - Retrieve the long value from the current JSON element using [`getAsLong`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsLong) on the `JsonPrimitive` at the top of the stack.
    - Remove the current element from the stack using [`popStack`](#JsonTreeReaderpopStack).
    - If there are remaining elements in the stack, increment the index of the current path in `pathIndices`.
    - Return the retrieved long value.
- **Output**:
    - Returns the next JSON element as a long value.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.locationString`](#JsonTreeReaderlocationString)
    - [`com.google.gson.JsonPrimitive.getAsLong`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsLong)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextInt<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextInt}} -->
The `nextInt` method retrieves the next JSON element as an integer, ensuring it is either a number or a string.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Call the [`peek`](#JsonTreeReaderpeek) method to determine the type of the next JSON token.
    - Check if the token is not a `NUMBER` or `STRING`, and if so, throw an `IllegalStateException`.
    - Retrieve the integer value from the current JSON element on the stack using [`getAsInt`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt).
    - Remove the current element from the stack using [`popStack`](#JsonTreeReaderpopStack).
    - If there are more elements in the stack, increment the index of the current path.
    - Return the integer value retrieved.
- **Output**:
    - Returns the next JSON element as an integer.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.locationString`](#JsonTreeReaderlocationString)
    - [`com.google.gson.JsonPrimitive.getAsInt`](../../JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.nextJsonElement<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.nextJsonElement}} -->
The `nextJsonElement` method retrieves the next `JsonElement` from the JSON stack, ensuring it is not a terminal or invalid token, and then skips the value in the stack.
- **Inputs**: None
- **Control Flow**:
    - Call the `peek()` method to determine the next `JsonToken` in the stack.
    - Check if the `peeked` token is `JsonToken.NAME`, `JsonToken.END_ARRAY`, `JsonToken.END_OBJECT`, or `JsonToken.END_DOCUMENT`.
    - If the `peeked` token is one of the above, throw an `IllegalStateException` indicating an unexpected token.
    - Retrieve the current `JsonElement` from the stack using `peekStack()`.
    - Call `skipValue()` to skip the current value in the stack.
    - Return the retrieved `JsonElement`.
- **Output**:
    - The method returns a `JsonElement` that represents the next element in the JSON stack.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](#JsonTreeReaderskipValue)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.close<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.close}} -->
The `close` method sets the stack to a closed state and updates the stack size to indicate closure.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method sets the `stack` array to contain only the `SENTINEL_CLOSED` object, indicating that the reader is closed.
    - The `stackSize` is set to 1, reflecting the new size of the stack after closure.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.skipValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.skipValue}} -->
The `skipValue` method skips over the current JSON token in the input stream without processing it.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method begins by peeking at the current JSON token using the `peek()` method.
    - A switch statement is used to handle different types of JSON tokens.
    - If the token is `NAME`, the method calls `nextName(true)` to skip the name.
    - If the token is `END_ARRAY`, the method calls `endArray()` to handle the end of an array.
    - If the token is `END_OBJECT`, the method calls `endObject()` to handle the end of an object.
    - If the token is `END_DOCUMENT`, the method does nothing as it indicates the end of the document.
    - For all other tokens, the method calls `popStack()` to remove the current element from the stack and increments the path index if the stack size is greater than zero.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.peek`](#JsonTreeReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.popStack`](#JsonTreeReaderpopStack)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.toString<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.toString}} -->
The `toString` method returns a string representation of the class name followed by the current JSON path location.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls `getClass().getSimpleName()` to retrieve the simple name of the class.
    - It then calls `locationString()` to get the current path location in the JSON structure.
    - The method concatenates the class name and the location string and returns the result.
- **Output**:
    - A string that combines the class's simple name and the current JSON path location.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.locationString`](#JsonTreeReaderlocationString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.promoteNameToValue<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.promoteNameToValue}} -->
The `promoteNameToValue` method promotes a JSON object's name to a value by pushing the value and the name as a `JsonPrimitive` onto the stack.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by expecting the current JSON token to be a `JsonToken.NAME` using the [`expect`](#JsonTreeReaderexpect) method.
    - It retrieves the current iterator from the top of the stack using [`peekStack`](#JsonTreeReaderpeekStack) and casts it to an `Iterator`.
    - The method then retrieves the next entry from the iterator, which is expected to be a `Map.Entry`.
    - It pushes the value of the entry onto the stack using the [`push`](#JsonTreeReaderpush) method.
    - Finally, it pushes the key of the entry, converted to a `JsonPrimitive`, onto the stack.
- **Output**:
    - The method does not return any value but modifies the internal stack of the `JsonTreeReader` object.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.expect`](#JsonTreeReaderexpect)
    - [`com.google.gson.internal.bind.JsonTreeReader.peekStack`](#JsonTreeReaderpeekStack)
    - [`com.google.gson.internal.bind.JsonTreeReader.push`](#JsonTreeReaderpush)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.push<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.push}} -->
The `push` method adds a new object to the top of the stack, expanding the stack's capacity if necessary.
- **Modifiers**: `private`
- **Inputs**:
    - `newTop`: The object to be added to the top of the stack.
- **Control Flow**:
    - Check if the current stack size equals the stack's length, indicating that the stack is full.
    - If the stack is full, double the stack's length and create new arrays for `stack`, `pathIndices`, and `pathNames` with the new length, copying the existing elements into these new arrays.
    - Add the `newTop` object to the stack at the current `stackSize` index.
    - Increment the `stackSize` to reflect the addition of the new object.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.getPath<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.getPath}} -->
The `getPath` method constructs a string representation of the current path in a JSON structure, optionally using the previous path indices.
- **Modifiers**: `private`
- **Inputs**:
    - `usePreviousPath`: A boolean flag indicating whether to use the previous path indices when constructing the path.
- **Control Flow**:
    - Initialize a StringBuilder with the root path symbol '$'.
    - Iterate over the stack up to the current stack size.
    - For each element in the stack, check if it is an instance of JsonArray or JsonObject.
    - If the element is a JsonArray and the next element in the stack is an Iterator, calculate the path index, adjusting it if usePreviousPath is true and certain conditions are met, then append the index to the result.
    - If the element is a JsonObject and the next element in the stack is an Iterator, append a dot and the path name (if available) to the result.
    - Return the constructed path as a string.
- **Output**:
    - A string representing the path in the JSON structure, starting with '$' and including indices for arrays and names for objects.
- **Functions called**:
    - [`com.google.gson.JsonElement.toString`](../../JsonElement.java.driver.md#JsonElementtoString)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.getPath<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.getPath}} -->
The [`getPath`](#JsonTreeReadergetPath) method returns the current JSON path as a string, starting from the root element.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls another method `getPath(boolean usePreviousPath)` with the argument `false`.
- **Output**:
    - A `String` representing the current path in the JSON structure.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.getPreviousPath<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.getPreviousPath}} -->
The `getPreviousPath` method returns the JSON path of the last accessed element in the JSON structure, adjusted to point to the previous element if applicable.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`getPath`](#JsonTreeReadergetPath) method with the argument `true`, which indicates that the path should be adjusted to point to the previous element.
    - The [`getPath`](#JsonTreeReadergetPath) method constructs a string representing the path in the JSON structure, decrementing the path index if `usePreviousPath` is true and the current index is at the last or second-to-last position in the stack.
- **Output**:
    - A `String` representing the JSON path to the previous element.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)


---
#### JsonTreeReader\.locationString<!-- {{#callable:com.google.gson.internal.bind.JsonTreeReader.locationString}} -->
The `locationString` method returns a string indicating the current path in the JSON structure being read.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`getPath`](#JsonTreeReadergetPath) method to retrieve the current path in the JSON structure.
    - It concatenates the string ' at path ' with the result of [`getPath`](#JsonTreeReadergetPath).
- **Output**:
    - A string that represents the current path in the JSON structure, prefixed with ' at path '.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.internal.bind.JsonTreeReader`](#JsonTreeReader)  (Base Class)



