# Purpose
The `JsonArrayTest` class is a comprehensive suite of unit tests designed to validate the functionality of the `JsonArray` class within the Google Gson library. This test class focuses on ensuring the correct behavior of JSON array operations, such as equality checks, element addition and removal, deep copying, and type-specific operations. The tests cover a wide range of scenarios, including handling of empty and non-empty arrays, manipulation of primitive and complex data types, and the correct handling of null values. The class uses various assertions to verify that the `JsonArray` behaves as expected under different conditions, ensuring robustness and reliability in JSON array handling.

The test methods within `JsonArrayTest` utilize the JUnit framework for structuring and executing tests, and they employ additional utilities from the Google Truth library for expressive assertions. Key technical components include tests for equality and hash code consistency, exception handling for invalid operations, and validation of the `JsonArray`'s string representation. The class does not define public APIs or external interfaces; instead, it serves as an internal validation tool to ensure that the `JsonArray` class adheres to its expected contract and handles various edge cases effectively. This test suite is crucial for maintaining the integrity of the JSON array functionality within the Gson library, providing confidence in its use for JSON data manipulation.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.common.testing.EqualsTester`
- `com.google.gson.common.MoreAsserts`
- `java.math.BigInteger`
- `org.junit.Test`


# Classes

---
### JsonArrayTest<!-- {{#class:com.google.gson.JsonArrayTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `JsonArrayTest` class is a comprehensive test suite for the `JsonArray` class, part of the Google Gson library, which is used for handling JSON arrays. It includes a variety of test cases to ensure the correct functionality of `JsonArray` methods, such as adding, removing, and setting elements, as well as testing equality, deep copying, and handling of different data types including primitives and null values. The tests also cover edge cases and exceptions to verify the robustness of the `JsonArray` implementation.
- **Methods**:
    - [`com.google.gson.JsonArrayTest.testEqualsOnEmptyArray`](#JsonArrayTesttestEqualsOnEmptyArray)
    - [`com.google.gson.JsonArrayTest.testEqualsNonEmptyArray`](#JsonArrayTesttestEqualsNonEmptyArray)
    - [`com.google.gson.JsonArrayTest.testRemove`](#JsonArrayTesttestRemove)
    - [`com.google.gson.JsonArrayTest.testSet`](#JsonArrayTesttestSet)
    - [`com.google.gson.JsonArrayTest.testDeepCopy`](#JsonArrayTesttestDeepCopy)
    - [`com.google.gson.JsonArrayTest.testIsEmpty`](#JsonArrayTesttestIsEmpty)
    - [`com.google.gson.JsonArrayTest.testFailedGetArrayValues`](#JsonArrayTesttestFailedGetArrayValues)
    - [`com.google.gson.JsonArrayTest.testGetAs_WrongArraySize`](#JsonArrayTesttestGetAs_WrongArraySize)
    - [`com.google.gson.JsonArrayTest.testStringPrimitiveAddition`](#JsonArrayTesttestStringPrimitiveAddition)
    - [`com.google.gson.JsonArrayTest.testIntegerPrimitiveAddition`](#JsonArrayTesttestIntegerPrimitiveAddition)
    - [`com.google.gson.JsonArrayTest.testDoublePrimitiveAddition`](#JsonArrayTesttestDoublePrimitiveAddition)
    - [`com.google.gson.JsonArrayTest.testBooleanPrimitiveAddition`](#JsonArrayTesttestBooleanPrimitiveAddition)
    - [`com.google.gson.JsonArrayTest.testCharPrimitiveAddition`](#JsonArrayTesttestCharPrimitiveAddition)
    - [`com.google.gson.JsonArrayTest.testMixedPrimitiveAddition`](#JsonArrayTesttestMixedPrimitiveAddition)
    - [`com.google.gson.JsonArrayTest.testNullPrimitiveAddition`](#JsonArrayTesttestNullPrimitiveAddition)
    - [`com.google.gson.JsonArrayTest.testNullJsonElementAddition`](#JsonArrayTesttestNullJsonElementAddition)
    - [`com.google.gson.JsonArrayTest.testSameAddition`](#JsonArrayTesttestSameAddition)
    - [`com.google.gson.JsonArrayTest.testToString`](#JsonArrayTesttestToString)

**Methods**

---
#### JsonArrayTest\.testEqualsOnEmptyArray<!-- {{#callable:com.google.gson.JsonArrayTest.testEqualsOnEmptyArray}} -->
The `testEqualsOnEmptyArray` method tests the equality and hash code consistency of two empty `JsonArray` instances.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method creates two new instances of `JsonArray`, both of which are empty.
    - It calls `MoreAsserts.assertEqualsAndHashCode` to verify that the two empty `JsonArray` instances are equal and have the same hash code.
- **Output**:
    - The method does not return any value; it is a test method that asserts conditions.
- **Functions called**:
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testEqualsNonEmptyArray<!-- {{#callable:com.google.gson.JsonArrayTest.testEqualsNonEmptyArray}} -->
The `testEqualsNonEmptyArray` method tests the equality and hash code behavior of non-empty `JsonArray` instances under various conditions.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize two empty `JsonArray` instances, `a` and `b`.
    - Use `EqualsTester` to verify that two empty arrays are considered equal.
    - Add a `JsonObject` to `a` and assert that `a` and `b` are not equal.
    - Add a `JsonObject` to `b` and use `MoreAsserts.assertEqualsAndHashCode` to verify that `a` and `b` are now equal and have the same hash code.
    - Add another `JsonObject` to `a` and assert that `a` and `b` are not equal.
    - Add `JsonNull.INSTANCE` to `b` and assert that `a` and `b` are not equal.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code behavior of `JsonArray` instances.
- **Functions called**:
    - [`com.google.gson.JsonPrimitiveTest.testEquals`](JsonPrimitiveTest.java.driver.md#JsonPrimitiveTesttestEquals)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testRemove<!-- {{#callable:com.google.gson.JsonArrayTest.testRemove}} -->
The `testRemove` method tests the removal functionality of the `JsonArray` class, ensuring correct behavior when removing elements by index and by object reference.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - An assertion is made that removing an element at index 0 throws an `IndexOutOfBoundsException`.
    - A `JsonPrimitive` object `a` with the value "a" is created and added to the array.
    - An assertion checks that removing `a` from the array returns `true`, and another assertion checks that `a` is no longer in the array.
    - The `JsonPrimitive` `a` is added back to the array, followed by another `JsonPrimitive` with the value "b".
    - An assertion checks that removing the element at index 1 returns a `JsonPrimitive` with the value "b".
    - Assertions verify that the array now has a size of 1 and contains the `JsonPrimitive` `a`.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the correct behavior of the [`remove`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayremove) method in `JsonArray` through assertions.
- **Functions called**:
    - [`com.google.gson.JsonArray.remove`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayremove)
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonPrimitive.getAsString`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsString)
    - [`com.google.gson.JsonArray.contains`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testSet<!-- {{#callable:com.google.gson.JsonArrayTest.testSet}} -->
The `testSet` method tests the behavior of the [`set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset) method in a `JsonArray` for various scenarios, including setting elements at specific indices and handling null values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - An `IndexOutOfBoundsException` is asserted when attempting to set an element at index 0 in the empty array.
    - A `JsonPrimitive` with value "a" is added to the array.
    - A `JsonPrimitive` with value "b" is set at index 0, replacing "a", and the old value is asserted to be "a".
    - The element at index 0 is set to `null`, and the old value is asserted to be "b"; the new value is asserted to be `JsonNull.INSTANCE`.
    - A `JsonPrimitive` with value "c" is set at index 0, replacing `JsonNull.INSTANCE`, and the old value is asserted to be `JsonNull.INSTANCE`.
    - The final state of the array is asserted to have size 1.
- **Output**:
    - The method does not return a value but uses assertions to verify the expected behavior of the [`set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset) method in `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget)
    - [`com.google.gson.JsonPrimitive.getAsString`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testDeepCopy<!-- {{#callable:com.google.gson.JsonArrayTest.testDeepCopy}} -->
The `testDeepCopy` method verifies that a deep copy of a `JsonArray` is independent of the original array after modifications.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new `JsonArray` named `original`.
    - Create another `JsonArray` named `firstEntry` and add it to `original`.
    - Perform a deep copy of `original` into a new `JsonArray` named `copy`.
    - Add a new `JsonPrimitive` with value "y" to `original`.
    - Assert that `copy` has a size of 1, confirming it is unaffected by the addition to `original`.
    - Add a new `JsonPrimitive` with value "z" to `firstEntry`.
    - Assert that the first element of `original` has a size of 1, confirming the addition to `firstEntry`.
    - Assert that the first element of `copy` has a size of 0, confirming it is unaffected by the addition to `firstEntry`.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of the deep copy operation.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonElement.deepCopy`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementdeepCopy)
    - [`com.google.gson.JsonArray.get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget)
    - [`com.google.gson.JsonElement.getAsJsonArray`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonArray)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testIsEmpty<!-- {{#callable:com.google.gson.JsonArrayTest.testIsEmpty}} -->
The `testIsEmpty` method verifies the behavior of a `JsonArray` when checking if it is empty or not after adding and removing elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created and asserted to be empty using `assertThat(array).isEmpty()`.
    - A `JsonPrimitive` with the value "a" is created and added to the `JsonArray`, then the array is asserted to be not empty using `assertThat(array).isNotEmpty()`.
    - The element at index 0 is removed from the `JsonArray`, and the array is asserted to be empty again using `assertThat(array).isEmpty()`.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts the expected behavior of the `JsonArray` being empty or not at different stages.
- **Functions called**:
    - [`com.google.gson.JsonObject.isEmpty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectisEmpty)
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.remove`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayremove)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testFailedGetArrayValues<!-- {{#callable:com.google.gson.JsonArrayTest.testFailedGetArrayValues}} -->
The `testFailedGetArrayValues` method tests various failure scenarios when attempting to retrieve values from a `JsonArray` using incorrect methods or indices.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` is created and a JSON object is added to it as a string.
    - The method asserts that calling `getAsBoolean()` on the `JsonArray` throws an `UnsupportedOperationException` with the message 'JsonObject'.
    - It asserts that accessing an invalid index (-1) throws an `IndexOutOfBoundsException` with the appropriate message.
    - The method checks that calling `getAsString()` throws an `UnsupportedOperationException` with the message 'JsonObject'.
    - The JSON object is removed from the array, and a string 'hello' is added.
    - It asserts that calling `getAsDouble()` and `getAsInt()` on the array throws a `NumberFormatException` with the message 'For input string: "hello"'.
    - The method checks that calling `get(0).getAsJsonArray()` throws an `IllegalStateException` with the message 'Not a JSON Array: "hello"'.
    - It asserts that calling `getAsJsonObject()` throws an `IllegalStateException` with the message 'Not a JSON Object: ["hello"]'.
    - Finally, it checks that calling `getAsLong()` throws a `NumberFormatException` with the message 'For input string: "hello"'.
- **Output**:
    - The method does not return any value; it is a test method that verifies exceptions are thrown under specific conditions.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonParser.parseString`](../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.JsonElement.getAsBoolean`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsBoolean)
    - [`com.google.gson.JsonArray.get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
    - [`com.google.gson.JsonArray.remove`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayremove)
    - [`com.google.gson.JsonArray.getAsDouble`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraygetAsDouble)
    - [`com.google.gson.JsonPrimitive.getAsInt`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt)
    - [`com.google.gson.JsonElement.getAsJsonArray`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonArray)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonArray.getAsLong`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraygetAsLong)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testGetAs\_WrongArraySize<!-- {{#callable:com.google.gson.JsonArrayTest.testGetAs_WrongArraySize}} -->
The method `testGetAs_WrongArraySize` tests that the [`getAsByte`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsByte) method of a `JsonArray` throws an `IllegalStateException` when the array size is not exactly one.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - The method `assertThrows` is used to verify that calling [`getAsByte`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsByte) on an empty `JsonArray` throws an `IllegalStateException` with the message 'Array must have size 1, but has size 0'.
    - Two boolean values, `true` and `false`, are added to the `JsonArray`.
    - The method `assertThrows` is used again to verify that calling [`getAsByte`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsByte) on the `JsonArray` with two elements throws an `IllegalStateException` with the message 'Array must have size 1, but has size 2'.
- **Output**:
    - The method does not return any value; it verifies that exceptions are thrown under specific conditions.
- **Functions called**:
    - [`com.google.gson.JsonElement.getAsByte`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsByte)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testStringPrimitiveAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testStringPrimitiveAddition}} -->
The `testStringPrimitiveAddition` method tests the addition of string and null values to a `JsonArray` and verifies the resulting JSON string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - Several string values ('Hello', 'Goodbye', 'Thank you', 'Yes') and a null value are added to the `JsonArray`.
    - The method uses an assertion to check if the `JsonArray`'s string representation matches the expected JSON format '["Hello","Goodbye","Thank you",null,"Yes"]'.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the `JsonArray`'s content.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testIntegerPrimitiveAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testIntegerPrimitiveAddition}} -->
The `testIntegerPrimitiveAddition` method tests the addition of integer primitives and null values to a `JsonArray` and verifies the resulting JSON string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - An integer variable `x` is initialized to 1 and added to the `JsonArray`.
    - The variable `x` is reassigned to 2 and added to the `JsonArray`.
    - The variable `x` is reassigned to -3 and added to the `JsonArray`.
    - A null value is explicitly added to the `JsonArray` as an `Integer`.
    - The variable `x` is reassigned to 4 and added to the `JsonArray`.
    - The variable `x` is reassigned to 0 and added to the `JsonArray`.
    - An assertion checks that the string representation of the `JsonArray` matches the expected JSON string '[1,2,-3,null,4,0]'.
- **Output**:
    - The method does not return a value but asserts that the `JsonArray`'s string representation is equal to '[1,2,-3,null,4,0]'.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testDoublePrimitiveAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testDoublePrimitiveAddition}} -->
The `testDoublePrimitiveAddition` method tests the addition of double primitive values and nulls to a `JsonArray` and verifies the resulting JSON string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - A double variable `x` is initialized to 1.0 and added to the `JsonArray`.
    - The variable `x` is updated to 2.13232 and added to the `JsonArray`.
    - The variable `x` is updated to 0.121 and added to the `JsonArray`.
    - A null value is explicitly added to the `JsonArray` as a `Double` object.
    - The variable `x` is updated to -0.00234 and added to the `JsonArray`.
    - Another null value is explicitly added to the `JsonArray` as a `Double` object.
    - The method asserts that the string representation of the `JsonArray` matches the expected JSON string '[1.0,2.13232,0.121,null,-0.00234,null]'.
- **Output**:
    - The method does not return any value, but it asserts that the `JsonArray`'s string representation is equal to the expected JSON string.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testBooleanPrimitiveAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testBooleanPrimitiveAddition}} -->
The `testBooleanPrimitiveAddition` method tests the addition of boolean values, including null, to a `JsonArray` and verifies the resulting JSON string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - Boolean values `true`, `true`, `false`, `false`, and `null` are added to the `JsonArray`.
    - Another `true` boolean value is added to the `JsonArray`.
    - The method asserts that the string representation of the `JsonArray` matches the expected JSON string '[true,true,false,false,null,true]'.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the `JsonArray` content.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testCharPrimitiveAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testCharPrimitiveAddition}} -->
The `testCharPrimitiveAddition` method tests the addition of various character and string elements to a `JsonArray` and verifies the resulting JSON string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - Characters 'a', 'e', 'i', and 'u' are added to the `JsonArray`.
    - The character with ASCII value 111 ('o') is added to the `JsonArray`.
    - A `null` character is added to the `JsonArray`, which is represented as `null` in JSON.
    - The string "and sometimes Y" is added to the `JsonArray`.
    - The [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) method of `JsonArray` is called to get its JSON string representation.
    - An assertion checks if the JSON string representation matches the expected value `["a","e","i","o",null,"u","and sometimes Y"]`.
- **Output**:
    - The method does not return any value, but it asserts that the JSON string representation of the `JsonArray` matches the expected output.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testMixedPrimitiveAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testMixedPrimitiveAddition}} -->
The `testMixedPrimitiveAddition` method tests the addition of various primitive types and null values to a `JsonArray` and verifies the resulting JSON string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - Various elements are added to the `JsonArray`, including a character, a string, an integer, a character cast from an integer, and null values cast to `Boolean` and `Character`.
    - Assertions are made to check that null values are correctly represented as `JsonNull.INSTANCE` in the `JsonArray`.
    - Additional elements, a double and a `BigInteger`, are added to the `JsonArray`.
    - The final state of the `JsonArray` is asserted to match the expected JSON string representation.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonObject.size`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectsize)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testNullPrimitiveAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testNullPrimitiveAddition}} -->
The `testNullPrimitiveAddition` method tests the addition of various null primitive types to a `JsonArray` and verifies that they are stored as `JsonNull` instances.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - Various null primitive types (Character, Boolean, Integer, Double, Float, BigInteger, String, Boolean, Number) are added to the `JsonArray`.
    - The method asserts that the `JsonArray`'s string representation is a list of nulls.
    - A loop iterates over each element in the `JsonArray` to assert that each element is a `JsonNull` instance.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonArray` when null primitives are added.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
    - [`com.google.gson.JsonObject.size`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectsize)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testNullJsonElementAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testNullJsonElementAddition}} -->
The method `testNullJsonElementAddition` tests the behavior of adding a null `JsonElement` to a `JsonArray` and verifies that it is stored as `JsonNull.INSTANCE`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - A null `JsonElement` is added to the `JsonArray`.
    - An assertion checks that the first element of the `JsonArray` is `JsonNull.INSTANCE`.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that a null `JsonElement` is stored as `JsonNull.INSTANCE` in the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testSameAddition<!-- {{#callable:com.google.gson.JsonArrayTest.testSameAddition}} -->
The `testSameAddition` method tests the addition of duplicate primitive values and nulls to a `JsonArray` and verifies the resulting JSON string representation.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created.
    - The method adds duplicate values of different types (character, boolean, integer, double) and nulls to the `JsonArray`.
    - The method uses `assertThat` to verify that the `JsonArray`'s string representation matches the expected JSON format with duplicates and nulls.
- **Output**:
    - The method does not return a value; it performs assertions to validate the behavior of the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)


---
#### JsonArrayTest\.testToString<!-- {{#callable:com.google.gson.JsonArrayTest.testToString}} -->
The `testToString` method verifies the string representation of a `JsonArray` with various elements, including nulls, special characters, nested arrays, and objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance is created and its string representation is asserted to be an empty array '[]'.
    - The `JsonArray` is populated with various elements: a `JsonNull` instance, a `Float.NaN`, a string containing a null character, a nested `JsonArray` containing a double quote character, and a `JsonObject` with a property containing a null character.
    - The string representation of the populated `JsonArray` is asserted to match the expected JSON string '[null,NaN,"a\u0000",["\""],{"n\u0000":1}]'.
- **Output**:
    - The method does not return any value; it uses assertions to validate the expected string representation of the `JsonArray`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
- **See also**: [`com.google.gson.JsonArrayTest`](#JsonArrayTest)  (Base Class)



