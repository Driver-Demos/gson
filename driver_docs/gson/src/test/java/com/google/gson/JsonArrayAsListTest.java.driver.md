# Purpose
The `JsonArrayAsListTest` class is a comprehensive test suite designed to validate the functionality of the `asList()` method in the `JsonArray` class from the Google Gson library. This test class ensures that the `asList()` method, which provides a view of the `JsonArray` as a `List<JsonElement>`, behaves correctly according to the Java Collections Framework standards. The tests cover a wide range of operations that can be performed on the list view, including element retrieval, size checking, element setting, addition, removal, and clearing of elements. Additionally, the tests verify the behavior of the list when interacting with null elements, ensuring that appropriate exceptions are thrown when necessary.

The test suite also includes tests for more advanced list operations such as sorting, replacing elements, converting the list to an array, and checking equality and hash code consistency. The [`testViewUpdates`](#JsonArrayAsListTesttestViewUpdates) method specifically verifies that changes to the `JsonArray` are reflected in the list view and vice versa, ensuring that the list view is a dynamic representation of the `JsonArray`. This suite uses assertions from the `Truth` library and JUnit's `assertThrows` to validate expected outcomes and exceptions, providing a robust framework for ensuring the integrity and reliability of the `asList()` method in various scenarios.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.gson.common.MoreAsserts`
- `java.util.Arrays`
- `java.util.Collections`
- `java.util.Comparator`
- `java.util.List`
- `java.util.Spliterator`
- `java.util.stream.Collectors`
- `java.util.stream.StreamSupport`
- `org.junit.Test`


# Classes

---
### JsonArrayAsListTest<!-- {{#class:com.google.gson.JsonArrayAsListTest}} -->
- **Modifiers**: `public`
- **Description**: The `JsonArrayAsListTest` class is a comprehensive test suite for verifying the functionality of the `JsonArray#asList()` method in the Gson library. It includes a variety of test cases to ensure that the list view of a `JsonArray` behaves correctly, covering operations such as getting, setting, adding, removing elements, and checking the size and contents of the list. The tests also verify that changes to the `JsonArray` are reflected in the list view and vice versa, and they handle edge cases like null elements and index out-of-bounds exceptions.
- **Methods**:
    - [`com.google.gson.JsonArrayAsListTest.testGet`](#JsonArrayAsListTesttestGet)
    - [`com.google.gson.JsonArrayAsListTest.testSize`](#JsonArrayAsListTesttestSize)
    - [`com.google.gson.JsonArrayAsListTest.testSet`](#JsonArrayAsListTesttestSet)
    - [`com.google.gson.JsonArrayAsListTest.testAdd`](#JsonArrayAsListTesttestAdd)
    - [`com.google.gson.JsonArrayAsListTest.testAddAll`](#JsonArrayAsListTesttestAddAll)
    - [`com.google.gson.JsonArrayAsListTest.testRemoveIndex`](#JsonArrayAsListTesttestRemoveIndex)
    - [`com.google.gson.JsonArrayAsListTest.testRemoveElement`](#JsonArrayAsListTesttestRemoveElement)
    - [`com.google.gson.JsonArrayAsListTest.testClear`](#JsonArrayAsListTesttestClear)
    - [`com.google.gson.JsonArrayAsListTest.testContains`](#JsonArrayAsListTesttestContains)
    - [`com.google.gson.JsonArrayAsListTest.testIndexOf`](#JsonArrayAsListTesttestIndexOf)
    - [`com.google.gson.JsonArrayAsListTest.spliteratorToList`](#JsonArrayAsListTestspliteratorToList)
    - [`com.google.gson.JsonArrayAsListTest.testSpliterator`](#JsonArrayAsListTesttestSpliterator)
    - [`com.google.gson.JsonArrayAsListTest.testSort`](#JsonArrayAsListTesttestSort)
    - [`com.google.gson.JsonArrayAsListTest.testReplaceAll`](#JsonArrayAsListTesttestReplaceAll)
    - [`com.google.gson.JsonArrayAsListTest.testToArray`](#JsonArrayAsListTesttestToArray)
    - [`com.google.gson.JsonArrayAsListTest.testEqualsHashCode`](#JsonArrayAsListTesttestEqualsHashCode)
    - [`com.google.gson.JsonArrayAsListTest.testViewUpdates`](#JsonArrayAsListTesttestViewUpdates)

**Methods**

---
#### JsonArrayAsListTest\.testGet<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testGet}} -->
The `testGet` method tests the behavior of the [`get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget) method on a `List` view of a `JsonArray`, including valid and invalid index access and handling of null elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonArray` object `a` is created and an integer `1` is added to it.
    - The [`asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList) method is called on `a` to obtain a `List<JsonElement>` view of the array.
    - The method asserts that the first element of the list is equal to a `JsonPrimitive` containing `1`.
    - It checks that accessing an invalid index (-1 and 2) throws an `IndexOutOfBoundsException`.
    - A `null` element is added to the `JsonArray`, and the method asserts that the second element of the list is `JsonNull.INSTANCE`.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the correct behavior of the [`get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget) method on a `List` view of a `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testSize<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testSize}} -->
The `testSize` method verifies that the size of a `JsonArray` and its corresponding `List` view updates correctly when elements are added.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonArray` instance `a` is created and an integer `1` is added to it.
    - The `asList()` method is called on `a` to obtain a `List<JsonElement>` view of the array, stored in `list`.
    - An assertion checks that the size of `list` is 1, confirming the initial addition.
    - A new `JsonPrimitive` with value `2` is added to `list`.
    - Another assertion checks that the size of `list` is now 2, confirming the successful addition of the new element.
- **Output**:
    - The method does not return any value; it uses assertions to validate the expected behavior.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testSet<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testSet}} -->
The `testSet` method tests the behavior of the [`set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset) operation on a `List` view of a `JsonArray`, including element replacement, index bounds checking, and null element handling.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonArray` and add an integer element `1` to it.
    - Convert the `JsonArray` to a `List<JsonElement>` using `asList()`.
    - Replace the element at index `0` with a new `JsonPrimitive` containing `2` and store the old element.
    - Assert that the old element is equal to a `JsonPrimitive` containing `1`.
    - Assert that the element at index `0` in the list is now a `JsonPrimitive` containing `2`.
    - Assert that the element at index `0` in the original `JsonArray` is also a `JsonPrimitive` containing `2`.
    - Attempt to set an element at an invalid negative index and assert that it throws an `IndexOutOfBoundsException`.
    - Attempt to set an element at an index beyond the current size and assert that it throws an `IndexOutOfBoundsException`.
    - Attempt to set a `null` element at index `0` and assert that it throws a `NullPointerException` with a specific message.
- **Output**:
    - The method does not return a value; it uses assertions to validate the behavior of the [`set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset) operation on the list.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.JsonArray.get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testAdd<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testAdd}} -->
The `testAdd` method tests the behavior of adding elements to a `JsonArray` and its corresponding list view, including handling of null elements and index bounds.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `JsonArray` and add an integer element to it.
    - Convert the `JsonArray` to a `List<JsonElement>` using `asList()`.
    - Add elements at specific indices in the list and verify the additions using assertions.
    - Check that adding elements to the list returns `true` for successful additions.
    - Create an expected list and assert that the modified list matches this expected list.
    - Test for `IndexOutOfBoundsException` by attempting to set elements at invalid indices.
    - Test for `NullPointerException` by attempting to add null elements to the list and verify the exception message.
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of the list operations.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.set`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayset)
    - [`com.google.gson.JsonArray.size`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraysize)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testAddAll<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testAddAll}} -->
The `testAddAll` method tests the functionality of adding multiple elements to a `JsonArray`'s list view and ensures that null elements are not allowed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `JsonArray` and add a single element (1) to it.
    - Convert the `JsonArray` to a `List<JsonElement>` using `asList()`.
    - Add multiple elements (2 and 3) to the list using [`addAll`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayaddAll) method.
    - Create an expected list with elements 1, 2, and 3 and assert that the list matches this expected list.
    - Attempt to add a null element to the list using [`addAll`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayaddAll) with an index, expecting a `NullPointerException`.
    - Attempt to add a null element to the list using [`addAll`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayaddAll) without an index, expecting a `NullPointerException`.
- **Output**:
    - The method does not return any value but performs assertions to validate the behavior of the [`addAll`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayaddAll) method on a list view of a `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.addAll`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayaddAll)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testRemoveIndex<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testRemoveIndex}} -->
The `testRemoveIndex` method tests the removal of an element by index from a `JsonArray` and verifies the behavior when attempting to remove from an empty list.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new `JsonArray` instance and add a single element with value `1`.
    - Convert the `JsonArray` to a `List<JsonElement>` using `asList()`.
    - Remove the element at index `0` from the list and assert that the removed element is equal to a `JsonPrimitive` with value `1`.
    - Assert that the list is now empty by checking its size is `0`.
    - Assert that the original `JsonArray` is also empty by checking its size is `0`.
    - Attempt to remove an element at index `0` from the now-empty list and assert that this throws an `IndexOutOfBoundsException`.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the correct behavior of element removal by index and exception handling in a `JsonArray`.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.remove`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayremove)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testRemoveElement<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testRemoveElement}} -->
The `testRemoveElement` method tests the removal of elements from a `JsonArray` and its corresponding list view, ensuring that the removal operation behaves as expected.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonArray` object `a` is created and an integer `1` is added to it.
    - The `asList()` method is called on `a` to obtain a `List<JsonElement>` view of the array, stored in `list`.
    - The method asserts that removing a `JsonPrimitive` with value `1` from `list` returns `true`, indicating successful removal.
    - It then checks that both `list` and `a` have a size of `0` after the removal, confirming that the element was removed from both the list view and the original array.
    - The method asserts that attempting to remove a `JsonPrimitive` with value `1` again returns `false`, indicating the element is no longer present.
    - It also asserts that removing `null` from `list` returns `false`, as `null` is not present in the list.
- **Output**:
    - The method does not return any value; it uses assertions to verify the correctness of the removal operations.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.remove`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayremove)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testClear<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testClear}} -->
The `testClear` method verifies that clearing a list view of a `JsonArray` also clears the original `JsonArray`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new `JsonArray` instance `a` and add an integer element `1` to it.
    - Convert the `JsonArray` `a` to a `List<JsonElement>` using the `asList()` method and store it in `list`.
    - Call the `clear()` method on `list` to remove all elements from the list.
    - Use assertions to verify that both `list` and the original `JsonArray` `a` have a size of 0, confirming that both are cleared.
- **Output**:
    - The method does not return any value as it is a test method, but it asserts that both the list and the original `JsonArray` are empty after clearing.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testContains<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testContains}} -->
The `testContains` method verifies the behavior of the [`contains`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains) method on a `List` view of a `JsonArray`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonArray` object `a` is created and the integer `1` is added to it.
    - The [`asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList) method is called on `a` to obtain a `List<JsonElement>` view named `list`.
    - Assertions are made to check that `list` contains a `JsonPrimitive` with value `1`, and does not contain a `JsonPrimitive` with value `2` or `null`.
    - A boolean variable `containsInt` is assigned the result of checking if `list` contains the integer `1`, which should be `false` since `list` should only contain `JsonPrimitive` objects.
    - An assertion is made to verify that `containsInt` is `false`.
- **Output**:
    - The method does not return any value; it uses assertions to validate the expected behavior of the [`contains`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains) method.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.contains`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testIndexOf<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testIndexOf}} -->
The `testIndexOf` method tests the behavior of the `indexOf` and `lastIndexOf` methods on a `JsonArray` converted to a `List`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonArray` object `a` is created and the integer `1` is added twice to it.
    - The `JsonArray` is converted to a `List<JsonElement>` called `list`.
    - The method asserts that the index of the first occurrence of `JsonPrimitive(1)` in `list` is `0`.
    - It asserts that the index of `JsonPrimitive(2)` and `null` in `list` is `-1`, indicating they are not present.
    - A suppressed warning is used to check the index of the integer `1` directly, which should return `-1` since the list contains `JsonPrimitive(1)`, not the integer `1`.
    - The method asserts that the last index of `JsonPrimitive(1)` in `list` is `1`, confirming the second occurrence.
    - It asserts that the last index of `JsonPrimitive(2)` and `null` in `list` is `-1`, indicating they are not present.
- **Output**:
    - The method does not return any value; it uses assertions to validate the expected behavior of `indexOf` and `lastIndexOf` methods.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.spliteratorToList<!-- {{#callable:com.google.gson.JsonArrayAsListTest.spliteratorToList}} -->
The `spliteratorToList` method converts a given `Spliterator` into a `List` by streaming its elements and collecting them into a list.
- **Modifiers**: `private`
- **Inputs**:
    - `spliterator`: A `Spliterator` of type `T` that provides a sequence of elements to be converted into a list.
- **Control Flow**:
    - The method uses `StreamSupport.stream` to create a sequential stream from the provided `Spliterator`.
    - The stream is then collected into a `List` using `Collectors.toList()`.
    - The resulting list is returned as the output of the method.
- **Output**:
    - A `List` containing all elements from the input `Spliterator`.
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testSpliterator<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testSpliterator}} -->
The `testSpliterator` method tests the conversion of a `JsonArray` to a `List` using a `Spliterator` and verifies the order and content of the resulting list.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new `JsonArray` and add elements 1, 3, and 2 to it.
    - Convert the `JsonArray` to a `List` using `asList()` method.
    - Convert the `List` to another list using [`spliteratorToList`](#JsonArrayAsListTestspliteratorToList) method with the list's `Spliterator`.
    - Assert that the resulting list contains exactly the elements 1, 3, and 2 in order.
    - Create an empty `JsonArray` and convert it to a `List`.
    - Convert the empty `List` to another list using [`spliteratorToList`](#JsonArrayAsListTestspliteratorToList) method with the list's `Spliterator`.
    - Assert that the resulting list is empty.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the [`spliteratorToList`](#JsonArrayAsListTestspliteratorToList) conversion.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArrayAsListTest.spliteratorToList`](#JsonArrayAsListTestspliteratorToList)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testSort<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testSort}} -->
The `testSort` method tests the sorting functionality of a `JsonArray` converted to a `List` of `JsonElement` objects, ensuring proper sorting and handling of non-comparable elements.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonArray` and add three integer elements: 1, 3, and 2.
    - Convert the `JsonArray` to a `List` of `JsonElement` using `asList()`.
    - Attempt to sort the list using `list.sort(null)`, which should throw a `ClassCastException` because `JsonElement` does not implement `Comparable`.
    - Sort the list using a `Comparator` that compares the integer values of `JsonElement` objects using `JsonElement::getAsInt`.
    - Assert that the sorted list contains the elements 1, 2, and 3 in order.
    - Assert that the original `JsonArray` also reflects the sorted order of elements.
- **Output**:
    - The method does not return a value but asserts the correct sorting behavior and exception handling of the `JsonArray` and its corresponding `List`.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testReplaceAll<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testReplaceAll}} -->
The `testReplaceAll` method tests the functionality of replacing all elements in a `JsonArray` with their negated integer values and verifies the behavior when attempting to replace elements with null.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `JsonArray` is created and populated with the integers 1, 3, and 2.
    - The `asList()` method is called on the `JsonArray` to obtain a `List<JsonElement>`.
    - The `replaceAll` method is used on the list to replace each element with its negated integer value using a lambda expression.
    - Assertions are made to verify that the list and the original `JsonArray` contain the negated values -1, -3, and -2 in order.
    - An attempt is made to replace all elements with `null`, which is expected to throw a `NullPointerException`.
    - An assertion checks that the exception message is 'Element must be non-null'.
- **Output**:
    - The method does not return a value but performs assertions to verify the correctness of the `replaceAll` operation and exception handling.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonPrimitive.getAsInt`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsInt)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testToArray<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testToArray}} -->
The `testToArray` method verifies the behavior of converting a `JsonArray` to an array using the `toArray` method in various scenarios.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonArray` instance and add a single integer element to it.
    - Convert the `JsonArray` to a `List<JsonElement>` using `asList()`.
    - Assert that converting the list to an array without specifying a type results in an array containing a `JsonPrimitive` of the integer.
    - Convert the list to a `JsonElement` array with an initial size of 0 and assert the result is as expected.
    - Create a `JsonElement` array with a size of 1, convert the list to this array, and assert the result is as expected.
    - Create a `JsonElement` array with two elements, one being `null`, convert the list to this array, and assert that the first element is replaced and the second remains `null`.
- **Output**:
    - The method does not return a value; it uses assertions to verify the correctness of the `toArray` method's behavior.
- **Functions called**:
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testEqualsHashCode<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testEqualsHashCode}} -->
The `testEqualsHashCode` method verifies the equality and hash code consistency of a `JsonArray` converted to a `List` with expected values.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `JsonArray` instance and add an integer value `1` to it.
    - Convert the `JsonArray` to a `List<JsonElement>` using the `asList()` method.
    - Use `MoreAsserts.assertEqualsAndHashCode` to assert that the list is equal to a singleton list containing a `JsonPrimitive` with value `1` and that their hash codes are consistent.
    - Assert that the list is not equal to an empty list using `assertThat` and `isFalse()`.
    - Assert that the list is not equal to a singleton list containing a `JsonPrimitive` with value `2` using `assertThat` and `isFalse()`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the [`equals`](GsonTest.java.driver.md#DummyFactoryequals) and `hashCode` methods.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
    - [`com.google.gson.GsonTest.testGetDelegateAdapter.DummyFactory.equals`](GsonTest.java.driver.md#DummyFactoryequals)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)


---
#### JsonArrayAsListTest\.testViewUpdates<!-- {{#callable:com.google.gson.JsonArrayAsListTest.testViewUpdates}} -->
The `testViewUpdates` method verifies that updates to a `JsonArray` are reflected in its list view and vice versa.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new `JsonArray` instance `a`.
    - Obtain a list view of `a` using `a.asList()` and store it in `list`.
    - Add an integer `1` to the `JsonArray` `a`.
    - Assert that the list view `list` has a size of 1 and its first element is equal to a `JsonPrimitive` of 1.
    - Add a `JsonPrimitive` of 2 to the list view `list`.
    - Assert that the `JsonArray` `a` now has a size of 2 and its second element is equal to a `JsonPrimitive` of 2.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of the `JsonArray` and its list view.
- **Functions called**:
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.add`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayadd)
    - [`com.google.gson.JsonArray.get`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayget)
- **See also**: [`com.google.gson.JsonArrayAsListTest`](#JsonArrayAsListTest)  (Base Class)



