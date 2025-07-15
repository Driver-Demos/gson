# Purpose
The `JsonReaderPathTest` class is a comprehensive test suite designed to validate the functionality of the `JsonReader` class, specifically focusing on the path tracking capabilities of JSON parsing. This file is part of the Google Gson library, which is used for converting Java objects to JSON and vice versa. The test class uses JUnit's parameterized testing feature to run tests with different configurations of `JsonReader` instances, created by the `Factory` enum. The tests cover a wide range of scenarios, including reading JSON objects and arrays, handling nested structures, and skipping values, all while verifying the correctness of the path information provided by the `JsonReader`.

The primary technical components of this file include the use of JUnit for structuring the tests and assertions, and the `JsonReader` class for parsing JSON data. The tests ensure that the `JsonReader` correctly updates its internal path state as it navigates through JSON structures, which is crucial for applications that need to track their position within a JSON document. The file does not define public APIs or external interfaces but serves as an internal validation tool to ensure the robustness and accuracy of the JSON parsing logic within the Gson library.
# Imports and Dependencies

---
- `com.google.gson.stream`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assume.assumeTrue`
- `com.google.gson.JsonElement`
- `com.google.gson.Strictness`
- `com.google.gson.internal.Streams`
- `com.google.gson.internal.bind.JsonTreeReader`
- `java.io.IOException`
- `java.io.StringReader`
- `java.util.Arrays`
- `java.util.List`
- `org.junit.Test`
- `org.junit.runner.RunWith`
- `org.junit.runners.Parameterized`


# Classes

---
### JsonReaderPathTest<!-- {{#class:com.google.gson.stream.JsonReaderPathTest}} -->
- **Modifiers**: `public`
- **Description**: The `JsonReaderPathTest` class is a parameterized JUnit test class designed to test the path tracking functionality of a `JsonReader` implementation. It verifies that the `JsonReader` correctly maintains and updates the path as it navigates through JSON structures, including objects and arrays, and handles various scenarios such as skipping values and handling multiple top-level values. The class uses parameterized tests to run the same set of tests with different `JsonReader` factory implementations, ensuring that both string-based and object-based readers are tested.
- **Fields**:
    - `factory`: `Factory` A `Factory` instance used to create `JsonReader` objects for testing.
- **Methods**:
    - [`com.google.gson.stream.JsonReaderPathTest.parameters`](#JsonReaderPathTestparameters)
    - [`com.google.gson.stream.JsonReaderPathTest.path`](#JsonReaderPathTestpath)
    - [`com.google.gson.stream.JsonReaderPathTest.objectPath`](#JsonReaderPathTestobjectPath)
    - [`com.google.gson.stream.JsonReaderPathTest.arrayPath`](#JsonReaderPathTestarrayPath)
    - [`com.google.gson.stream.JsonReaderPathTest.multipleTopLevelValuesInOneDocument`](#JsonReaderPathTestmultipleTopLevelValuesInOneDocument)
    - [`com.google.gson.stream.JsonReaderPathTest.skipArrayElements`](#JsonReaderPathTestskipArrayElements)
    - [`com.google.gson.stream.JsonReaderPathTest.skipArrayEnd`](#JsonReaderPathTestskipArrayEnd)
    - [`com.google.gson.stream.JsonReaderPathTest.skipObjectNames`](#JsonReaderPathTestskipObjectNames)
    - [`com.google.gson.stream.JsonReaderPathTest.skipObjectValues`](#JsonReaderPathTestskipObjectValues)
    - [`com.google.gson.stream.JsonReaderPathTest.skipObjectEnd`](#JsonReaderPathTestskipObjectEnd)
    - [`com.google.gson.stream.JsonReaderPathTest.skipNestedStructures`](#JsonReaderPathTestskipNestedStructures)
    - [`com.google.gson.stream.JsonReaderPathTest.skipEndOfDocument`](#JsonReaderPathTestskipEndOfDocument)
    - [`com.google.gson.stream.JsonReaderPathTest.arrayOfObjects`](#JsonReaderPathTestarrayOfObjects)
    - [`com.google.gson.stream.JsonReaderPathTest.arrayOfArrays`](#JsonReaderPathTestarrayOfArrays)
    - [`com.google.gson.stream.JsonReaderPathTest.objectOfObjects`](#JsonReaderPathTestobjectOfObjects)

**Methods**

---
#### JsonReaderPathTest\.parameters<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.parameters}} -->
The `parameters` method provides a list of parameter sets for parameterized tests, each containing a different `Factory` instance.
- **Modifiers**: `public`, `static`
- **Inputs**: None
- **Control Flow**:
    - The method uses `Arrays.asList` to create a list of `Object[]` arrays.
    - Each `Object[]` array contains a single element, which is a `Factory` enum constant (`Factory.STRING_READER` or `Factory.OBJECT_READER`).
    - The method returns the list of these `Object[]` arrays.
- **Output**:
    - A `List<Object[]>` containing two arrays, each with a single `Factory` enum constant.
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.path<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.path}} -->
The `path` method tests the `JsonReader`'s ability to track and return the current and previous JSON path as it navigates through a JSON structure.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is created using a JSON string with nested objects and arrays.
    - The initial path and previous path are asserted to be `"$"`.
    - The reader begins reading an object, and the paths are updated and asserted accordingly.
    - The reader navigates through the JSON structure, reading names, integers, booleans, nulls, and strings, while asserting the current and previous paths at each step.
    - The reader enters and exits nested objects and arrays, with path assertions at each transition.
    - The method concludes by asserting that the paths return to the root `"$"` after reading the entire JSON structure.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the `JsonReader`'s path tracking.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.beginObject`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextBoolean`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextBoolean)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextNull`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextNull)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextString`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextString)
    - [`com.google.gson.stream.JsonReader.endObject`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendObject)
    - [`com.google.gson.stream.JsonReader.endArray`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendArray)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.objectPath<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.objectPath}} -->
The `objectPath` method tests the path tracking functionality of a `JsonReader` when reading a simple JSON object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonReader` instance using the factory with a JSON string containing an object with two key-value pairs: `{"a":1,"b":2}`.
    - Assert that the initial path and previous path are both `"$"`.
    - Peek at the next token and assert that the path and previous path remain `"$"`.
    - Begin reading the object and assert that the path and previous path update to `"$."`.
    - Peek at the next token and assert that the path and previous path remain `"$."`.
    - Read the next name (key) and assert that the path and previous path update to `"$.a"`.
    - Peek at the next token and assert that the path and previous path remain `"$.a"`.
    - Read the next integer value and assert that the path and previous path remain `"$.a"`.
    - Peek at the next token and assert that the path and previous path remain `"$.a"`.
    - Read the next name (key) and assert that the path and previous path update to `"$.b"`.
    - Peek at the next token and assert that the path and previous path remain `"$.b"`.
    - Read the next integer value and assert that the path and previous path remain `"$.b"`.
    - Peek at the next token and assert that the path and previous path remain `"$.b"`.
    - End reading the object and assert that the path and previous path revert to `"$"`.
    - Peek at the next token and assert that the path and previous path remain `"$"`.
    - Close the reader and assert that the path and previous path remain `"$"`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the path tracking of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.stream.JsonReader.nextName`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.stream.JsonReader.endObject`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderendObject)
    - [`com.google.gson.stream.JsonReader.close`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderclose)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.arrayPath<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.arrayPath}} -->
The `arrayPath` method tests the path tracking functionality of a `JsonReader` when reading a JSON array.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonReader` instance using the factory with the JSON string '[1,2]'.
    - Assert that the initial path and previous path are both '$'.
    - Peek at the first token and assert that the path and previous path remain '$'.
    - Begin reading the array and assert that the path updates to '$[0]'.
    - Peek at the next token and assert that the path and previous path are '$[0]'.
    - Read the first integer and assert that the path updates to '$[1]'.
    - Peek at the next token and assert that the path and previous path are '$[1]'.
    - Read the second integer and assert that the path updates to '$[2]'.
    - Peek at the next token and assert that the path and previous path are '$[2]'.
    - End reading the array and assert that the path and previous path return to '$'.
    - Peek at the next token and assert that the path and previous path remain '$'.
    - Close the reader and assert that the path and previous path remain '$'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the path tracking of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.stream.JsonReader.getPreviousPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPreviousPath)
    - [`com.google.gson.stream.JsonReader.getPath`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReadergetPath)
    - [`com.google.gson.stream.JsonReader.peek`](../../../../../../main/java/com/google/gson/stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.close`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderclose)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.multipleTopLevelValuesInOneDocument<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.multipleTopLevelValuesInOneDocument}} -->
The `multipleTopLevelValuesInOneDocument` method tests the ability of a `JsonReader` to handle multiple top-level JSON arrays in a single document in a lenient mode.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by assuming that the `factory` is of type `Factory.STRING_READER` to ensure the test is applicable.
    - A `JsonReader` is created using the factory with the input string `"[][]"`, which represents two top-level JSON arrays.
    - The `JsonReader` is set to lenient mode using `setStrictness(Strictness.LENIENT)` to allow multiple top-level values.
    - The method then begins reading the first array using `beginArray()` and ends it with `endArray()`.
    - Assertions are made to check that the `getPreviousPath()` and `getPath()` methods return `"$"`, indicating the reader is at the root level after reading the first array.
    - The method repeats the process for the second array, again using `beginArray()` and `endArray()`, followed by the same assertions to verify the path is still at the root level.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.stream.JsonWriter.setStrictness`](../../../../../../main/java/com/google/gson/stream/JsonWriter.java.driver.md#JsonWritersetStrictness)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.skipArrayElements<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.skipArrayElements}} -->
The `skipArrayElements` method tests the functionality of skipping elements in a JSON array using a `JsonReader`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonReader` instance using the `factory` to parse the JSON string '[1,2,3]'.
    - Begin reading the array using `reader.beginArray()`.
    - Skip the first element of the array using `reader.skipValue()`.
    - Skip the second element of the array using `reader.skipValue()`.
    - Assert that the `getPreviousPath()` method of the reader returns '$[1]', indicating the path of the last skipped element.
    - Assert that the `getPath()` method of the reader returns '$[2]', indicating the path of the next element to be read.
- **Output**:
    - The method does not return any value; it performs assertions to verify the path of the JSON reader after skipping elements.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.skipArrayEnd<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.skipArrayEnd}} -->
The `skipArrayEnd` method tests the behavior of a `JsonReader` when skipping the end of an array within a JSON structure.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonReader` instance using the `factory` to parse the JSON string `[[],1]`.
    - Begin reading the outer array using `reader.beginArray()`.
    - Begin reading the inner array using `reader.beginArray()`.
    - Assert that the `getPreviousPath()` and `getPath()` methods return `$[0][0]`, indicating the current position in the JSON structure.
    - Call `reader.skipValue()` to skip the end of the inner array.
    - Assert that `getPreviousPath()` returns `$[0]` and `getPath()` returns `$[1]`, indicating the reader has moved past the inner array to the next element in the outer array.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correct path tracking of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.skipObjectNames<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.skipObjectNames}} -->
The `skipObjectNames` method tests the behavior of a `JsonReader` when skipping over object names in a JSON structure.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is created using the `factory` with a JSON string containing an object with an empty array as its value.
    - The `JsonReader` begins reading the object using `beginObject()`.
    - The `skipValue()` method is called to skip the current value, which is the array associated with the object name.
    - Assertions are made to verify that the `getPreviousPath()` and `getPath()` methods return the expected path values, indicating that the object name was skipped.
    - The `JsonReader` then begins reading the array using `beginArray()`.
    - Further assertions are made to verify the path values after beginning the array.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonReader` when skipping object names.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.skipObjectValues<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.skipObjectValues}} -->
The `skipObjectValues` method tests the behavior of skipping values in a JSON object using a `JsonReader`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonReader` instance using the `factory` to parse the JSON string '{"a":1,"b":2}'.
    - Begin reading the JSON object using `reader.beginObject()`.
    - Assert that the initial path and previous path are both '$.'.
    - Read the next name in the JSON object and store it in `unused1`.
    - Skip the value associated with the first name using `reader.skipValue()`.
    - Assert that the previous path is now '$.a' and the current path is '$.a'.
    - Read the next name in the JSON object and store it in `unused2`.
    - Assert that the previous path is now '$.b' and the current path is '$.b'.
- **Output**:
    - The method does not return any value; it performs assertions to verify the path tracking of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.skipObjectEnd<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.skipObjectEnd}} -->
The `skipObjectEnd` method tests the behavior of the `JsonReader` when skipping the end of an object in a JSON structure.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is created using a JSON string with nested objects.
    - The reader begins reading the outer object and then the inner object.
    - The method asserts the path before and after skipping the end of the inner object using `skipValue()`.
    - Assertions are made to verify that the path updates correctly after skipping the end of the object.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correct path behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.skipNestedStructures<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.skipNestedStructures}} -->
The `skipNestedStructures` method tests the ability of a `JsonReader` to skip over nested JSON structures and correctly update its path tracking.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is created using the `factory` with the JSON string `[[1,2,3],4]`.
    - The `JsonReader` begins reading an array using `beginArray()`.
    - The `JsonReader` skips the first value, which is a nested array `[1,2,3]`, using `skipValue()`.
    - Assertions are made to verify that the `JsonReader`'s previous path is `$[0]` and the current path is `$[1]`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correct path tracking of the `JsonReader` after skipping a nested structure.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.skipEndOfDocument<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.skipEndOfDocument}} -->
The `skipEndOfDocument` method tests the behavior of the `JsonReader` when attempting to skip values at the end of a JSON document.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonReader` instance using the `factory` to parse an empty JSON array `[]`.
    - Begin reading the array with `reader.beginArray()` and then end it with `reader.endArray()`.
    - Assert that the `getPreviousPath()` and `getPath()` methods of `reader` both return `"$"`, indicating the root path.
    - Call `reader.skipValue()` twice, each time asserting that `getPreviousPath()` and `getPath()` still return `"$"`, confirming that skipping values at the end of the document does not change the path.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.arrayOfObjects<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.arrayOfObjects}} -->
The `arrayOfObjects` method tests the path tracking of a `JsonReader` when reading an array of empty JSON objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by creating a `JsonReader` instance using the `factory` to parse a JSON string representing an array of three empty objects: `[{}, {}, {}]`.
    - The `JsonReader` is instructed to begin reading the array, and assertions are made to verify that the path is correctly set to the first element `$[0]`.
    - For each object in the array, the method begins reading the object, checks the path, ends the object, and verifies that the path updates to the next object in the array.
    - This process is repeated for all three objects in the array, with assertions checking the path before and after each object is read.
    - Finally, the method ends the array and asserts that the path returns to the root `$`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correct path tracking of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.arrayOfArrays<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.arrayOfArrays}} -->
The `arrayOfArrays` method tests the path tracking of a `JsonReader` when reading a JSON array containing empty arrays.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method begins by creating a `JsonReader` instance using a factory method with the JSON string '[[],[],[]]'.
    - It calls `beginArray()` on the reader to start reading the outer array and asserts the initial path is '$[0]'.
    - For each empty array within the outer array, it calls `beginArray()`, asserts the path is '$[i][0]', and then calls `endArray()` to close the inner array, asserting the path updates to the next array index.
    - After processing all inner arrays, it calls `endArray()` to close the outer array and asserts the final path is '$'.
- **Output**:
    - The method does not return any value; it uses assertions to verify the path tracking of the `JsonReader`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginArray)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.endArray`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendArray)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)


---
#### JsonReaderPathTest\.objectOfObjects<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.objectOfObjects}} -->
The `objectOfObjects` method tests the path tracking functionality of a `JsonReader` when reading a JSON object containing nested objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonReader` is created using a JSON string with nested objects: `{"a":{"a1":1,"a2":2},"b":{"b1":1}}`.
    - The method begins reading the outermost JSON object using `reader.beginObject()`.
    - Assertions are made to verify the initial path and previous path are both `"$."`.
    - The first name in the JSON object is read using `reader.nextName()`, and assertions check the path updates to `"$.a"`.
    - The method begins reading the nested object under `"a"` using `reader.beginObject()`, and assertions verify the path updates to `"$.a."`.
    - The first name-value pair in the nested object is read, and assertions verify the path updates to `"$.a.a1"` after reading the name and value.
    - The second name-value pair in the nested object is read, and assertions verify the path updates to `"$.a.a2"` after reading the name and value.
    - The method ends reading the nested object under `"a"` using `reader.endObject()`, and assertions verify the path reverts to `"$.a"`.
    - The next name in the outer object is read using `reader.nextName()`, and assertions check the path updates to `"$.b"`.
    - The method begins reading the nested object under `"b"` using `reader.beginObject()`, and assertions verify the path updates to `"$.b."`.
    - The name-value pair in the nested object is read, and assertions verify the path updates to `"$.b.b1"` after reading the name and value.
    - The method ends reading the nested object under `"b"` using `reader.endObject()`, and assertions verify the path reverts to `"$.b"`.
    - The method ends reading the outermost JSON object using `reader.endObject()`, and assertions verify the path reverts to `"$"`.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the `JsonReader` path tracking.
- **Functions called**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPreviousPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPreviousPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.getPath`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadergetPath)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextInt`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReadernextInt)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](../../../../../../main/java/com/google/gson/internal/bind/JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest`](#JsonReaderPathTest)  (Base Class)



---
### Factory<!-- {{#class:com.google.gson.stream.JsonReaderPathTest.Factory}} -->
- **Modifiers**: `public`
- **Description**: The `Factory` enum provides two distinct strategies for creating `JsonReader` instances from a given JSON string. It defines two constants, `STRING_READER` and `OBJECT_READER`, each implementing the `create` method to return a `JsonReader`. The `STRING_READER` creates a `JsonReader` directly from a `StringReader`, while the `OBJECT_READER` first parses the JSON string into a `JsonElement` and then creates a `JsonTreeReader` from it. This design allows for flexibility in how JSON data is read and processed, depending on the specific needs of the application.
- **Methods**:
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)
    - [`com.google.gson.stream.JsonReaderPathTest.Factory.create`](#Factorycreate)

**Methods**

---
#### Factory\.create<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.Factory.create}} -->
The `create` method instantiates a `JsonReader` using a `StringReader` initialized with the provided JSON data string.
- **Modifiers**: `public`
- **Inputs**:
    - `data`: A `String` containing JSON data to be read by the `JsonReader`.
- **Control Flow**:
    - The method takes a `String` parameter named `data`.
    - It creates a new `StringReader` object using the `data` string.
    - It then creates a new `JsonReader` object using the `StringReader` instance.
    - Finally, it returns the newly created `JsonReader` object.
- **Output**:
    - Returns a `JsonReader` object initialized to read from the provided JSON data string.
- **See also**: [`com.google.gson.stream.JsonReaderPathTest.Factory`](#JsonReaderPathTest.Factory)  (Base Class)


---
#### Factory\.create<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.Factory.create}} -->
The `create` method in the `OBJECT_READER` enum parses a JSON string into a `JsonElement` and returns a `JsonTreeReader` initialized with that element.
- **Modifiers**: `public`
- **Inputs**:
    - `data`: A `String` containing JSON data to be parsed.
- **Control Flow**:
    - A new `JsonReader` is created using the provided JSON string wrapped in a `StringReader`.
    - The `Streams.parse` method is called with the `JsonReader` to parse the JSON string into a `JsonElement`.
    - A new `JsonTreeReader` is instantiated with the parsed `JsonElement` and returned.
- **Output**:
    - Returns a `JsonTreeReader` initialized with the parsed `JsonElement`.
- **Functions called**:
    - [`com.google.gson.internal.Streams.parse`](../../../../../../main/java/com/google/gson/internal/Streams.java.driver.md#Streamsparse)
- **See also**: [`com.google.gson.stream.JsonReaderPathTest.Factory`](#JsonReaderPathTest.Factory)  (Base Class)


---
#### Factory\.create<!-- {{#callable:com.google.gson.stream.JsonReaderPathTest.Factory.create}} -->
The `create` method is an abstract method in the `Factory` enum that takes a JSON string as input and returns a `JsonReader` object.
- **Modifiers**: `abstract`
- **Inputs**:
    - `data`: A `String` representing JSON data to be read by the `JsonReader`.
- **Control Flow**:
    - The method is abstract, meaning it must be implemented by each enum constant in the `Factory` enum.
    - The `STRING_READER` constant implements this method by creating a `JsonReader` using a `StringReader` initialized with the input data.
    - The `OBJECT_READER` constant implements this method by parsing the input data into a `JsonElement` using `Streams.parse` and then creating a `JsonTreeReader` with this element.
- **Output**:
    - The method returns a `JsonReader` object that can be used to read the JSON data provided as input.
- **See also**: [`com.google.gson.stream.JsonReaderPathTest.Factory`](#JsonReaderPathTest.Factory)  (Base Class)



