# Purpose
The `GraphAdapterBuilderTest` Java file is a comprehensive test suite designed to validate the functionality of the `GraphAdapterBuilder` class, which is part of the Google Gson library. This class is used to handle complex object graphs during serialization and deserialization processes, particularly when dealing with cyclic references or shared instances. The test cases within this file cover a variety of scenarios, including serialization and deserialization of objects with direct and indirect self-references, custom instance creation, and handling of lists of lists. The tests ensure that the `GraphAdapterBuilder` correctly manages object identity and reference consistency, which are crucial for maintaining the integrity of object graphs in JSON representations.

The file defines several test methods using the JUnit framework, each focusing on a specific aspect of the `GraphAdapterBuilder`'s functionality. Key components include the use of `GsonBuilder` to configure Gson instances with custom type adapters, and the `assertThat` method from the Google Truth library to verify expected outcomes. The test cases also demonstrate the flexibility of the `GraphAdapterBuilder` in handling multiple types and custom instance creators, as well as its ability to be reused and modified without affecting previous configurations. The file includes inner classes [`Roshambo`](#RoshamboRoshambo), [`Employee`](#EmployeeEmployee), and [`Company`](#CompanyCompany) to model the objects being serialized and deserialized, providing a clear context for the tests. Overall, this test suite ensures the robustness and reliability of the `GraphAdapterBuilder` in managing complex serialization scenarios.
# Imports and Dependencies

---
- `com.google.gson.graph`
- `com.google.common.truth.Truth.assertThat`
- `com.google.gson.Gson`
- `com.google.gson.GsonBuilder`
- `com.google.gson.reflect.TypeToken`
- `java.lang.reflect.Type`
- `java.util.ArrayList`
- `java.util.List`
- `org.junit.Test`


# Classes

---
### GraphAdapterBuilderTest<!-- {{#class:com.google.gson.graph.GraphAdapterBuilderTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `GraphAdapterBuilderTest` class is a comprehensive test suite designed to validate the functionality of the `GraphAdapterBuilder` in serializing and deserializing complex object graphs using Gson. It includes various test cases that cover scenarios such as serialization and deserialization of cyclic references, custom instance creators, overwriting type creators, handling lists of lists, and ensuring the integrity of object references across multiple types. The tests ensure that the `GraphAdapterBuilder` can correctly handle complex data structures and maintain object identity and relationships during JSON serialization and deserialization.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testSerialization`](#GraphAdapterBuilderTesttestSerialization)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testDeserialization`](#GraphAdapterBuilderTesttestDeserialization)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testDeserializationDirectSelfReference`](#GraphAdapterBuilderTesttestDeserializationDirectSelfReference)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testAddTypeCustomInstanceCreator`](#GraphAdapterBuilderTesttestAddTypeCustomInstanceCreator)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testAddTypeOverwrite`](#GraphAdapterBuilderTesttestAddTypeOverwrite)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testSerializeListOfLists`](#GraphAdapterBuilderTesttestSerializeListOfLists)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testDeserializeListOfLists`](#GraphAdapterBuilderTesttestDeserializeListOfLists)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testSerializationWithMultipleTypes`](#GraphAdapterBuilderTesttestSerializationWithMultipleTypes)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testDeserializationWithMultipleTypes`](#GraphAdapterBuilderTesttestDeserializationWithMultipleTypes)
    - [`com.google.gson.graph.GraphAdapterBuilderTest.testBuilderReuse`](#GraphAdapterBuilderTesttestBuilderReuse)

**Methods**

---
#### GraphAdapterBuilderTest\.testSerialization<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testSerialization}} -->
The `testSerialization` method tests the serialization of a cyclic graph of `Roshambo` objects using Gson with a custom graph adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create three `Roshambo` objects named 'ROCK', 'SCISSORS', and 'PAPER'.
    - Set up a cyclic relationship where 'ROCK' beats 'SCISSORS', 'SCISSORS' beats 'PAPER', and 'PAPER' beats 'ROCK'.
    - Initialize a `GsonBuilder` and register a `GraphAdapterBuilder` for the `Roshambo` class on it.
    - Create a `Gson` instance from the `GsonBuilder`.
    - Serialize the 'ROCK' object to JSON using the `Gson` instance, replacing double quotes with single quotes in the resulting JSON string.
    - Assert that the serialized JSON string matches the expected cyclic graph representation.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testDeserialization<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testDeserialization}} -->
The `testDeserialization` method tests the deserialization of a JSON string into a `Roshambo` object graph using Gson with a custom adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing a graph of `Roshambo` objects is defined.
    - A `GsonBuilder` is instantiated and a `GraphAdapterBuilder` is used to register the `Roshambo` type on it.
    - A `Gson` instance is created from the `GsonBuilder`.
    - The JSON string is deserialized into a `Roshambo` object named `rock`.
    - Assertions are made to verify that the `name` of `rock` is 'ROCK', the `name` of `rock.beats` is 'SCISSORS', the `name` of `rock.beats.beats` is 'PAPER', and that `rock.beats.beats.beats` is the same instance as `rock`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testDeserializationDirectSelfReference<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testDeserializationDirectSelfReference}} -->
The method `testDeserializationDirectSelfReference` tests the deserialization of a JSON object with a direct self-reference using Gson and a custom graph adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A JSON string representing an object with a direct self-reference is defined.
    - A `GsonBuilder` instance is created and a `GraphAdapterBuilder` is used to add the `Roshambo` type and register it on the `GsonBuilder`.
    - A `Gson` instance is created from the `GsonBuilder`.
    - The JSON string is deserialized into a `Roshambo` object using the `Gson` instance.
    - Assertions are made to verify that the `name` of the deserialized object is 'SUICIDE' and that the `beats` field is the same instance as the object itself, confirming the self-reference.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testAddTypeCustomInstanceCreator<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testAddTypeCustomInstanceCreator}} -->
The `testAddTypeCustomInstanceCreator` method tests the deserialization of a JSON string into a `Company` object using a custom instance creator for the `Company` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created.
    - A `GraphAdapterBuilder` is used to add a custom instance creator for the `Company` class, which creates a `Company` object with the name 'custom', and the `Employee` class is also added.
    - The `GraphAdapterBuilder` is registered on the `GsonBuilder`.
    - A `Gson` instance is created from the `GsonBuilder`.
    - A JSON string representing a `Company` with an `Employee` is deserialized into a `Company` object using the `Gson` instance.
    - Assertions are made to verify that the `Company` name is 'custom', the `Employee` name is 'Jesse', and the `Employee`'s company is the same instance as the `Company`.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testAddTypeOverwrite<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testAddTypeOverwrite}} -->
The `testAddTypeOverwrite` method tests the behavior of overwriting type creators in a `GraphAdapterBuilder` when registering custom and default instance creators for the `Company` class.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created.
    - A `GraphAdapterBuilder` is instantiated and a custom instance creator for `Company` is added, followed by another custom instance creator for `Company` that overwrites the first one, and then an `Employee` type is added.
    - The `GraphAdapterBuilder` is registered on the `GsonBuilder`, and a `Gson` instance is created from it.
    - A `Company` object is deserialized from JSON, and it is asserted that the `name` is 'custom-2', verifying the overwrite of the instance creator.
    - A new `GsonBuilder` instance is created.
    - A `GraphAdapterBuilder` is instantiated again, a custom instance creator for `Company` is added, followed by a default instance creator for `Company` that overwrites the custom one, and then an `Employee` type is added.
    - The `GraphAdapterBuilder` is registered on the new `GsonBuilder`, and a new `Gson` instance is created from it.
    - A `Company` object is deserialized from JSON, and it is asserted that the `name` is `null`, verifying the overwrite with the default instance creator.
- **Output**:
    - The method does not return any value; it performs assertions to verify the behavior of the `GraphAdapterBuilder` when overwriting type creators.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testSerializeListOfLists<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testSerializeListOfLists}} -->
The `testSerializeListOfLists` method tests the serialization of a list of lists using Gson with a custom graph adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a `Type` for a list of lists and a list of any type using `TypeToken`.
    - Create a `List<List<?>>` and add itself and an empty list to it.
    - Instantiate a `GsonBuilder` and register a `GraphAdapterBuilder` with the types defined.
    - Create a `Gson` instance from the `GsonBuilder`.
    - Serialize the `listOfLists` to JSON using the `Gson` instance and the `listOfListsType`.
    - Assert that the serialized JSON matches the expected string with single quotes.
- **Output**:
    - The method does not return a value; it performs an assertion to verify the correctness of the serialization.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../../../gson/src/main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testDeserializeListOfLists<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testDeserializeListOfLists}} -->
The `testDeserializeListOfLists` method tests the deserialization of a JSON string into a list of lists using Gson with a custom graph adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Define a `Type` for a list of any type and a list of lists using `TypeToken`.
    - Create a `GsonBuilder` instance.
    - Register the types with a new `GraphAdapterBuilder` on the `GsonBuilder`.
    - Create a `Gson` instance from the `GsonBuilder`.
    - Deserialize a JSON string representing a list of lists into a `List<List<?>>` using the `Gson` instance.
    - Assert that the deserialized list has a size of 2.
    - Assert that the first element of the list is the same instance as the list itself.
    - Assert that the second element of the list is empty.
- **Output**:
    - The method does not return any value; it performs assertions to validate the deserialization process.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getType`](../../../../../../../../gson/src/main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testSerializationWithMultipleTypes<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testSerializationWithMultipleTypes}} -->
The method `testSerializationWithMultipleTypes` tests the serialization of a `Company` object with multiple `Employee` objects into a JSON string using Gson with a custom graph adapter.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Create a `Company` object named `google` with the name 'Google'.
    - Instantiate two `Employee` objects, `unused1` and `unused2`, with names 'Jesse' and 'Joel', respectively, and associate them with the `google` company, which automatically adds them to the company's employee list.
    - Initialize a `GsonBuilder` object and register a `GraphAdapterBuilder` with types `Company` and `Employee` to handle serialization of these types.
    - Create a `Gson` object from the `GsonBuilder`.
    - Serialize the `google` company object to a JSON string using the `Gson` object, replacing double quotes with single quotes for comparison.
    - Assert that the serialized JSON string matches the expected JSON structure, which includes the company and its employees with unique identifiers.
- **Output**:
    - The method does not return any value; it performs an assertion to verify the correctness of the serialization process.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.GsonBuilder.create`](../../../../../../../../gson/src/main/java/com/google/gson/GsonBuilder.java.driver.md#GsonBuildercreate)
    - [`com.google.gson.Gson.toJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testDeserializationWithMultipleTypes<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testDeserializationWithMultipleTypes}} -->
The method `testDeserializationWithMultipleTypes` tests the deserialization of a JSON string into a `Company` object with associated `Employee` objects using Gson and verifies the integrity of the deserialized objects.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created to configure Gson settings.
    - A `GraphAdapterBuilder` is used to register `Company` and `Employee` types on the `GsonBuilder`.
    - A `Gson` instance is created from the `GsonBuilder`.
    - A JSON string representing a `Company` with two `Employee` objects is defined.
    - The JSON string is deserialized into a `Company` object using `gson.fromJson`.
    - Assertions are made to verify that the `Company` name is 'Google'.
    - The first `Employee` is retrieved from the `Company`'s employee list, and assertions verify its name is 'Jesse' and its `company` reference is the same as the `Company` object.
    - The second `Employee` is retrieved, and similar assertions verify its name is 'Joel' and its `company` reference is the same as the `Company` object.
- **Output**:
    - The method does not return any value; it performs assertions to verify the correctness of the deserialization process.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.graph.GraphAdapterBuilder.Factory.create`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#Factorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../../../gson/src/main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)


---
#### GraphAdapterBuilderTest\.testBuilderReuse<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.testBuilderReuse}} -->
The `testBuilderReuse` method tests the reuse of a `GraphAdapterBuilder` to register different type adapters on multiple `GsonBuilder` instances and verifies that changes to one builder do not affect previously created `Gson` instances.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A `GsonBuilder` instance is created and a `GraphAdapterBuilder` is initialized with custom type adapters for `Company` and `Employee` classes.
    - The `GraphAdapterBuilder` is registered on the first `GsonBuilder`, and a `Gson` instance is created from it.
    - A `Company` object is deserialized from JSON using the first `Gson` instance, and its name is asserted to be 'custom'.
    - A second `GsonBuilder` is created, and the `GraphAdapterBuilder` is reused to add a new type adapter for `Company` with a different name 'custom-2'.
    - The `GraphAdapterBuilder` is registered on the second `GsonBuilder`, and a second `Gson` instance is created.
    - A `Company` object is deserialized from JSON using the second `Gson` instance, and its name is asserted to be 'custom-2'.
    - The first `Gson` instance is used again to deserialize a `Company` object, and its name is asserted to remain 'custom', confirming that the first adapter was not affected by changes to the builder.
- **Output**:
    - The method does not return any value but uses assertions to verify that the `GraphAdapterBuilder` can be reused without affecting previously registered adapters.
- **Functions called**:
    - [`com.google.gson.graph.GraphAdapterBuilder.addType`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderaddType)
    - [`com.google.gson.graph.GraphAdapterBuilder.registerOn`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#GraphAdapterBuilderregisterOn)
    - [`com.google.gson.graph.GraphAdapterBuilder.Factory.create`](../../../../../../main/java/com/google/gson/graph/GraphAdapterBuilder.java.driver.md#Factorycreate)
    - [`com.google.gson.Gson.fromJson`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest`](#GraphAdapterBuilderTest)  (Base Class)



---
### Roshambo<!-- {{#class:com.google.gson.graph.GraphAdapterBuilderTest.Roshambo}} -->
- **Modifiers**: `static`
- **Description**: The `Roshambo` class represents an entity in the game of Rock-Paper-Scissors, where each instance has a name and a reference to another `Roshambo` instance that it can beat, allowing for the representation of the game's cyclical nature.
- **Fields**:
    - `name`: `String` A string representing the name of the Roshambo instance, such as 'ROCK', 'PAPER', or 'SCISSORS'.
    - `beats`: `Roshambo` A reference to another Roshambo instance that this instance can beat, establishing the game's rules.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilderTest.Roshambo.Roshambo`](#RoshamboRoshambo)

**Methods**

---
#### Roshambo\.Roshambo<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.Roshambo.Roshambo}} -->
The `Roshambo` constructor initializes a new instance of the `Roshambo` class with a specified name.
- **Inputs**:
    - `name`: A `String` representing the name to be assigned to the `Roshambo` instance.
- **Control Flow**:
    - The constructor takes a single parameter `name`.
    - It assigns the value of `name` to the instance variable `this.name`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an object of the `Roshambo` class.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest.Roshambo`](#GraphAdapterBuilderTest.Roshambo)  (Base Class)



---
### Employee<!-- {{#class:com.google.gson.graph.GraphAdapterBuilderTest.Employee}} -->
- **Modifiers**: `static`
- **Description**: The `Employee` class represents an employee with a name and an associated company, and upon instantiation, it automatically adds itself to the company's list of employees.
- **Fields**:
    - `name`: `String` A final string representing the name of the employee.
    - `company`: `Company` A final reference to the Company object that the employee is associated with.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilderTest.Employee.Employee`](#EmployeeEmployee)

**Methods**

---
#### Employee\.Employee<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.Employee.Employee}} -->
The `Employee` constructor initializes an `Employee` object with a name and company, and adds the employee to the company's list of employees.
- **Inputs**:
    - `name`: A `String` representing the name of the employee.
    - `company`: A `Company` object representing the company to which the employee belongs.
- **Control Flow**:
    - Assigns the provided `name` to the `name` field of the `Employee` object.
    - Assigns the provided `company` to the `company` field of the `Employee` object.
    - Adds the current `Employee` object (`this`) to the `employees` list of the provided `Company` object.
- **Output**:
    - This constructor does not return a value as it is used to initialize an `Employee` object.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest.Employee`](#GraphAdapterBuilderTest.Employee)  (Base Class)



---
### Company<!-- {{#class:com.google.gson.graph.GraphAdapterBuilderTest.Company}} -->
- **Modifiers**: `static`
- **Description**: The `Company` class represents a company entity with a name and a list of employees associated with it. It provides a constructor to initialize the company with a specific name and maintains a list of `Employee` objects that are part of the company.
- **Fields**:
    - `name`: `String` A final string representing the name of the company.
    - `employees`: `List<Employee>` A list of employees that belong to the company, initialized as an empty ArrayList.
- **Methods**:
    - [`com.google.gson.graph.GraphAdapterBuilderTest.Company.Company`](#CompanyCompany)

**Methods**

---
#### Company\.Company<!-- {{#callable:com.google.gson.graph.GraphAdapterBuilderTest.Company.Company}} -->
The `Company` constructor initializes a new `Company` object with a specified name.
- **Inputs**:
    - `name`: A `String` representing the name of the company to be assigned to the `Company` object.
- **Control Flow**:
    - Assigns the provided `name` parameter to the `name` field of the `Company` object.
- **Output**:
    - A new instance of the `Company` class with its `name` field set to the provided `name` argument.
- **See also**: [`com.google.gson.graph.GraphAdapterBuilderTest.Company`](#GraphAdapterBuilderTest.Company)  (Base Class)



