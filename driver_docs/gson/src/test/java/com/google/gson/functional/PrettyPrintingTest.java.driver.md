# Purpose
The `PrettyPrintingTest` Java class is a suite of functional tests designed to verify the pretty-printing capabilities of the Gson library, a popular JSON serialization/deserialization library. This class is part of the `com.google.gson.functional` package and utilizes the JUnit testing framework to ensure that JSON output is formatted in a human-readable way when the `setPrettyPrinting` option is enabled in the `GsonBuilder`. The tests cover a variety of data structures, including lists, arrays, maps, and nested arrays, to ensure that the pretty-printing feature works consistently across different types of data.

The class is structured with a [`setUp`](#PrettyPrintingTestsetUp) method, which initializes a `Gson` instance configured for pretty printing, and several test methods that serialize different data structures into JSON strings. Each test method uses assertions to compare the generated JSON output against expected pretty-printed JSON strings. The tests include scenarios for lists of objects, arrays of primitives, arrays of objects, maps, and complex nested structures, ensuring comprehensive coverage of the pretty-printing functionality. Additionally, the class includes a test for an empty map field, addressing a specific bug (bug 153), to verify that the library handles empty collections correctly. Overall, this file serves as a robust validation tool for the pretty-printing feature of the Gson library.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.common.TestTypes.ArrayOfObjects`
- `com.google.gson.common.TestTypes.BagOfPrimitives`
- `com.google.gson.reflect.TypeToken`
- `java.lang.reflect.Type`
- `java.util.ArrayList`
- `java.util.Arrays`
- `java.util.LinkedHashMap`
- `java.util.List`
- `java.util.Map`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### PrettyPrintingTest<!-- {{#class:com.google.gson.functional.PrettyPrintingTest}} -->
- **Modifiers**: `public`
- **Description**: The `PrettyPrintingTest` class is a JUnit test class designed to verify the functionality of the pretty printing feature of the Gson library. It contains multiple test methods that serialize various data structures, such as lists, arrays, and maps, into JSON format using pretty printing, and then assert that the output matches the expected formatted JSON strings. The class ensures that the Gson library's pretty printing option correctly formats JSON output for different types of data structures.
- **Fields**:
    - `gson`: `Gson` An instance of Gson configured with pretty printing enabled.
- **Methods**:
    - [`com.google.gson.functional.PrettyPrintingTest.setUp`](#PrettyPrintingTestsetUp)
    - [`com.google.gson.functional.PrettyPrintingTest.testPrettyPrintList`](#PrettyPrintingTesttestPrettyPrintList)
    - [`com.google.gson.functional.PrettyPrintingTest.testPrettyPrintArrayOfObjects`](#PrettyPrintingTesttestPrettyPrintArrayOfObjects)
    - [`com.google.gson.functional.PrettyPrintingTest.testPrettyPrintArrayOfPrimitives`](#PrettyPrintingTesttestPrettyPrintArrayOfPrimitives)
    - [`com.google.gson.functional.PrettyPrintingTest.testPrettyPrintArrayOfPrimitiveArrays`](#PrettyPrintingTesttestPrettyPrintArrayOfPrimitiveArrays)
    - [`com.google.gson.functional.PrettyPrintingTest.testPrettyPrintListOfPrimitiveArrays`](#PrettyPrintingTesttestPrettyPrintListOfPrimitiveArrays)
    - [`com.google.gson.functional.PrettyPrintingTest.testMap`](#PrettyPrintingTesttestMap)
    - [`com.google.gson.functional.PrettyPrintingTest.testEmptyMapField`](#PrettyPrintingTesttestEmptyMapField)
    - [`com.google.gson.functional.PrettyPrintingTest.testMultipleArrays`](#PrettyPrintingTesttestMultipleArrays)

**Methods**

---
#### PrettyPrintingTest\.setUp<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.setUp}} -->
The setUp method initializes a Gson object with pretty printing enabled before each test is executed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with @Before, indicating it runs before each test method in the class.
    - A new Gson object is created using GsonBuilder with the setPrettyPrinting option enabled, and it is assigned to the gson field.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.GsonBuilder.setPrettyPrinting`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildersetPrettyPrinting)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testPrettyPrintList<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testPrettyPrintList}} -->
The `testPrettyPrintList` method tests the pretty-printing functionality of a list of `BagOfPrimitives` objects serialized to JSON using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate a `BagOfPrimitives` object `b`.
    - Create an empty `ArrayList` of `BagOfPrimitives` named `listOfB`.
    - Add the `BagOfPrimitives` object `b` to `listOfB` three times using a for loop.
    - Define the type of the source as a list of `BagOfPrimitives` using `TypeToken`.
    - Serialize `listOfB` to a JSON string using `gson.toJson` with the specified type.
    - Assert that the resulting JSON string matches the expected pretty-printed JSON format.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON output.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testPrettyPrintArrayOfObjects<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testPrettyPrintArrayOfObjects}} -->
The `testPrettyPrintArrayOfObjects` method tests the pretty-printing functionality of a JSON serialization of an `ArrayOfObjects` instance using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - An instance of `ArrayOfObjects` is created and assigned to the variable `target`.
    - The `gson.toJson(target)` method is called to serialize the `target` object into a JSON string with pretty-printing enabled, and the result is stored in the `json` variable.
    - The `assertThat(json).isEqualTo(...)` statement checks if the serialized JSON string matches the expected pretty-printed JSON format.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the JSON serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testPrettyPrintArrayOfPrimitives<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testPrettyPrintArrayOfPrimitives}} -->
The method `testPrettyPrintArrayOfPrimitives` tests the pretty-printing functionality of the Gson library for an array of primitive integers.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - An integer array `ints` is initialized with the values {1, 2, 3, 4, 5}.
    - The `gson.toJson` method is called to convert the integer array into a JSON string with pretty-printing enabled.
    - The resulting JSON string is compared to the expected pretty-printed JSON format using `assertThat` to ensure they are equal.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the pretty-printed JSON output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testPrettyPrintArrayOfPrimitiveArrays<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testPrettyPrintArrayOfPrimitiveArrays}} -->
The method `testPrettyPrintArrayOfPrimitiveArrays` tests the pretty printing of a two-dimensional array of integers using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a two-dimensional integer array `ints` with predefined values.
    - Convert the `ints` array to a JSON string using `gson.toJson(ints)`.
    - Assert that the resulting JSON string matches the expected pretty-printed format.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testPrettyPrintListOfPrimitiveArrays<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testPrettyPrintListOfPrimitiveArrays}} -->
The method `testPrettyPrintListOfPrimitiveArrays` tests the pretty-printing of a list of integer arrays into a JSON string using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A list of integer arrays is created using `Arrays.asList` with the arrays `{{1, 2}, {3, 4}, {5, 6}, {7, 8}, {9, 0}, {10}}`.
    - The list is converted to a JSON string using `gson.toJson(list)`.
    - An assertion is made using `assertThat(json).isEqualTo(...)` to verify that the JSON string matches the expected pretty-printed format.
- **Output**:
    - The method does not return any output; it performs an assertion to validate the JSON string format.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testMap<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testMap}} -->
The `testMap` method tests the JSON serialization of a `LinkedHashMap` using Gson with pretty printing enabled.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `LinkedHashMap` is instantiated and populated with two key-value pairs: "abc" mapped to 1 and "def" mapped to 5.
    - The `gson.toJson` method is called to serialize the map into a JSON string with pretty printing.
    - An assertion is made using `assertThat` to verify that the serialized JSON string matches the expected pretty-printed format.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the JSON output.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testEmptyMapField<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testEmptyMapField}} -->
The `testEmptyMapField` method tests the JSON serialization of an object with an empty map field using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Instantiate an object of `ClassWithMap`.
    - Assign an empty `LinkedHashMap` to the `map` field of the object.
    - Serialize the object to a JSON string using Gson.
    - Assert that the JSON string contains the expected representation of the object with an empty map and a default value of 2.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)


---
#### PrettyPrintingTest\.testMultipleArrays<!-- {{#callable:com.google.gson.functional.PrettyPrintingTest.testMultipleArrays}} -->
The `testMultipleArrays` method tests the JSON serialization of a three-dimensional integer array using Gson with pretty printing enabled.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A three-dimensional integer array `ints` is initialized with the value `{{{1}, {2}}}`.
    - The `gson.toJson(ints)` method is called to serialize the array into a JSON string with pretty printing.
    - The resulting JSON string is compared to the expected formatted JSON string using `assertThat(json).isEqualTo(...)`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the JSON output.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.PrettyPrintingTest`](#PrettyPrintingTest)  (Base Class)



---
### ClassWithMap<!-- {{#class:com.google.gson.functional.PrettyPrintingTest.ClassWithMap}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithMap` is a simple private static class that contains a map and an integer field, designed to demonstrate serialization and deserialization of objects with map fields using Gson.
- **Fields**:
    - `map`: `Map<String, Integer>` A map that associates String keys with Integer values.
    - `value`: `int` An integer field initialized to 2.


