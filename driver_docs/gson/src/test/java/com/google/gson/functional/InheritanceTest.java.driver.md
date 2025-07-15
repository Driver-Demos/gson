# Purpose
The provided Java source code file is a set of functional tests designed to verify the serialization and deserialization capabilities of the Gson library, particularly focusing on classes with inheritance hierarchies. The tests are organized within the `InheritanceTest` class, which utilizes the JUnit framework to define and execute various test cases. The primary objective of these tests is to ensure that Gson correctly handles JSON serialization and deserialization for objects that involve subclassing and polymorphism. This includes verifying that subclasses are serialized and deserialized accurately, both when treated as their specific subclass type and when treated as their base class type.

The code includes several test methods that cover different scenarios, such as serializing and deserializing subclasses, handling fields that are collections of base class types, and ensuring that explicit type specifications during serialization yield the expected JSON structure. The tests make use of various helper classes, such as [`SubTypeOfNested`](#SubTypeOfNestedSubTypeOfNested) and [`ClassWithSubInterfacesOfCollection`](#ClassWithSubInterfacesOfCollectionClassWithSubInterfacesOfCollection), to create complex object structures that mimic real-world use cases. The use of assertions from the `Truth` library ensures that the serialized JSON matches expected values, providing a robust validation mechanism for the Gson library's functionality in handling inheritance.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.Gson`
- `com.google.gson.JsonArray`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonObject`
- `com.google.gson.common.TestTypes.BagOfPrimitives`
- `com.google.gson.common.TestTypes.Base`
- `com.google.gson.common.TestTypes.ClassWithBaseArrayField`
- `com.google.gson.common.TestTypes.ClassWithBaseCollectionField`
- `com.google.gson.common.TestTypes.ClassWithBaseField`
- `com.google.gson.common.TestTypes.Nested`
- `com.google.gson.common.TestTypes.Sub`
- `java.util.ArrayList`
- `java.util.Collection`
- `java.util.LinkedList`
- `java.util.List`
- `java.util.Queue`
- `java.util.Set`
- `java.util.SortedSet`
- `java.util.TreeSet`
- `org.junit.Before`
- `org.junit.Test`


# Classes

---
### InheritanceTest<!-- {{#class:com.google.gson.functional.InheritanceTest}} -->
- **Modifiers**: `public`
- **Description**: The `InheritanceTest` class is a JUnit test class designed to perform functional tests on JSON serialization and deserialization of classes with inheritance hierarchies using the Gson library. It includes various test methods to verify the correct serialization and deserialization of subclasses, classes with base fields, and collections of base types. The class also tests the behavior of Gson when dealing with explicit type specifications during serialization. The tests ensure that the JSON output matches expected values and that the deserialization process correctly reconstructs the object hierarchy.
- **Fields**:
    - `gson`: `Gson` An instance of the Gson class used for JSON serialization and deserialization.
- **Methods**:
    - [`com.google.gson.functional.InheritanceTest.setUp`](#InheritanceTestsetUp)
    - [`com.google.gson.functional.InheritanceTest.testSubClassSerialization`](#InheritanceTesttestSubClassSerialization)
    - [`com.google.gson.functional.InheritanceTest.testSubClassDeserialization`](#InheritanceTesttestSubClassDeserialization)
    - [`com.google.gson.functional.InheritanceTest.testClassWithBaseFieldSerialization`](#InheritanceTesttestClassWithBaseFieldSerialization)
    - [`com.google.gson.functional.InheritanceTest.testClassWithBaseArrayFieldSerialization`](#InheritanceTesttestClassWithBaseArrayFieldSerialization)
    - [`com.google.gson.functional.InheritanceTest.testClassWithBaseCollectionFieldSerialization`](#InheritanceTesttestClassWithBaseCollectionFieldSerialization)
    - [`com.google.gson.functional.InheritanceTest.testBaseSerializedAsSub`](#InheritanceTesttestBaseSerializedAsSub)
    - [`com.google.gson.functional.InheritanceTest.testBaseSerializedAsSubForToJsonMethod`](#InheritanceTesttestBaseSerializedAsSubForToJsonMethod)
    - [`com.google.gson.functional.InheritanceTest.testBaseSerializedAsBaseWhenSpecifiedWithExplicitType`](#InheritanceTesttestBaseSerializedAsBaseWhenSpecifiedWithExplicitType)
    - [`com.google.gson.functional.InheritanceTest.testBaseSerializedAsBaseWhenSpecifiedWithExplicitTypeForToJsonMethod`](#InheritanceTesttestBaseSerializedAsBaseWhenSpecifiedWithExplicitTypeForToJsonMethod)
    - [`com.google.gson.functional.InheritanceTest.testBaseSerializedAsSubWhenSpecifiedWithExplicitType`](#InheritanceTesttestBaseSerializedAsSubWhenSpecifiedWithExplicitType)
    - [`com.google.gson.functional.InheritanceTest.testBaseSerializedAsSubWhenSpecifiedWithExplicitTypeForToJsonMethod`](#InheritanceTesttestBaseSerializedAsSubWhenSpecifiedWithExplicitTypeForToJsonMethod)
    - [`com.google.gson.functional.InheritanceTest.testSubInterfacesOfCollectionSerialization`](#InheritanceTesttestSubInterfacesOfCollectionSerialization)
    - [`com.google.gson.functional.InheritanceTest.testSubInterfacesOfCollectionDeserialization`](#InheritanceTesttestSubInterfacesOfCollectionDeserialization)

**Methods**

---
#### InheritanceTest\.setUp<!-- {{#callable:com.google.gson.functional.InheritanceTest.setUp}} -->
The setUp method initializes a Gson instance before each test is executed.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method is annotated with @Before, indicating it runs before each test method in the class.
    - A new instance of Gson is created and assigned to the gson field.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testSubClassSerialization<!-- {{#callable:com.google.gson.functional.InheritanceTest.testSubClassSerialization}} -->
The `testSubClassSerialization` method tests the serialization of a `SubTypeOfNested` object to JSON and verifies it against the expected JSON string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `SubTypeOfNested` object named `target` is instantiated with two `BagOfPrimitives` objects as its parameters.
    - The `gson.toJson(target)` method is called to serialize the `target` object into a JSON string.
    - The serialized JSON string is compared to the expected JSON string obtained from `target.getExpectedJson()` using an assertion.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testSubClassDeserialization<!-- {{#callable:com.google.gson.functional.InheritanceTest.testSubClassDeserialization}} -->
The `testSubClassDeserialization` method tests the deserialization of a JSON string into a `SubTypeOfNested` object and verifies that the resulting object's JSON representation matches the original JSON string.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a `SubTypeOfNested` object is defined.
    - The `gson.fromJson` method is used to deserialize the JSON string into a `SubTypeOfNested` object.
    - The `assertThat` method from the Truth library is used to assert that the JSON representation of the deserialized object matches the original JSON string.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testClassWithBaseFieldSerialization<!-- {{#callable:com.google.gson.functional.InheritanceTest.testClassWithBaseFieldSerialization}} -->
The method `testClassWithBaseFieldSerialization` tests the serialization of a `ClassWithBaseField` object to JSON and verifies that a specific field in the serialized JSON matches an expected value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `ClassWithBaseField` object is instantiated with a `Sub` object as its base field.
    - The `gson.toJsonTree` method is used to serialize the `ClassWithBaseField` object into a `JsonObject`.
    - The method retrieves the JSON element corresponding to the base field using `ClassWithBaseField.FIELD_KEY`.
    - It then asserts that the value of the `Sub.SUB_FIELD_KEY` in the base field's JSON object is equal to `Sub.SUB_NAME`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the serialization process.
- **Functions called**:
    - [`com.google.gson.Gson.toJsonTree`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJsonTree)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testClassWithBaseArrayFieldSerialization<!-- {{#callable:com.google.gson.functional.InheritanceTest.testClassWithBaseArrayFieldSerialization}} -->
The method `testClassWithBaseArrayFieldSerialization` tests the serialization of a class containing an array of base class objects into JSON and verifies the serialized content.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - An array of `Base` objects is created, containing two instances of `Sub`.
    - A `ClassWithBaseArrayField` object is instantiated using the `Base` array.
    - The object is serialized into a `JsonObject` using Gson's [`toJsonTree`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJsonTree) method.
    - The JSON object is accessed to retrieve the array field using the key `ClassWithBaseArrayField.FIELD_KEY`.
    - Each element in the JSON array is checked to ensure it contains the expected field `Sub.SUB_FIELD_KEY` with the value `Sub.SUB_NAME`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the serialized JSON content.
- **Functions called**:
    - [`com.google.gson.Gson.toJsonTree`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJsonTree)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonObject.getAsJsonArray`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectgetAsJsonArray)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testClassWithBaseCollectionFieldSerialization<!-- {{#callable:com.google.gson.functional.InheritanceTest.testClassWithBaseCollectionFieldSerialization}} -->
The method tests the serialization of a class with a collection of base class objects into JSON and verifies the serialized output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a collection of Base objects using an ArrayList and add two Sub objects to it.
    - Instantiate a ClassWithBaseCollectionField object using the collection of Base objects.
    - Serialize the ClassWithBaseCollectionField object to a JsonObject using Gson's toJsonTree method.
    - Retrieve the JsonArray from the JsonObject using the FIELD_KEY from ClassWithBaseArrayField.
    - Iterate over each JsonElement in the JsonArray and assert that the value of the SUB_FIELD_KEY in each element's JsonObject is equal to SUB_NAME.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.Gson.toJsonTree`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJsonTree)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsJsonArray`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonArray)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testBaseSerializedAsSub<!-- {{#callable:com.google.gson.functional.InheritanceTest.testBaseSerializedAsSub}} -->
The `testBaseSerializedAsSub` method tests the serialization of a `Base` object instantiated as a `Sub` object and verifies that the serialized JSON contains the expected `Sub` class field.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Base` object is instantiated as a `Sub` object.
    - The `gson.toJsonTree` method is used to serialize the `Base` object into a `JsonObject`.
    - The method asserts that the JSON object contains the `Sub` class specific field with the expected value using `assertThat`.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJsonTree`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJsonTree)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testBaseSerializedAsSubForToJsonMethod<!-- {{#callable:com.google.gson.functional.InheritanceTest.testBaseSerializedAsSubForToJsonMethod}} -->
This method tests if a 'Base' object, when serialized using Gson's toJson method, contains the expected 'Sub' class name.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A 'Base' object is instantiated as a 'Sub' object.
    - The 'base' object is serialized to a JSON string using Gson's 'toJson' method.
    - An assertion checks if the resulting JSON string contains the 'Sub.SUB_NAME'.
- **Output**:
    - The method does not return any value; it performs an assertion to validate the JSON serialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testBaseSerializedAsBaseWhenSpecifiedWithExplicitType<!-- {{#callable:com.google.gson.functional.InheritanceTest.testBaseSerializedAsBaseWhenSpecifiedWithExplicitType}} -->
This method tests the serialization of a subclass instance as a base class when explicitly specified with the base class type using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Base` object is instantiated as a `Sub` object.
    - The `gson.toJsonTree` method is called with the `base` object and `Base.class` as parameters to serialize the object as a `Base` type.
    - The resulting JSON object is checked to ensure it contains the base class field key with the expected base class name.
    - The JSON object is also checked to ensure it does not contain the subclass field key, confirming that the object is serialized as a base class.
- **Output**:
    - The method does not return any value; it performs assertions to validate the serialization behavior.
- **Functions called**:
    - [`com.google.gson.Gson.toJsonTree`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJsonTree)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testBaseSerializedAsBaseWhenSpecifiedWithExplicitTypeForToJsonMethod<!-- {{#callable:com.google.gson.functional.InheritanceTest.testBaseSerializedAsBaseWhenSpecifiedWithExplicitTypeForToJsonMethod}} -->
This method tests that a `Base` object is serialized as a `Base` type when explicitly specified in the [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method, ensuring that only `Base` fields are included in the JSON output.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Base` object is instantiated as a `Sub` object.
    - The `gson.toJson` method is called with the `Base` object and `Base.class` as parameters to serialize the object explicitly as a `Base` type.
    - The resulting JSON string is checked to ensure it contains the `Base.BASE_NAME` field.
    - The JSON string is also checked to ensure it does not contain the `Sub.SUB_FIELD_KEY` field.
- **Output**:
    - The method does not return any value; it performs assertions to validate the serialization behavior.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testBaseSerializedAsSubWhenSpecifiedWithExplicitType<!-- {{#callable:com.google.gson.functional.InheritanceTest.testBaseSerializedAsSubWhenSpecifiedWithExplicitType}} -->
This method tests the serialization of a Base object as a Sub object when an explicit type is specified using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Base object is instantiated as a Sub object.
    - The Gson library is used to serialize the Base object to a JSON tree, explicitly specifying the Sub class type.
    - The resulting JSON object is retrieved from the JSON tree.
    - An assertion checks that the JSON object contains the expected Sub class field key and value.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the serialization behavior.
- **Functions called**:
    - [`com.google.gson.Gson.toJsonTree`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJsonTree)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testBaseSerializedAsSubWhenSpecifiedWithExplicitTypeForToJsonMethod<!-- {{#callable:com.google.gson.functional.InheritanceTest.testBaseSerializedAsSubWhenSpecifiedWithExplicitTypeForToJsonMethod}} -->
This method tests if a `Base` object is serialized as a `Sub` object when an explicit type is specified in the [`toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson) method.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `Base` object is instantiated as a `Sub` object.
    - The `gson.toJson` method is called with the `Base` object and `Sub.class` as parameters to serialize the object.
    - The resulting JSON string is checked to ensure it contains the `Sub.SUB_NAME` string, indicating successful serialization as a `Sub` object.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the serialization behavior.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testSubInterfacesOfCollectionSerialization<!-- {{#callable:com.google.gson.functional.InheritanceTest.testSubInterfacesOfCollectionSerialization}} -->
The method `testSubInterfacesOfCollectionSerialization` tests the serialization of a class containing various collection sub-interfaces using Gson.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `List<Integer>` with values 0, 1, 2, and 3 using a `LinkedList` implementation.
    - Initialize a `Queue<Long>` with values 0L, 1L, 2L, and 3L using a `LinkedList` implementation.
    - Initialize a `Set<Float>` with values 0.1F, 0.2F, 0.3F, and 0.4F using a `TreeSet` implementation.
    - Initialize a `SortedSet<Character>` with values 'a', 'b', 'c', and 'd' using a `TreeSet` implementation.
    - Create an instance of `ClassWithSubInterfacesOfCollection` using the initialized collections.
    - Serialize the instance to JSON using Gson and assert that the resulting JSON matches the expected JSON representation of the instance.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correctness of the JSON serialization.
- **Functions called**:
    - [`com.google.gson.functional.CollectionTest.CollectionWithoutNoArgsConstructor.add`](CollectionTest.java.driver.md#CollectionWithoutNoArgsConstructoradd)
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](#ClassWithSubInterfacesOfCollectiongetExpectedJson)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)


---
#### InheritanceTest\.testSubInterfacesOfCollectionDeserialization<!-- {{#callable:com.google.gson.functional.InheritanceTest.testSubInterfacesOfCollectionDeserialization}} -->
This method tests the deserialization of JSON data into a Java object with various collection sub-interfaces and verifies the contents of these collections.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing collections (list, queue, set, sortedSet) is defined.
    - The JSON string is deserialized into an instance of ClassWithSubInterfacesOfCollection using Gson.
    - Assertions are made to verify that the deserialized collections contain the expected elements.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.listContains`](#ClassWithSubInterfacesOfCollectionlistContains)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.queueContains`](#ClassWithSubInterfacesOfCollectionqueueContains)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.setContains`](#ClassWithSubInterfacesOfCollectionsetContains)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.sortedSetContains`](#ClassWithSubInterfacesOfCollectionsortedSetContains)
- **See also**: [`com.google.gson.functional.InheritanceTest`](#InheritanceTest)  (Base Class)



---
### SubTypeOfNested<!-- {{#class:com.google.gson.functional.InheritanceTest.SubTypeOfNested}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `SubTypeOfNested` class is a private static subclass of `Nested` that represents a specialized type with an additional field `value`, which is a constant long set to 5. It overrides the `appendFields` method to include the `value` field in the JSON serialization process, appending it to a `StringBuilder` along with the fields from its superclass.
- **Fields**:
    - `value`: `long` A constant long field initialized to 5.
- **Methods**:
    - [`com.google.gson.functional.InheritanceTest.SubTypeOfNested.SubTypeOfNested`](#SubTypeOfNestedSubTypeOfNested)
    - [`com.google.gson.functional.InheritanceTest.SubTypeOfNested.appendFields`](#SubTypeOfNestedappendFields)
- **Extends/Implements**:
    - `Nested`

**Methods**

---
#### SubTypeOfNested\.SubTypeOfNested<!-- {{#callable:com.google.gson.functional.InheritanceTest.SubTypeOfNested.SubTypeOfNested}} -->
The `SubTypeOfNested` constructor initializes a new instance of the `SubTypeOfNested` class by calling the superclass constructor with two `BagOfPrimitives` objects.
- **Modifiers**: `public`
- **Inputs**:
    - `primitive1`: An instance of `BagOfPrimitives` representing the first set of primitive values.
    - `primitive2`: An instance of `BagOfPrimitives` representing the second set of primitive values.
- **Control Flow**:
    - The constructor is called with two parameters: `primitive1` and `primitive2`, both of type `BagOfPrimitives`.
    - The constructor invokes the superclass (`Nested`) constructor using `super(primitive1, primitive2)`, passing the two `BagOfPrimitives` instances to it.
- **Output**:
    - There is no return value as this is a constructor.
- **See also**: [`com.google.gson.functional.InheritanceTest.SubTypeOfNested`](#InheritanceTest.SubTypeOfNested)  (Base Class)


---
#### SubTypeOfNested\.appendFields<!-- {{#callable:com.google.gson.functional.InheritanceTest.SubTypeOfNested.appendFields}} -->
The `appendFields` method appends a JSON-like representation of the `value` field to a `StringBuilder` and then calls the superclass's `appendFields` method to append additional fields.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `sb`: A `StringBuilder` object to which the method appends a JSON-like representation of the object's fields.
- **Control Flow**:
    - Append the string '"value":' to the `StringBuilder` object `sb`.
    - Append the value of the `value` field to `sb`.
    - Append a comma to `sb` to separate this field from subsequent fields.
    - Call the superclass's `appendFields` method, passing `sb` to append additional fields from the superclass.
- **Output**:
    - The method does not return a value; it modifies the `StringBuilder` object passed as an argument by appending a JSON-like representation of the object's fields.
- **Functions called**:
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.append`](#ClassWithSubInterfacesOfCollectionappend)
- **See also**: [`com.google.gson.functional.InheritanceTest.SubTypeOfNested`](#InheritanceTest.SubTypeOfNested)  (Base Class)



---
### ClassWithSubInterfacesOfCollection<!-- {{#class:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `ClassWithSubInterfacesOfCollection` is a private static class designed to encapsulate collections of different types, specifically a `List` of integers, a `Queue` of longs, a `Set` of floats, and a `SortedSet` of characters. It provides methods to check if these collections contain specific values and to generate a JSON representation of the collections' contents.
- **Fields**:
    - `list`: `List<Integer>` A list of integers used to store integer values.
    - `queue`: `Queue<Long>` A queue of longs used to store long values.
    - `set`: `Set<Float>` A set of floats used to store float values.
    - `sortedSet`: `SortedSet<Character>` A sorted set of characters used to store character values in a sorted order.
- **Methods**:
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.ClassWithSubInterfacesOfCollection`](#ClassWithSubInterfacesOfCollectionClassWithSubInterfacesOfCollection)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.listContains`](#ClassWithSubInterfacesOfCollectionlistContains)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.queueContains`](#ClassWithSubInterfacesOfCollectionqueueContains)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.setContains`](#ClassWithSubInterfacesOfCollectionsetContains)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.sortedSetContains`](#ClassWithSubInterfacesOfCollectionsortedSetContains)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson`](#ClassWithSubInterfacesOfCollectiongetExpectedJson)
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.append`](#ClassWithSubInterfacesOfCollectionappend)

**Methods**

---
#### ClassWithSubInterfacesOfCollection\.ClassWithSubInterfacesOfCollection<!-- {{#callable:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.ClassWithSubInterfacesOfCollection}} -->
The constructor initializes a ClassWithSubInterfacesOfCollection object with specified List, Queue, Set, and SortedSet collections.
- **Modifiers**: `public`
- **Inputs**:
    - `list`: A List of Integer objects to be assigned to the class's list field.
    - `queue`: A Queue of Long objects to be assigned to the class's queue field.
    - `set`: A Set of Float objects to be assigned to the class's set field.
    - `sortedSet`: A SortedSet of Character objects to be assigned to the class's sortedSet field.
- **Control Flow**:
    - The constructor takes four parameters: a List of Integers, a Queue of Longs, a Set of Floats, and a SortedSet of Characters.
    - Each parameter is assigned to the corresponding private field of the ClassWithSubInterfacesOfCollection instance.
- **Output**:
    - The constructor does not return any value as it is used to initialize an instance of the class.
- **See also**: [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection`](#InheritanceTest.ClassWithSubInterfacesOfCollection)  (Base Class)


---
#### ClassWithSubInterfacesOfCollection\.listContains<!-- {{#callable:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.listContains}} -->
The `listContains` method checks if all specified integer values are present in the `list` field of the `ClassWithSubInterfacesOfCollection` class.
- **Inputs**:
    - `values`: A varargs parameter of integers to check for presence in the list.
- **Control Flow**:
    - Iterate over each integer in the `values` array.
    - For each integer, check if it is contained in the `list` field.
    - If any integer is not found in the list, return `false`.
    - If all integers are found in the list, return `true`.
- **Output**:
    - A boolean value indicating whether all specified integers are present in the list.
- **Functions called**:
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection`](#InheritanceTest.ClassWithSubInterfacesOfCollection)  (Base Class)


---
#### ClassWithSubInterfacesOfCollection\.queueContains<!-- {{#callable:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.queueContains}} -->
The `queueContains` method checks if all specified long values are present in a queue.
- **Inputs**:
    - `values`: A varargs parameter of type long, representing the values to check for presence in the queue.
- **Control Flow**:
    - Iterate over each long value in the `values` array.
    - For each value, check if it is contained in the `queue`.
    - If any value is not found in the `queue`, return `false`.
    - If all values are found in the `queue`, return `true`.
- **Output**:
    - A boolean value indicating whether all specified values are present in the queue.
- **Functions called**:
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection`](#InheritanceTest.ClassWithSubInterfacesOfCollection)  (Base Class)


---
#### ClassWithSubInterfacesOfCollection\.setContains<!-- {{#callable:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.setContains}} -->
The `setContains` method checks if all specified float values are present in a set.
- **Inputs**:
    - `values`: A varargs parameter of type float, representing the values to check for presence in the set.
- **Control Flow**:
    - Iterates over each float value in the `values` array.
    - For each value, checks if the set contains the value using the [`contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains) method.
    - If any value is not found in the set, returns `false`.
    - If all values are found in the set, returns `true`.
- **Output**:
    - A boolean value indicating whether all specified float values are present in the set.
- **Functions called**:
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection`](#InheritanceTest.ClassWithSubInterfacesOfCollection)  (Base Class)


---
#### ClassWithSubInterfacesOfCollection\.sortedSetContains<!-- {{#callable:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.sortedSetContains}} -->
The `sortedSetContains` method checks if all specified characters are present in a `SortedSet` of characters.
- **Inputs**:
    - `values`: A varargs array of characters to check for presence in the `SortedSet`.
- **Control Flow**:
    - Iterate over each character in the `values` array.
    - For each character, check if it is contained in the `sortedSet`.
    - If any character is not found in the `sortedSet`, return `false`.
    - If all characters are found, return `true`.
- **Output**:
    - A boolean value indicating whether all specified characters are present in the `SortedSet`.
- **Functions called**:
    - [`com.google.gson.JsonArray.contains`](../../../../../../main/java/com/google/gson/JsonArray.java.driver.md#JsonArraycontains)
- **See also**: [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection`](#InheritanceTest.ClassWithSubInterfacesOfCollection)  (Base Class)


---
#### ClassWithSubInterfacesOfCollection\.getExpectedJson<!-- {{#callable:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.getExpectedJson}} -->
The `getExpectedJson` method constructs and returns a JSON string representation of the collections `list`, `queue`, `set`, and `sortedSet`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize a `StringBuilder` instance `sb`.
    - Append the opening curly brace `{` to `sb`.
    - Append the key `"list":` to `sb` and call the [`append`](#ClassWithSubInterfacesOfCollectionappend) method with `sb` and `list`, then append a comma `,`.
    - Append the key `"queue":` to `sb` and call the [`append`](#ClassWithSubInterfacesOfCollectionappend) method with `sb` and `queue`, then append a comma `,`.
    - Append the key `"set":` to `sb` and call the [`append`](#ClassWithSubInterfacesOfCollectionappend) method with `sb` and `set`, then append a comma `,`.
    - Append the key `"sortedSet":` to `sb` and call the [`append`](#ClassWithSubInterfacesOfCollectionappend) method with `sb` and `sortedSet`.
    - Append the closing curly brace `}` to `sb`.
    - Convert `sb` to a string and return it.
- **Output**:
    - A JSON string representing the collections `list`, `queue`, `set`, and `sortedSet`.
- **Functions called**:
    - [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.append`](#ClassWithSubInterfacesOfCollectionappend)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection`](#InheritanceTest.ClassWithSubInterfacesOfCollection)  (Base Class)


---
#### ClassWithSubInterfacesOfCollection\.append<!-- {{#callable:com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection.append}} -->
The [`append`](ReadersWritersTest.java.driver.md#CustomAppendableappend) method formats a collection into a JSON-like string representation and appends it to a `StringBuilder`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `sb`: A `StringBuilder` object to which the formatted collection will be appended.
    - `c`: A `Collection` of objects to be formatted and appended to the `StringBuilder`.
- **Control Flow**:
    - The method starts by appending an opening bracket '[' to the `StringBuilder`.
    - A boolean variable `first` is initialized to `true` to track the first element in the collection.
    - The method iterates over each object `o` in the collection `c`.
    - For each object, if it is not the first element, a comma ',' is appended to the `StringBuilder`.
    - The `first` flag is set to `false` after processing the first element.
    - If the object `o` is an instance of `String` or `Character`, a double quote '"' is appended before and after the object's string representation.
    - The object's string representation is appended to the `StringBuilder`.
    - After iterating through all elements, a closing bracket ']' is appended to the `StringBuilder`.
- **Output**:
    - The method returns the `StringBuilder` with the appended formatted collection.
- **Functions called**:
    - [`com.google.gson.functional.ReadersWritersTest.testToJsonAppendable.CustomAppendable.append`](ReadersWritersTest.java.driver.md#CustomAppendableappend)
    - [`com.google.gson.functional.MapTest.Point.toString`](MapTest.java.driver.md#PointtoString)
- **See also**: [`com.google.gson.functional.InheritanceTest.ClassWithSubInterfacesOfCollection`](#InheritanceTest.ClassWithSubInterfacesOfCollection)  (Base Class)



