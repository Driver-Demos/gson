# Purpose
The `JsonObjectTest` class is a comprehensive suite of unit tests designed to validate the functionality of the `JsonObject` class from the Google Gson library. This test class ensures that the `JsonObject` class behaves as expected when performing various operations such as adding, removing, and manipulating properties. The tests cover a wide range of scenarios, including adding properties with different data types (e.g., strings, booleans, characters), handling null values, and managing properties with special characters or empty names. Additionally, the tests verify the correct behavior of methods like `size()`, `isEmpty()`, `deepCopy()`, and the preservation of insertion order in key and entry sets.

The test class also includes specific tests for edge cases and bug reports, such as handling properties with quotes and empty string names, as well as ensuring the correct implementation of `equals()` and `hashCode()` methods. The use of assertions from the `Truth` library and JUnit's `assertThrows` method ensures that the tests are both expressive and robust. By thoroughly testing the `JsonObject` class, this file plays a crucial role in maintaining the reliability and correctness of the Gson library's JSON manipulation capabilities.
# Imports and Dependencies

---
- `com.google.gson`
- `com.google.common.truth.Truth.assertThat`
- `org.junit.Assert.assertThrows`
- `com.google.common.testing.EqualsTester`
- `com.google.gson.common.MoreAsserts`
- `java.util.AbstractMap.SimpleEntry`
- `java.util.ArrayDeque`
- `java.util.ArrayList`
- `java.util.Arrays`
- `java.util.Collections`
- `java.util.Deque`
- `java.util.Iterator`
- `java.util.List`
- `java.util.Map.Entry`
- `java.util.Set`
- `org.junit.Test`


# Classes

---
### JsonObjectTest<!-- {{#class:com.google.gson.JsonObjectTest}} -->
- **Modifiers**: `public`
- **Description**: The `JsonObjectTest` class is a comprehensive unit test suite for the `JsonObject` class from the Gson library, designed to validate the functionality of JSON object manipulation, including adding, removing, and modifying properties, handling null and empty values, and ensuring correct behavior of equality, hash code, and deep copy operations. It also tests the preservation of insertion order in key and entry sets, and verifies the correct serialization of JSON objects to strings.
- **Methods**:
    - [`com.google.gson.JsonObjectTest.testAddingAndRemovingObjectProperties`](#JsonObjectTesttestAddingAndRemovingObjectProperties)
    - [`com.google.gson.JsonObjectTest.testAddingNullPropertyValue`](#JsonObjectTesttestAddingNullPropertyValue)
    - [`com.google.gson.JsonObjectTest.testAddingNullOrEmptyPropertyName`](#JsonObjectTesttestAddingNullOrEmptyPropertyName)
    - [`com.google.gson.JsonObjectTest.testAddingBooleanProperties`](#JsonObjectTesttestAddingBooleanProperties)
    - [`com.google.gson.JsonObjectTest.testAddingStringProperties`](#JsonObjectTesttestAddingStringProperties)
    - [`com.google.gson.JsonObjectTest.testAddingCharacterProperties`](#JsonObjectTesttestAddingCharacterProperties)
    - [`com.google.gson.JsonObjectTest.testPropertyWithQuotes`](#JsonObjectTesttestPropertyWithQuotes)
    - [`com.google.gson.JsonObjectTest.testWritePropertyWithEmptyStringName`](#JsonObjectTesttestWritePropertyWithEmptyStringName)
    - [`com.google.gson.JsonObjectTest.testReadPropertyWithEmptyStringName`](#JsonObjectTesttestReadPropertyWithEmptyStringName)
    - [`com.google.gson.JsonObjectTest.testEqualsOnEmptyObject`](#JsonObjectTesttestEqualsOnEmptyObject)
    - [`com.google.gson.JsonObjectTest.testEqualsNonEmptyObject`](#JsonObjectTesttestEqualsNonEmptyObject)
    - [`com.google.gson.JsonObjectTest.testEqualsHashCodeIgnoringOrder`](#JsonObjectTesttestEqualsHashCodeIgnoringOrder)
    - [`com.google.gson.JsonObjectTest.testSize`](#JsonObjectTesttestSize)
    - [`com.google.gson.JsonObjectTest.testIsEmpty`](#JsonObjectTesttestIsEmpty)
    - [`com.google.gson.JsonObjectTest.testDeepCopy`](#JsonObjectTesttestDeepCopy)
    - [`com.google.gson.JsonObjectTest.testKeySet`](#JsonObjectTesttestKeySet)
    - [`com.google.gson.JsonObjectTest.testEntrySet`](#JsonObjectTesttestEntrySet)
    - [`com.google.gson.JsonObjectTest.testToString`](#JsonObjectTesttestToString)

**Methods**

---
#### JsonObjectTest\.testAddingAndRemovingObjectProperties<!-- {{#callable:com.google.gson.JsonObjectTest.testAddingAndRemovingObjectProperties}} -->
This method tests the addition and removal of properties in a JsonObject, ensuring correct behavior and state changes.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new JsonObject instance is created.
    - A property name 'property' is defined as a String.
    - The method asserts that the JsonObject does not initially have the property and that its value is null.
    - A JsonPrimitive with the value 'blah' is created and added to the JsonObject under the property name.
    - The method asserts that the property now exists in the JsonObject and its value is equal to the JsonPrimitive added.
    - The property is removed from the JsonObject, and the method asserts that the removed element is equal to the previously added JsonPrimitive.
    - The method asserts that the property no longer exists in the JsonObject and its value is null after removal.
    - The method asserts that attempting to remove the property again returns null.
- **Output**:
    - The method does not return any value; it uses assertions to verify the correct behavior of adding and removing properties in a JsonObject.
- **Functions called**:
    - [`com.google.gson.JsonObject.has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.remove`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectremove)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testAddingNullPropertyValue<!-- {{#callable:com.google.gson.JsonObjectTest.testAddingNullPropertyValue}} -->
The method `testAddingNullPropertyValue` tests the behavior of adding a null value to a `JsonObject` and verifies that it is stored as a `JsonNull`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `String` variable `propertyName` is initialized with the value "property".
    - A new `JsonObject` instance `jsonObj` is created.
    - The method [`add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd) is called on `jsonObj` with `propertyName` and `null` as arguments, adding a null property value to the JSON object.
    - An assertion checks that `jsonObj` has the property `propertyName`, expecting it to be true.
    - A `JsonElement` `jsonElement` is retrieved from `jsonObj` using [`get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget) with `propertyName`.
    - Assertions verify that `jsonElement` is not null and that it is an instance of `JsonNull`.
- **Output**:
    - The method does not return any value as it is a test method; it uses assertions to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.isJsonNull`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementisJsonNull)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testAddingNullOrEmptyPropertyName<!-- {{#callable:com.google.gson.JsonObjectTest.testAddingNullOrEmptyPropertyName}} -->
The method `testAddingNullOrEmptyPropertyName` tests the behavior of adding null or empty property names to a `JsonObject`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonObject` instance is created.
    - The method asserts that adding a null property name to the `JsonObject` throws a `NullPointerException`.
    - The method adds an empty string and a string with whitespace as property names to the `JsonObject`, both with `JsonNull.INSTANCE` as their value.
    - The method asserts that the `JsonObject`'s key set contains exactly the empty string and the whitespace string.
- **Output**:
    - The method does not return any value as it is a test method, but it verifies the behavior of the `JsonObject` when handling null or empty property names.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.keySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectkeySet)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testAddingBooleanProperties<!-- {{#callable:com.google.gson.JsonObjectTest.testAddingBooleanProperties}} -->
The `testAddingBooleanProperties` method tests the addition of a boolean property to a `JsonObject` and verifies its presence and value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `String` variable `propertyName` is initialized with the value "property".
    - A new `JsonObject` instance `jsonObj` is created.
    - The method [`addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty) is called on `jsonObj` to add a boolean property with the name `propertyName` and value `true`.
    - An assertion checks that `jsonObj` has the property `propertyName` using [`has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas) method and expects it to be `true`.
    - A `JsonElement` `jsonElement` is retrieved from `jsonObj` using the [`get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget) method with `propertyName`.
    - Assertions verify that `jsonElement` is not null and that its boolean value is `true` using [`getAsBoolean`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsBoolean).
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of adding a boolean property to a `JsonObject`.
- **Functions called**:
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsBoolean`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsBoolean)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testAddingStringProperties<!-- {{#callable:com.google.gson.JsonObjectTest.testAddingStringProperties}} -->
The method `testAddingStringProperties` tests the addition of a string property to a `JsonObject` and verifies its presence and value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a string variable `propertyName` with the value 'property'.
    - Initialize a string variable `value` with the value 'blah'.
    - Create a new `JsonObject` instance named `jsonObj`.
    - Add a property to `jsonObj` with the name `propertyName` and value `value` using [`addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty).
    - Assert that `jsonObj` contains the property `propertyName` using `assertThat` and [`has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas).
    - Retrieve the `JsonElement` associated with `propertyName` from `jsonObj`.
    - Assert that the retrieved `JsonElement` is not null.
    - Assert that the string value of the `JsonElement` is equal to `value`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of adding a string property to a `JsonObject`.
- **Functions called**:
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testAddingCharacterProperties<!-- {{#callable:com.google.gson.JsonObjectTest.testAddingCharacterProperties}} -->
The `testAddingCharacterProperties` method tests the addition of a character property to a `JsonObject` and verifies its retrieval and conversion to a character.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `String` variable `propertyName` with the value "property" and a `char` variable `value` with the character 'a'.
    - Create a new `JsonObject` instance named `jsonObj`.
    - Add a property to `jsonObj` with the name `propertyName` and the value `value` using [`addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty).
    - Assert that `jsonObj` contains the property `propertyName` using `assertThat` and [`has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas).
    - Retrieve the `JsonElement` associated with `propertyName` from `jsonObj` and store it in `jsonElement`.
    - Assert that `jsonElement` is not null and its string representation equals the string value of `value`.
    - Suppress deprecation warnings and retrieve the character value from `jsonElement` using [`getAsCharacter`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsCharacter).
    - Assert that the retrieved character equals the original `value`.
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of adding and retrieving a character property in a `JsonObject`.
- **Functions called**:
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.has`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
    - [`com.google.gson.JsonPrimitive.getAsCharacter`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsCharacter)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testPropertyWithQuotes<!-- {{#callable:com.google.gson.JsonObjectTest.testPropertyWithQuotes}} -->
The `testPropertyWithQuotes` method tests the serialization of a `JsonObject` with property names and values containing quotes, ensuring they are correctly escaped in the resulting JSON string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonObject` is instantiated.
    - A property with the name `a"b` and value `c"d` is added to the `JsonObject`.
    - The `JsonObject` is serialized to a JSON string using `Gson`.
    - An assertion checks that the serialized JSON string matches the expected string `{"a\"b":"c\"d"}`.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the JSON serialization.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.TypeAdapter.toJson`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJson)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testWritePropertyWithEmptyStringName<!-- {{#callable:com.google.gson.JsonObjectTest.testWritePropertyWithEmptyStringName}} -->
The method `testWritePropertyWithEmptyStringName` tests the ability of a `JsonObject` to handle a property with an empty string as its name and verifies the JSON serialization of such an object.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonObject` instance is created.
    - An empty string is used as a property name, and a `JsonPrimitive` with a boolean value `true` is added to the `JsonObject`.
    - The `Gson` library is used to serialize the `JsonObject` to a JSON string.
    - An assertion checks that the serialized JSON string is equal to the expected string `{"":true}`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the expected behavior.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.Gson.toJson`](../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testReadPropertyWithEmptyStringName<!-- {{#callable:com.google.gson.JsonObjectTest.testReadPropertyWithEmptyStringName}} -->
The method `testReadPropertyWithEmptyStringName` tests if a JSON object can correctly read a property with an empty string as its name and verify its boolean value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string '{"":true}' is parsed into a `JsonObject` using `JsonParser.parseString` and [`getAsJsonObject`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject) methods.
    - The method retrieves the value associated with the empty string key from the `JsonObject` using `jsonObj.get("")`.
    - The retrieved value is converted to a boolean using `getAsBoolean()` and is asserted to be true using `assertThat(...).isTrue()`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the behavior of the `JsonObject`.
- **Functions called**:
    - [`com.google.gson.JsonParser.parseString`](../../../../../main/java/com/google/gson/JsonParser.java.driver.md#JsonParserparseString)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonPrimitive.getAsBoolean`](../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsBoolean)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testEqualsOnEmptyObject<!-- {{#callable:com.google.gson.JsonObjectTest.testEqualsOnEmptyObject}} -->
The method `testEqualsOnEmptyObject` tests the equality and hash code consistency of two empty `JsonObject` instances.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method creates two new instances of `JsonObject`.
    - It calls `MoreAsserts.assertEqualsAndHashCode` with these two `JsonObject` instances to verify that they are equal and have the same hash code.
- **Output**:
    - The method does not return any value; it is a test method that asserts conditions.
- **Functions called**:
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testEqualsNonEmptyObject<!-- {{#callable:com.google.gson.JsonObjectTest.testEqualsNonEmptyObject}} -->
The `testEqualsNonEmptyObject` method tests the equality and hash code behavior of `JsonObject` instances when they are modified with different properties.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create two new `JsonObject` instances, `a` and `b`.
    - Use `EqualsTester` to add `a` to an equality group and test its equality.
    - Add a property 'foo' with a new `JsonObject` to `a` and assert that `a` and `b` are not equal.
    - Add the same property 'foo' with a new `JsonObject` to `b` and assert that `a` and `b` are equal using `MoreAsserts.assertEqualsAndHashCode`.
    - Add a property 'bar' with a new `JsonObject` to `a` and assert that `a` and `b` are not equal.
    - Add a property 'bar' with `JsonNull.INSTANCE` to `b` and assert that `a` and `b` are not equal.
- **Output**:
    - The method does not return any value; it performs assertions to validate the equality and hash code behavior of `JsonObject` instances.
- **Functions called**:
    - [`com.google.gson.JsonPrimitiveTest.testEquals`](JsonPrimitiveTest.java.driver.md#JsonPrimitiveTesttestEquals)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.equals`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectequals)
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testEqualsHashCodeIgnoringOrder<!-- {{#callable:com.google.gson.JsonObjectTest.testEqualsHashCodeIgnoringOrder}} -->
The method `testEqualsHashCodeIgnoringOrder` tests the equality and hash code of two `JsonObject` instances, ensuring they are considered equal despite having properties added in different orders.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create two `JsonObject` instances, `a` and `b`.
    - Add properties to `a` and `b` such that they have the same keys and values but in different orders.
    - Convert the key sets of `a` and `b` to `ArrayList` and assert their contents and order.
    - Use `MoreAsserts.assertEqualsAndHashCode` to assert that `a` and `b` are equal and have the same hash code.
- **Output**:
    - The method does not return any value; it performs assertions to validate the behavior of the `JsonObject` class.
- **Functions called**:
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.JsonObject.keySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectkeySet)
    - [`com.google.gson.common.MoreAsserts.assertEqualsAndHashCode`](common/MoreAsserts.java.driver.md#MoreAssertsassertEqualsAndHashCode)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testSize<!-- {{#callable:com.google.gson.JsonObjectTest.testSize}} -->
The `testSize` method verifies the size functionality of a `JsonObject` by adding and removing elements and asserting the expected size at each step.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonObject` instance `o` is created.
    - The size of `o` is asserted to be 0 using `assertThat(o.size()).isEqualTo(0);`.
    - A new key-value pair ('Hello', 1) is added to `o`, and the size is asserted to be 1.
    - Another key-value pair ('Hi', 1) is added to `o`, and the size is asserted to be 2.
    - The key 'Hello' is removed from `o`, and the size is asserted to be 1.
- **Output**:
    - The method does not return any value; it uses assertions to validate the size of the `JsonObject` at various stages.
- **Functions called**:
    - [`com.google.gson.JsonObject.size`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectsize)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.remove`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectremove)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testIsEmpty<!-- {{#callable:com.google.gson.JsonObjectTest.testIsEmpty}} -->
The `testIsEmpty` method verifies the behavior of the [`isEmpty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectisEmpty) method of a `JsonObject` by asserting its state before and after adding and removing an element.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new `JsonObject` instance `o`.
    - Assert that `o.isEmpty()` returns `true` when the object is newly created and contains no elements.
    - Add a key-value pair ('Hello', 1) to the `JsonObject` using `o.add()`.
    - Assert that `o.isEmpty()` returns `false` after adding an element.
    - Remove the key 'Hello' from the `JsonObject` using `o.remove()`.
    - Assert that `o.isEmpty()` returns `true` after removing the element.
- **Output**:
    - The method does not return any value; it uses assertions to validate the behavior of the [`isEmpty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectisEmpty) method.
- **Functions called**:
    - [`com.google.gson.JsonObject.isEmpty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectisEmpty)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.remove`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectremove)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testDeepCopy<!-- {{#callable:com.google.gson.JsonObjectTest.testDeepCopy}} -->
The `testDeepCopy` method verifies that a deep copy of a `JsonObject` does not reflect changes made to the original object after the copy is made.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a new `JsonObject` named `original`.
    - Create a new `JsonArray` named `firstEntry` and add it to `original` with the key "key".
    - Create a deep copy of `original` and store it in `copy`.
    - Add a new `JsonPrimitive` with the value "z" to `firstEntry`.
    - Assert that the size of the `JsonArray` retrieved from `original` using the key "key" is 1.
    - Assert that the size of the `JsonArray` retrieved from `copy` using the key "key" is 0.
- **Output**:
    - The method does not return any value; it uses assertions to verify the behavior of the [`deepCopy`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementdeepCopy) method.
- **Functions called**:
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonElement.deepCopy`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementdeepCopy)
    - [`com.google.gson.JsonObject.get`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsJsonArray`](../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonArray)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testKeySet<!-- {{#callable:com.google.gson.JsonObjectTest.testKeySet}} -->
The `testKeySet` method verifies the behavior of the [`keySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectkeySet) method in the `JsonObject` class, ensuring it maintains insertion order and allows for key removal.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a new `JsonObject` instance `a` and assert its key set size is 0.
    - Add a `JsonArray` with key 'foo' and a `JsonObject` with key 'bar' to `a`.
    - Assert the size of `a` is 2 and its key set contains 'foo' and 'bar' in order.
    - Add boolean properties with keys '1' and '2' to `a`.
    - Create a `Deque` `expectedKeys` with the keys 'foo', 'bar', '1', '2' and assert the key set of `a` matches this order.
    - Iterate over the key set of `a`, removing each key and asserting the size and order of the remaining keys match `expectedKeys`.
- **Output**:
    - The method does not return a value; it uses assertions to validate the behavior of the [`keySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectkeySet) method.
- **Functions called**:
    - [`com.google.gson.JsonObject.keySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectkeySet)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.size`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectsize)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.iterator`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayiterator)
    - [`com.google.gson.JsonStreamParser.hasNext`](../../../../../main/java/com/google/gson/JsonStreamParser.java.driver.md#JsonStreamParserhasNext)
    - [`com.google.gson.JsonStreamParser.next`](../../../../../main/java/com/google/gson/JsonStreamParser.java.driver.md#JsonStreamParsernext)
    - [`com.google.gson.JsonObject.remove`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectremove)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testEntrySet<!-- {{#callable:com.google.gson.JsonObjectTest.testEntrySet}} -->
The `testEntrySet` method tests the behavior of the [`entrySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectentrySet) method of a `JsonObject`, including insertion order, value setting, and entry removal.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `JsonObject` and assert its entry set is empty.
    - Add a property to the `JsonObject` and assert the entry set contains the expected entry and has size 1.
    - Add another property and assert the entry set maintains insertion order with the expected entries list.
    - Iterate over the entry set, setting new values for each entry and asserting the values are updated correctly.
    - Attempt to set a null value for an entry, expecting a `NullPointerException`, and assert the entry's value remains non-null.
    - Add additional properties to the `JsonObject` and assert the entry set contains all entries in the expected order.
    - Iterate over the entry set, removing entries one by one, and assert the size and content of the entry set decrease accordingly.
- **Output**:
    - The method does not return a value; it uses assertions to validate the behavior of the [`entrySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectentrySet) method.
- **Functions called**:
    - [`com.google.gson.JsonObject.entrySet`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectentrySet)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
    - [`com.google.gson.JsonArray.asList`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayasList)
    - [`com.google.gson.JsonArray.iterator`](../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArrayiterator)
    - [`com.google.gson.JsonObject.size`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectsize)
    - [`com.google.gson.JsonStreamParser.next`](../../../../../main/java/com/google/gson/JsonStreamParser.java.driver.md#JsonStreamParsernext)
    - [`com.google.gson.ParameterizedTypeFixtures.MyParameterizedType.getValue`](ParameterizedTypeFixtures.java.driver.md#MyParameterizedTypegetValue)
    - [`com.google.gson.JsonStreamParser.hasNext`](../../../../../main/java/com/google/gson/JsonStreamParser.java.driver.md#JsonStreamParserhasNext)
    - [`com.google.gson.JsonObject.remove`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectremove)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)


---
#### JsonObjectTest\.testToString<!-- {{#callable:com.google.gson.JsonObjectTest.testToString}} -->
The `testToString` method verifies the string representation of a `JsonObject` after adding various properties and nested structures.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A new `JsonObject` is instantiated and its string representation is asserted to be an empty JSON object `{}`.
    - A property 'a' with a `JsonNull` value is added to the `JsonObject`.
    - A property 'b\0' with a `Float.NaN` value is added to the `JsonObject`.
    - A `JsonArray` containing a double quote character is created and added as property 'c' to the `JsonObject`.
    - A nested `JsonObject` with a property 'n\0' set to 1 is created and added as property 'd' to the main `JsonObject`.
    - The final string representation of the `JsonObject` is asserted to match the expected JSON string with all added properties and nested structures.
- **Output**:
    - The method does not return a value; it uses assertions to validate the expected behavior of the [`toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString) method on a `JsonObject`.
- **Functions called**:
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
    - [`com.google.gson.JsonObject.add`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.addProperty`](../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectaddProperty)
- **See also**: [`com.google.gson.JsonObjectTest`](#JsonObjectTest)  (Base Class)



