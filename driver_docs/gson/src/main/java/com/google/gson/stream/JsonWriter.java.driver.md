# Purpose
The provided Java source code defines a class named [`JsonWriter`](#JsonWriterJsonWriter) within the `com.google.gson.stream` package. This class is a core component of the Gson library, which is used for serializing Java objects into JSON and deserializing JSON into Java objects. The [`JsonWriter`](#JsonWriterJsonWriter) class specifically handles the task of writing JSON data to a stream, one token at a time, allowing for efficient and controlled JSON output generation. It supports writing JSON arrays and objects, and provides methods to write various data types such as strings, numbers, booleans, and null values. The class is designed to be used in a structured manner, where methods like `beginArray()`, `endArray()`, `beginObject()`, and `endObject()` are used to define the JSON structure.

The [`JsonWriter`](#JsonWriterJsonWriter) class offers several configuration options to customize the JSON output, such as setting the formatting style (compact or pretty), enabling HTML-safe output, and controlling the serialization of null values. It also supports different levels of strictness in JSON writing, allowing for lenient writing of non-standard JSON values like NaN and Infinity when configured. The class is not thread-safe and is intended for use in single-threaded contexts. It implements the `Closeable` and `Flushable` interfaces, ensuring that resources are properly managed and data is flushed to the underlying writer. The class is a fundamental part of the Gson library's functionality, providing a flexible and efficient way to generate JSON data from Java applications.
# Imports and Dependencies

---
- `com.google.gson.stream`
- `com.google.gson.stream.JsonScope.DANGLING_NAME`
- `com.google.gson.stream.JsonScope.EMPTY_ARRAY`
- `com.google.gson.stream.JsonScope.EMPTY_DOCUMENT`
- `com.google.gson.stream.JsonScope.EMPTY_OBJECT`
- `com.google.gson.stream.JsonScope.NONEMPTY_ARRAY`
- `com.google.gson.stream.JsonScope.NONEMPTY_DOCUMENT`
- `com.google.gson.stream.JsonScope.NONEMPTY_OBJECT`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.FormattingStyle`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.Strictness`
- `java.io.Closeable`
- `java.io.Flushable`
- `java.io.IOException`
- `java.io.Writer`
- `java.math.BigDecimal`
- `java.math.BigInteger`
- `java.util.Arrays`
- `java.util.Objects`
- `java.util.concurrent.atomic.AtomicInteger`
- `java.util.concurrent.atomic.AtomicLong`
- `java.util.regex.Pattern`


# Classes

---
### JsonWriter<!-- {{#class:com.google.gson.stream.JsonWriter}} -->
- **Modifiers**: `public`
- **Description**: The `JsonWriter` class is a utility for writing JSON-encoded data to a stream, adhering to the JSON format as specified in RFC 8259. It provides methods to write JSON objects and arrays, and supports configuration options such as formatting style, strictness, and HTML safety. The class ensures that JSON is written correctly by managing the state of the JSON structure using a stack, and it allows for customization of the output format, including indentation and handling of null values. It is designed to be used for writing a single JSON stream and is not thread-safe.
- **Fields**:
    - `VALID_JSON_NUMBER_PATTERN`: `Pattern` A pattern to validate JSON numbers according to RFC 8259.
    - `REPLACEMENT_CHARS`: `String[]` An array of strings used to escape characters in JSON strings.
    - `HTML_SAFE_REPLACEMENT_CHARS`: `String[]` An array of strings used to escape HTML characters in JSON strings for safe inclusion in HTML/XML.
    - `out`: `Writer` The Writer object where JSON output is written.
    - `stack`: `int[]` An array used to manage the state of the JSON structure being written.
    - `stackSize`: `int` The current size of the stack, indicating the depth of the JSON structure.
    - `formattingStyle`: `FormattingStyle` The formatting style used for the JSON output, affecting indentation and newline characters.
    - `formattedColon`: `String` A cached string representing the colon separator, formatted according to the current style.
    - `formattedComma`: `String` A cached string representing the comma separator, formatted according to the current style.
    - `usesEmptyNewlineAndIndent`: `boolean` A boolean indicating if the current formatting style uses empty newline and indent.
    - `strictness`: `Strictness` The strictness level of the writer, determining how strictly it adheres to JSON syntax rules.
    - `htmlSafe`: `boolean` A boolean indicating if the writer should escape HTML characters in the JSON output.
    - `deferredName`: `String` A string holding a property name that is deferred until its value is written.
    - `serializeNulls`: `boolean` A boolean indicating if null values should be serialized in the JSON output.
- **Methods**:
    - [`com.google.gson.stream.JsonWriter.JsonWriter`](#JsonWriterJsonWriter)
    - [`com.google.gson.stream.JsonWriter.setIndent`](#JsonWritersetIndent)
    - [`com.google.gson.stream.JsonWriter.setFormattingStyle`](#JsonWritersetFormattingStyle)
    - [`com.google.gson.stream.JsonWriter.getFormattingStyle`](#JsonWritergetFormattingStyle)
    - [`com.google.gson.stream.JsonWriter.setLenient`](#JsonWritersetLenient)
    - [`com.google.gson.stream.JsonWriter.isLenient`](#JsonWriterisLenient)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](#JsonWritersetStrictness)
    - [`com.google.gson.stream.JsonWriter.getStrictness`](#JsonWritergetStrictness)
    - [`com.google.gson.stream.JsonWriter.setHtmlSafe`](#JsonWritersetHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.isHtmlSafe`](#JsonWriterisHtmlSafe)
    - [`com.google.gson.stream.JsonWriter.setSerializeNulls`](#JsonWritersetSerializeNulls)
    - [`com.google.gson.stream.JsonWriter.getSerializeNulls`](#JsonWritergetSerializeNulls)
    - [`com.google.gson.stream.JsonWriter.beginArray`](#JsonWriterbeginArray)
    - [`com.google.gson.stream.JsonWriter.endArray`](#JsonWriterendArray)
    - [`com.google.gson.stream.JsonWriter.beginObject`](#JsonWriterbeginObject)
    - [`com.google.gson.stream.JsonWriter.endObject`](#JsonWriterendObject)
    - [`com.google.gson.stream.JsonWriter.openScope`](#JsonWriteropenScope)
    - [`com.google.gson.stream.JsonWriter.closeScope`](#JsonWritercloseScope)
    - [`com.google.gson.stream.JsonWriter.push`](#JsonWriterpush)
    - [`com.google.gson.stream.JsonWriter.peek`](#JsonWriterpeek)
    - [`com.google.gson.stream.JsonWriter.replaceTop`](#JsonWriterreplaceTop)
    - [`com.google.gson.stream.JsonWriter.name`](#JsonWritername)
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.value`](#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.value`](#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.value`](#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.value`](#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.value`](#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.value`](#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.value`](#JsonWritervalue)
    - [`com.google.gson.stream.JsonWriter.nullValue`](#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.jsonValue`](#JsonWriterjsonValue)
    - [`com.google.gson.stream.JsonWriter.flush`](#JsonWriterflush)
    - [`com.google.gson.stream.JsonWriter.close`](#JsonWriterclose)
    - [`com.google.gson.stream.JsonWriter.alwaysCreatesValidJsonNumber`](#JsonWriteralwaysCreatesValidJsonNumber)
    - [`com.google.gson.stream.JsonWriter.string`](#JsonWriterstring)
    - [`com.google.gson.stream.JsonWriter.newline`](#JsonWriternewline)
    - [`com.google.gson.stream.JsonWriter.beforeName`](#JsonWriterbeforeName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **Extends/Implements**:
    - `Closeable`
    - `Flushable`

**Methods**

---
#### JsonWriter\.JsonWriter<!-- {{#callable:com.google.gson.stream.JsonWriter.JsonWriter}} -->
The `JsonWriter` constructor initializes a new instance of the `JsonWriter` class with a specified `Writer` output and sets the default formatting style to `COMPACT`.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `Writer` object that serves as the destination for the JSON output; it must not be null.
- **Control Flow**:
    - The constructor takes a `Writer` object as an argument.
    - It checks if the `Writer` object is null using `Objects.requireNonNull`, throwing a `NullPointerException` if it is null.
    - It assigns the `Writer` object to the instance variable `out`.
    - It calls the [`setFormattingStyle`](#JsonWritersetFormattingStyle) method with `FormattingStyle.COMPACT` to set the default formatting style.
- **Output**:
    - The constructor does not return any value as it is used to initialize an instance of the `JsonWriter` class.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setFormattingStyle`](#JsonWritersetFormattingStyle)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.setIndent<!-- {{#callable:com.google.gson.stream.JsonWriter.setIndent}} -->
The `setIndent` method configures the JSON writer's formatting style based on whether the provided indent string is empty or not.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `indent`: A string containing only whitespace, used to set the indentation level for JSON formatting.
- **Control Flow**:
    - Check if the `indent` string is empty.
    - If `indent` is empty, set the formatting style to `FormattingStyle.COMPACT`.
    - If `indent` is not empty, set the formatting style to `FormattingStyle.PRETTY` with the specified indent.
- **Output**:
    - This method does not return a value; it modifies the internal state of the JSON writer's formatting style.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setFormattingStyle`](#JsonWritersetFormattingStyle)
    - [`com.google.gson.FormattingStyle.withIndent`](../FormattingStyle.java.driver.md#FormattingStylewithIndent)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.setFormattingStyle<!-- {{#callable:com.google.gson.stream.JsonWriter.setFormattingStyle}} -->
The `setFormattingStyle` method configures the JSON writer's formatting style, affecting how separators and newlines are handled in the output.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `formattingStyle`: An instance of `FormattingStyle` that specifies the desired formatting style for the JSON output.
- **Control Flow**:
    - The method starts by assigning the provided `formattingStyle` to the instance variable `this.formattingStyle` after ensuring it is not null using `Objects.requireNonNull`.
    - It initializes `this.formattedComma` to a comma (",").
    - It checks if the `formattingStyle` uses space after separators by calling `usesSpaceAfterSeparators()`.
    - If true, it sets `this.formattedColon` to ": ".
    - It further checks if the newline style is empty by calling `getNewline().isEmpty()`.
    - If the newline is empty, it updates `this.formattedComma` to ", ".
    - If `usesSpaceAfterSeparators()` is false, it sets `this.formattedColon` to ":".
    - Finally, it sets `this.usesEmptyNewlineAndIndent` to true if both the newline and indent styles are empty, determined by calling `getNewline().isEmpty()` and `getIndent().isEmpty()`.
- **Output**:
    - The method does not return any value; it modifies the instance variables related to formatting style.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.usesSpaceAfterSeparators`](../FormattingStyle.java.driver.md#FormattingStyleusesSpaceAfterSeparators)
    - [`com.google.gson.FormattingStyle.getNewline`](../FormattingStyle.java.driver.md#FormattingStylegetNewline)
    - [`com.google.gson.FormattingStyle.getIndent`](../FormattingStyle.java.driver.md#FormattingStylegetIndent)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.getFormattingStyle<!-- {{#callable:com.google.gson.stream.JsonWriter.getFormattingStyle}} -->
The `getFormattingStyle` method returns the current `FormattingStyle` used by the `JsonWriter`.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `formattingStyle` field of the `JsonWriter` class.
- **Output**:
    - The method returns an instance of `FormattingStyle`, which represents the current formatting style used by the `JsonWriter`.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.setLenient<!-- {{#callable:com.google.gson.stream.JsonWriter.setLenient}} -->
The `setLenient` method sets the strictness level of the `JsonWriter` to either `LENIENT` or `LEGACY_STRICT` based on the boolean input.
- **Modifiers**: `public`, `final`, `deprecated`
- **Inputs**:
    - `lenient`: A boolean value indicating whether the writer should be lenient (`true`) or not (`false`).
- **Control Flow**:
    - The method checks the value of the `lenient` parameter.
    - If `lenient` is `true`, it calls [`setStrictness`](#JsonWritersetStrictness) with `Strictness.LENIENT`.
    - If `lenient` is `false`, it calls [`setStrictness`](#JsonWritersetStrictness) with `Strictness.LEGACY_STRICT`.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.setStrictness`](#JsonWritersetStrictness)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.isLenient<!-- {{#callable:com.google.gson.stream.JsonWriter.isLenient}} -->
The `isLenient` method checks if the current `JsonWriter` instance is set to lenient mode by comparing its strictness to `Strictness.LENIENT`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method returns the result of the comparison between the `strictness` field and `Strictness.LENIENT`.
- **Output**:
    - A boolean value indicating whether the `JsonWriter` is in lenient mode.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.setStrictness<!-- {{#callable:com.google.gson.stream.JsonWriter.setStrictness}} -->
The `setStrictness` method sets the strictness level for the `JsonWriter` instance, ensuring the provided `Strictness` value is not null.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `strictness`: An instance of the `Strictness` enum that defines the strictness level for the `JsonWriter`.
- **Control Flow**:
    - The method takes a `Strictness` object as a parameter.
    - It uses `Objects.requireNonNull` to ensure that the `strictness` parameter is not null.
    - The `strictness` field of the `JsonWriter` instance is set to the provided `strictness` value.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.getStrictness<!-- {{#callable:com.google.gson.stream.JsonWriter.getStrictness}} -->
The `getStrictness` method returns the current strictness level of the `JsonWriter` instance.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns the value of the `strictness` field, which is of type `Strictness`.
- **Output**:
    - The method returns a `Strictness` object representing the current strictness level of the `JsonWriter`.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.setHtmlSafe<!-- {{#callable:com.google.gson.stream.JsonWriter.setHtmlSafe}} -->
The `setHtmlSafe` method configures the `JsonWriter` to emit JSON that is safe for inclusion in HTML and XML documents by escaping certain HTML characters.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `htmlSafe`: A boolean value indicating whether the JSON output should be HTML-safe, escaping characters like '<', '>', '&', '=', and '\''.
- **Control Flow**:
    - Assigns the input boolean value `htmlSafe` to the instance variable `this.htmlSafe`.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.isHtmlSafe<!-- {{#callable:com.google.gson.stream.JsonWriter.isHtmlSafe}} -->
The `isHtmlSafe` method checks if the JSON writer is configured to produce HTML-safe JSON output.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns the value of the `htmlSafe` boolean field.
- **Output**:
    - A boolean value indicating whether the JSON writer is set to produce HTML-safe output.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.setSerializeNulls<!-- {{#callable:com.google.gson.stream.JsonWriter.setSerializeNulls}} -->
The `setSerializeNulls` method sets whether null values should be serialized in JSON output.
- **Modifiers**: `public`, `final`
- **Inputs**:
    - `serializeNulls`: A boolean indicating whether null values should be serialized (true) or not (false).
- **Control Flow**:
    - Assigns the input boolean value to the instance variable `serializeNulls`.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.getSerializeNulls<!-- {{#callable:com.google.gson.stream.JsonWriter.getSerializeNulls}} -->
The `getSerializeNulls` method returns the current setting for whether null object members are serialized in JSON output.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns the value of the `serializeNulls` boolean field.
- **Output**:
    - A boolean value indicating if null object members are serialized.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.beginArray<!-- {{#callable:com.google.gson.stream.JsonWriter.beginArray}} -->
The `beginArray` method initiates the encoding of a new JSON array in the output stream.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Calls `writeDeferredName()` to handle any deferred property name that needs to be written before starting the array.
    - Invokes `openScope(EMPTY_ARRAY, '[')` to open a new array scope, writing the '[' character to the output stream and updating the internal stack to reflect the new array context.
- **Output**:
    - Returns the `JsonWriter` instance to allow for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.openScope`](#JsonWriteropenScope)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.endArray<!-- {{#callable:com.google.gson.stream.JsonWriter.endArray}} -->
The `endArray` method finalizes the encoding of the current JSON array by closing its scope and writing the closing bracket.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`closeScope`](#JsonWritercloseScope) with parameters `EMPTY_ARRAY`, `NONEMPTY_ARRAY`, and the closing bracket `']'`.
    - [`closeScope`](#JsonWritercloseScope) checks the current context to ensure it is either `NONEMPTY_ARRAY` or `EMPTY_ARRAY`.
    - If the context is valid, it decrements the stack size and writes the closing bracket to the output.
- **Output**:
    - The method returns the `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.closeScope`](#JsonWritercloseScope)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.beginObject<!-- {{#callable:com.google.gson.stream.JsonWriter.beginObject}} -->
The `beginObject` method starts encoding a new JSON object by writing any deferred name and opening a new scope with an opening curly brace.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method first calls `writeDeferredName()` to handle any deferred property name that needs to be written before starting the object.
    - It then calls `openScope(EMPTY_OBJECT, '{')` to open a new JSON object scope, which writes the opening curly brace '{' to the output and updates the internal state to reflect the new object scope.
- **Output**:
    - The method returns the `JsonWriter` instance itself, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.openScope`](#JsonWriteropenScope)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.endObject<!-- {{#callable:com.google.gson.stream.JsonWriter.endObject}} -->
The `endObject` method finalizes the encoding of a JSON object by closing its scope and writing the closing bracket '}' to the output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls [`closeScope`](#JsonWritercloseScope) with parameters `EMPTY_OBJECT`, `NONEMPTY_OBJECT`, and '}' to handle the closing of the current JSON object scope.
    - [`closeScope`](#JsonWritercloseScope) checks the current context to ensure it is either `NONEMPTY_OBJECT` or `EMPTY_OBJECT`, throwing an `IllegalStateException` if not.
    - If there is a deferred name, it throws an `IllegalStateException` for a dangling name.
    - The method decrements the stack size and writes a newline if the context was `NONEMPTY_OBJECT`.
    - Finally, it writes the closing bracket '}' to the output.
- **Output**:
    - The method returns the `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.closeScope`](#JsonWritercloseScope)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.openScope<!-- {{#callable:com.google.gson.stream.JsonWriter.openScope}} -->
The `openScope` method prepares the JSON writer to begin a new JSON array or object by writing the appropriate opening bracket and updating the internal state.
- **Modifiers**: `private`
- **Inputs**:
    - `empty`: An integer representing the state of the JSON scope, indicating whether it is an empty array or object.
    - `openBracket`: A character representing the opening bracket for the JSON scope, either '[' for arrays or '{' for objects.
- **Control Flow**:
    - Call the [`beforeValue`](#JsonWriterbeforeValue) method to handle any necessary formatting or state changes before writing a new value.
    - Push the `empty` state onto the internal stack to track the current scope.
    - Write the `openBracket` character to the output to signify the start of a new JSON array or object.
    - Return the current instance of `JsonWriter` for method chaining.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
    - [`com.google.gson.stream.JsonWriter.push`](#JsonWriterpush)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.closeScope<!-- {{#callable:com.google.gson.stream.JsonWriter.closeScope}} -->
The `closeScope` method closes the current JSON scope by writing the appropriate closing bracket and handling any necessary state transitions or errors.
- **Modifiers**: `private`
- **Inputs**:
    - `empty`: An integer representing the state of an empty scope (e.g., EMPTY_ARRAY or EMPTY_OBJECT).
    - `nonempty`: An integer representing the state of a non-empty scope (e.g., NONEMPTY_ARRAY or NONEMPTY_OBJECT).
    - `closeBracket`: A character representing the closing bracket to be written (e.g., ']' for arrays or '}' for objects).
- **Control Flow**:
    - Retrieve the current context from the stack using the [`peek`](#JsonWriterpeek) method.
    - Check if the current context is neither `nonempty` nor `empty`; if so, throw an `IllegalStateException` indicating a nesting problem.
    - Check if `deferredName` is not null; if so, throw an `IllegalStateException` indicating a dangling name.
    - Decrement the `stackSize` to remove the current scope from the stack.
    - If the current context is `nonempty`, call the [`newline`](#JsonWriternewline) method to handle formatting.
    - Write the `closeBracket` character to the output writer.
    - Return the current `JsonWriter` instance.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.peek`](#JsonWriterpeek)
    - [`com.google.gson.stream.JsonWriter.newline`](#JsonWriternewline)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.push<!-- {{#callable:com.google.gson.stream.JsonWriter.push}} -->
The `push` method adds a new integer value to the top of the stack, expanding the stack's capacity if necessary.
- **Modifiers**: `private`
- **Inputs**:
    - `newTop`: An integer value to be added to the top of the stack.
- **Control Flow**:
    - Check if the current stack size is equal to the length of the stack array, indicating that the stack is full.
    - If the stack is full, double the size of the stack array using `Arrays.copyOf` to accommodate more elements.
    - Add the `newTop` integer to the current top position of the stack and increment the `stackSize` to reflect the addition of the new element.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.peek<!-- {{#callable:com.google.gson.stream.JsonWriter.peek}} -->
The `peek` method returns the top value of the stack without removing it, throwing an exception if the stack is empty.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Check if `stackSize` is 0, indicating the stack is empty.
    - If the stack is empty, throw an `IllegalStateException` with the message 'JsonWriter is closed.'
    - Return the value at the top of the stack, which is `stack[stackSize - 1]`.
- **Output**:
    - The method returns an integer representing the top value of the stack.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.replaceTop<!-- {{#callable:com.google.gson.stream.JsonWriter.replaceTop}} -->
The `replaceTop` method updates the top element of the stack with a new value.
- **Modifiers**: `private`
- **Inputs**:
    - `topOfStack`: An integer value that will replace the current top element of the stack.
- **Control Flow**:
    - Access the stack array at the index `stackSize - 1`, which represents the top of the stack.
    - Assign the value of `topOfStack` to this position in the stack array.
- **Output**:
    - This method does not return any value.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.name<!-- {{#callable:com.google.gson.stream.JsonWriter.name}} -->
The `name` method sets the name of the next JSON property to be written, ensuring it is called within a valid object context.
- **Modifiers**: `public`
- **Inputs**:
    - `name`: A `String` representing the name of the forthcoming JSON property; it must not be null.
- **Control Flow**:
    - The method first checks if the provided `name` is null and throws a `NullPointerException` if it is.
    - It then checks if `deferredName` is already set, indicating a name has already been written without a corresponding value, and throws an `IllegalStateException` if so.
    - The method retrieves the current context from the stack using the `peek()` method.
    - It checks if the current context is not `EMPTY_OBJECT` or `NONEMPTY_OBJECT`, throwing an `IllegalStateException` if the context is invalid for writing a name.
    - If all checks pass, it assigns the provided `name` to `deferredName` for later use when writing the value.
- **Output**:
    - Returns the current `JsonWriter` instance to allow for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.peek`](#JsonWriterpeek)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.writeDeferredName<!-- {{#callable:com.google.gson.stream.JsonWriter.writeDeferredName}} -->
The `writeDeferredName` method writes a deferred JSON property name to the output if it exists, and then clears the deferred name.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Check if `deferredName` is not null.
    - If true, call `beforeName()` to handle any necessary formatting or state changes before writing a name.
    - Write the `deferredName` to the output using the [`string`](#JsonWriterstring) method.
    - Set `deferredName` to null to clear it.
- **Output**:
    - This method does not return any value.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.beforeName`](#JsonWriterbeforeName)
    - [`com.google.gson.stream.JsonWriter.string`](#JsonWriterstring)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.value<!-- {{#callable:com.google.gson.stream.JsonWriter.value}} -->
The `value` method writes a string value to the JSON output, handling null values by writing a null literal instead.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: The literal string value to be encoded, or null to encode a null literal.
- **Control Flow**:
    - Check if the input `value` is null; if so, call `nullValue()` and return its result.
    - If the input `value` is not null, call `writeDeferredName()` to handle any deferred property names.
    - Call `beforeValue()` to manage any necessary separators or whitespace before writing the value.
    - Call `string(value)` to write the string value to the JSON output.
    - Return `this` to allow method chaining.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
    - [`com.google.gson.stream.JsonWriter.string`](#JsonWriterstring)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.value<!-- {{#callable:com.google.gson.stream.JsonWriter.value}} -->
The `value` method writes a boolean value to the JSON output stream, converting it to a string representation of "true" or "false".
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A boolean value to be written to the JSON output stream.
- **Control Flow**:
    - Call `writeDeferredName()` to handle any deferred property names that need to be written before the value.
    - Call `beforeValue()` to manage any necessary separators or whitespace before writing the value.
    - Write the boolean value to the output stream as a string, either "true" or "false" based on the input.
    - Return the current instance of `JsonWriter` for method chaining.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.value<!-- {{#callable:com.google.gson.stream.JsonWriter.value}} -->
The `value` method writes a Boolean value to the JSON output stream, handling null values by delegating to the [`nullValue`](#JsonWriternullValue) method.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A Boolean object that represents the value to be written to the JSON output stream.
- **Control Flow**:
    - Check if the input Boolean value is null; if so, call and return the result of the [`nullValue`](#JsonWriternullValue) method.
    - If the value is not null, call [`writeDeferredName`](#JsonWriterwriteDeferredName) to handle any deferred JSON property names.
    - Call [`beforeValue`](#JsonWriterbeforeValue) to manage JSON syntax and state before writing the value.
    - Write the Boolean value as a string ('true' or 'false') to the output stream.
    - Return the current instance of `JsonWriter` for method chaining.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.value<!-- {{#callable:com.google.gson.stream.JsonWriter.value}} -->
The `value` method writes a float value to the JSON output, ensuring it is finite unless the writer is in lenient mode.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A float value to be written to the JSON output.
- **Control Flow**:
    - Call `writeDeferredName()` to handle any deferred JSON property names.
    - Check if the writer's strictness is not `LENIENT` and if the float value is NaN or infinite; if so, throw an `IllegalArgumentException`.
    - Call `beforeValue()` to handle any necessary formatting or state changes before writing the value.
    - Append the string representation of the float value to the output writer.
    - Return the current `JsonWriter` instance for method chaining.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.value<!-- {{#callable:com.google.gson.stream.JsonWriter.value}} -->
The `value` method writes a double value to the JSON output, ensuring it is finite unless in lenient mode, and returns the `JsonWriter` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A double value to be written to the JSON output.
- **Control Flow**:
    - Call `writeDeferredName()` to handle any deferred property name.
    - Check if the `strictness` is not `LENIENT` and if the `value` is NaN or infinite; if so, throw an `IllegalArgumentException`.
    - Call `beforeValue()` to handle any necessary formatting or state changes before writing the value.
    - Append the string representation of the `value` to the output writer.
    - Return the current `JsonWriter` instance.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.value<!-- {{#callable:com.google.gson.stream.JsonWriter.value}} -->
The `value` method writes a long value to the JSON output stream and returns the current `JsonWriter` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A long integer value to be written to the JSON output stream.
- **Control Flow**:
    - Call `writeDeferredName()` to handle any deferred property name that needs to be written before the value.
    - Call `beforeValue()` to manage any necessary separators or whitespace before writing the value.
    - Convert the long `value` to a string and write it to the output stream using `out.write(Long.toString(value))`.
    - Return the current instance of `JsonWriter` to allow method chaining.
- **Output**:
    - The method returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.value<!-- {{#callable:com.google.gson.stream.JsonWriter.value}} -->
The `value` method writes a numeric value to the JSON output, ensuring it is valid according to the current strictness settings.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A `Number` object representing the numeric value to be written to the JSON output.
- **Control Flow**:
    - If the input `value` is `null`, the method calls `nullValue()` and returns its result.
    - The method calls `writeDeferredName()` to handle any deferred JSON property names.
    - The numeric value is converted to a string using `toString()`.
    - The method checks if the numeric value's class always creates valid JSON numbers using `alwaysCreatesValidJsonNumber()`.
    - If the class does not always create valid JSON numbers, the method validates the string representation against specific conditions (e.g., not being '-Infinity', 'Infinity', or 'NaN') and the `VALID_JSON_NUMBER_PATTERN`.
    - If the value is invalid and the strictness is not `LENIENT`, an `IllegalArgumentException` is thrown.
    - The method calls `beforeValue()` to handle any necessary formatting before writing the value.
    - The numeric string is appended to the output writer.
    - The method returns `this` to allow method chaining.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.alwaysCreatesValidJsonNumber`](#JsonWriteralwaysCreatesValidJsonNumber)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.nullValue<!-- {{#callable:com.google.gson.stream.JsonWriter.nullValue}} -->
The `nullValue` method writes a JSON null value to the output stream, handling deferred names and serialization settings.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Check if `deferredName` is not null.
    - If `deferredName` is not null and `serializeNulls` is true, call `writeDeferredName()` to write the deferred name.
    - If `deferredName` is not null and `serializeNulls` is false, set `deferredName` to null and return the current `JsonWriter` instance, skipping the name and value.
    - Call `beforeValue()` to handle any necessary formatting or state changes before writing a value.
    - Write the string "null" to the output stream.
    - Return the current `JsonWriter` instance.
- **Output**:
    - Returns the current instance of `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.jsonValue<!-- {{#callable:com.google.gson.stream.JsonWriter.jsonValue}} -->
The `jsonValue` method writes a raw JSON value to the output stream without quoting or escaping it, and returns the current `JsonWriter` instance.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: A `String` representing the raw JSON value to be written, or `null` to encode a null literal.
- **Control Flow**:
    - Check if the input `value` is `null`; if so, call `nullValue()` and return its result.
    - Call `writeDeferredName()` to handle any deferred property name that needs to be written before the value.
    - Call `beforeValue()` to insert any necessary separators and whitespace before writing the value.
    - Append the `value` directly to the output stream `out`.
    - Return the current instance of `JsonWriter`.
- **Output**:
    - Returns the current `JsonWriter` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.writeDeferredName`](#JsonWriterwriteDeferredName)
    - [`com.google.gson.stream.JsonWriter.beforeValue`](#JsonWriterbeforeValue)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.flush<!-- {{#callable:com.google.gson.stream.JsonWriter.flush}} -->
The `flush` method ensures that all buffered data is written to the underlying `Writer` and flushes it, throwing an exception if the `JsonWriter` is closed.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - Check if `stackSize` is 0, indicating the `JsonWriter` is closed, and throw an `IllegalStateException` if true.
    - Call the `flush` method on the `out` object to flush the underlying `Writer`.
- **Output**:
    - The method does not return any value but may throw an `IOException` if an I/O error occurs.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.close<!-- {{#callable:com.google.gson.stream.JsonWriter.close}} -->
The [`close`](JsonReader.java.driver.md#JsonReaderclose) method closes the underlying writer and ensures the JSON document is complete, throwing an `IOException` if it is not.
- **Modifiers**: `public`, `override`
- **Inputs**: None
- **Control Flow**:
    - The method first calls `out.close()` to close the underlying writer.
    - It then checks the `stackSize` to determine if the JSON document is complete.
    - If `stackSize` is greater than 1, or if it is 1 and the top of the stack is not `NONEMPTY_DOCUMENT`, it throws an `IOException` indicating an incomplete document.
    - Finally, it sets `stackSize` to 0, effectively resetting the stack.
- **Output**:
    - The method does not return a value but may throw an `IOException` if the JSON document is incomplete.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.close`](JsonReader.java.driver.md#JsonReaderclose)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.alwaysCreatesValidJsonNumber<!-- {{#callable:com.google.gson.stream.JsonWriter.alwaysCreatesValidJsonNumber}} -->
The method `alwaysCreatesValidJsonNumber` checks if a given class type of `Number` always produces a valid JSON number.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `c`: A `Class` object representing a subclass of `Number` to be checked.
- **Control Flow**:
    - The method checks if the class `c` is one of the following: `Integer`, `Long`, `Byte`, `Short`, `BigDecimal`, `BigInteger`, `AtomicInteger`, or `AtomicLong`.
    - If `c` matches any of these classes, the method returns `true`.
    - If `c` does not match any of these classes, the method returns `false`.
- **Output**:
    - A boolean value indicating whether the class type always produces a valid JSON number.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.string<!-- {{#callable:com.google.gson.stream.JsonWriter.string}} -->
The `string` method writes a JSON-encoded string to the output, escaping necessary characters based on the HTML safety setting.
- **Modifiers**: `private`
- **Inputs**:
    - `value`: The string value to be JSON-encoded and written to the output.
- **Control Flow**:
    - Determine the appropriate replacement character array based on the `htmlSafe` flag.
    - Write an opening double quote to the output.
    - Iterate over each character in the input string `value`.
    - For each character, determine if it needs to be replaced based on its ASCII value or if it is a special Unicode character (`\u2028` or `\u2029`).
    - If a replacement is needed, write the substring from the last non-replaced character to the current character, followed by the replacement string.
    - Update the `last` index to the position after the current character if a replacement was made.
    - After the loop, write any remaining substring from the last non-replaced character to the end of the string.
    - Write a closing double quote to the output.
- **Output**:
    - The method writes the JSON-encoded string to the `out` writer, escaping necessary characters.
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.newline<!-- {{#callable:com.google.gson.stream.JsonWriter.newline}} -->
The `newline` method writes a newline character and appropriate indentation to the output stream unless the formatting style uses empty newline and indent.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Check if `usesEmptyNewlineAndIndent` is true; if so, return immediately without writing anything.
    - Write the newline character to the output stream using `formattingStyle.getNewline()`.
    - Iterate from 1 to `stackSize - 1`, writing the indent string from `formattingStyle.getIndent()` to the output stream for each iteration.
- **Output**:
    - The method does not return any value, but it writes to the `out` stream.
- **Functions called**:
    - [`com.google.gson.FormattingStyle.getNewline`](../FormattingStyle.java.driver.md#FormattingStylegetNewline)
    - [`com.google.gson.FormattingStyle.getIndent`](../FormattingStyle.java.driver.md#FormattingStylegetIndent)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.beforeName<!-- {{#callable:com.google.gson.stream.JsonWriter.beforeName}} -->
The `beforeName` method prepares the JSON writer to write a property name by handling necessary formatting and state transitions.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the current context from the stack using the [`peek`](#JsonWriterpeek) method.
    - Check if the context is `NONEMPTY_OBJECT`; if true, write a formatted comma to the output writer.
    - If the context is not `EMPTY_OBJECT`, throw an `IllegalStateException` indicating a nesting problem.
    - Call the [`newline`](#JsonWriternewline) method to handle any necessary line breaks and indentation.
    - Replace the top of the stack with `DANGLING_NAME` to indicate that a name is expected next.
- **Output**:
    - The method does not return any value but modifies the state of the JSON writer and writes to the output stream.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.peek`](#JsonWriterpeek)
    - [`com.google.gson.stream.JsonWriter.newline`](#JsonWriternewline)
    - [`com.google.gson.stream.JsonWriter.replaceTop`](#JsonWriterreplaceTop)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)


---
#### JsonWriter\.beforeValue<!-- {{#callable:com.google.gson.stream.JsonWriter.beforeValue}} -->
The `beforeValue` method manages the state transitions and formatting required before writing a JSON value to the output stream.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method begins by checking the current state using the `peek()` method to determine the top of the stack.
    - If the state is `NONEMPTY_DOCUMENT` and strictness is not `LENIENT`, it throws an `IllegalStateException` to ensure only one top-level value is allowed in strict mode.
    - If the state is `EMPTY_DOCUMENT`, it transitions the state to `NONEMPTY_DOCUMENT`.
    - If the state is `EMPTY_ARRAY`, it transitions the state to `NONEMPTY_ARRAY` and writes a newline to the output.
    - If the state is `NONEMPTY_ARRAY`, it appends a formatted comma to the output and writes a newline.
    - If the state is `DANGLING_NAME`, it appends a formatted colon to the output and transitions the state to `NONEMPTY_OBJECT`.
    - If none of the above states match, it throws an `IllegalStateException` indicating a nesting problem.
- **Output**:
    - The method does not return a value but modifies the internal state and writes to the output stream as necessary.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.peek`](#JsonWriterpeek)
    - [`com.google.gson.stream.JsonWriter.replaceTop`](#JsonWriterreplaceTop)
    - [`com.google.gson.stream.JsonWriter.newline`](#JsonWriternewline)
- **See also**: [`com.google.gson.stream.JsonWriter`](#JsonWriter)  (Base Class)



