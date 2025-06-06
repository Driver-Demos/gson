# Purpose
The provided Java source code file is a functional test suite for the [`RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory) feature in the Google Gson library. This test suite is designed to verify the correct serialization and deserialization of polymorphic types using Gson's `TypeAdapterFactory` mechanism. The code defines a set of classes representing geometric shapes, specifically [`Circle`](#CircleCircle) and [`Square`](#SquareSquare), which extend a base class [`Shape`](#ShapeShape). The [`Shape`](#ShapeShape) class is annotated with `@JsonAdapter`, linking it to a custom [`JsonAdapterFactory`](#JsonAdapterFactoryJsonAdapterFactory) that extends [`RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory). This factory is responsible for managing the serialization and deserialization process by associating specific JSON type labels with their corresponding Java classes.

The [`RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory) class is a generic implementation that allows for the dynamic registration of subtypes and their corresponding labels, facilitating the polymorphic handling of JSON data. It provides methods to register subtypes and create type adapters that handle the conversion between JSON and Java objects. The test method [`testSubclassesAutomaticallySerialized`](#RuntimeTypeAdapterFactoryFunctionalTesttestSubclassesAutomaticallySerialized) demonstrates the functionality by serializing and deserializing instances of [`Circle`](#CircleCircle) and [`Square`](#SquareSquare), ensuring that the correct subtype is instantiated based on the JSON data. This file serves as a comprehensive test to ensure that the [`RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory) correctly handles the serialization and deserialization of polymorphic types, maintaining the integrity of the type information throughout the process.
# Imports and Dependencies

---
- `com.google.gson.functional`
- `com.google.common.truth.Truth.assertThat`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.Gson`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.annotations.JsonAdapter`
- `com.google.gson.internal.Streams`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.util.LinkedHashMap`
- `java.util.Map`
- `org.junit.Test`


# Classes

---
### RuntimeTypeAdapterFactoryFunctionalTest<!-- {{#class:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `RuntimeTypeAdapterFactoryFunctionalTest` class is a functional test suite designed to validate the functionality of the `RuntimeTypeAdapterFactory` feature in Gson, specifically testing the serialization and deserialization of polymorphic types using custom type adapters. It includes a test method that verifies the automatic serialization and deserialization of subclass instances (`Circle` and `Square`) of a base class (`Shape`) using a `JsonAdapterFactory` registered with Gson. The class ensures that the `TypeAdapterFactory` registered through `JsonAdapter` annotations works correctly with Gson's delegate adapter mechanism.
- **Fields**:
    - `gson`: `Gson` An instance of Gson used for JSON serialization and deserialization in the test.
- **Methods**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.testSubclassesAutomaticallySerialized`](#RuntimeTypeAdapterFactoryFunctionalTesttestSubclassesAutomaticallySerialized)

**Methods**

---
#### RuntimeTypeAdapterFactoryFunctionalTest\.testSubclassesAutomaticallySerialized<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.testSubclassesAutomaticallySerialized}} -->
The method tests the automatic serialization and deserialization of subclass instances using Gson and a custom TypeAdapterFactory.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - A Circle object with a radius of 25 is created and serialized to JSON using Gson.
    - The JSON is deserialized back into a Shape object, and it is asserted that the radius of the Circle is still 25.
    - A Square object with a side length of 15 is created and serialized to JSON using Gson.
    - The JSON is deserialized back into a Shape object, and it is asserted that the side length of the Square is still 15.
    - It is also asserted that the type of the deserialized Shape is ShapeType.SQUARE.
- **Output**:
    - The method does not return any value but performs assertions to verify the correctness of serialization and deserialization.
- **Functions called**:
    - [`com.google.gson.Gson.toJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsontoJson)
    - [`com.google.gson.Gson.fromJson`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsonfromJson)
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest`](#RuntimeTypeAdapterFactoryFunctionalTest)  (Base Class)



---
### Shape<!-- {{#class:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape}} -->
- **Modifiers**: `static`
- **Description**: The `Shape` class is a base class for different types of shapes, such as `Circle` and `Square`, and is designed to be used with Gson for JSON serialization and deserialization. It uses a custom `JsonAdapterFactory` to handle the polymorphic nature of its subclasses, allowing instances of `Shape` to be serialized and deserialized based on their specific type, which is determined by the `ShapeType` enum.
- **Fields**:
    - `type`: `ShapeType` A final field that holds the type of the shape, represented by the `ShapeType` enum.
- **Methods**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape.Shape`](#ShapeShape)

**Methods**

---
#### Shape\.Shape<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape.Shape}} -->
The `Shape` constructor initializes a `Shape` object with a specified `ShapeType`.
- **Inputs**:
    - `type`: A `ShapeType` enum value that specifies the type of the shape being created.
- **Control Flow**:
    - Assigns the provided `ShapeType` argument to the `type` field of the `Shape` object.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape`](#RuntimeTypeAdapterFactoryFunctionalTest.Shape)  (Base Class)



---
### JsonAdapterFactory<!-- {{#class:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape.JsonAdapterFactory}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `JsonAdapterFactory` class is a specialized extension of the `RuntimeTypeAdapterFactory` designed to handle JSON serialization and deserialization for the `Shape` class and its subtypes, `Circle` and `Square`. It registers these subtypes with specific labels, allowing the Gson library to correctly serialize and deserialize JSON objects based on the `type` field, which distinguishes between different shape types.
- **Methods**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape.JsonAdapterFactory.JsonAdapterFactory`](#JsonAdapterFactoryJsonAdapterFactory)

**Methods**

---
#### JsonAdapterFactory\.JsonAdapterFactory<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape.JsonAdapterFactory.JsonAdapterFactory}} -->
The `JsonAdapterFactory` constructor initializes a `RuntimeTypeAdapterFactory` for `Shape` with a type field and registers subtypes `Circle` and `Square` with their respective labels.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor calls the superclass `RuntimeTypeAdapterFactory` with `Shape.class` and the string "type" to specify the base type and the type field name.
    - It registers the `Circle` class as a subtype with the label `ShapeType.CIRCLE.toString()`.
    - It registers the `Square` class as a subtype with the label `ShapeType.SQUARE.toString()`.
- **Output**:
    - This constructor does not return any value as it is a constructor for initializing an object of `JsonAdapterFactory`.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype)
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape.JsonAdapterFactory`](#RuntimeTypeAdapterFactoryFunctionalTest.Shape.JsonAdapterFactory)  (Base Class)



---
### ShapeType<!-- {{#class:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.ShapeType}} -->
- **Modifiers**: `public`
- **Description**: The `ShapeType` enum defines a set of constants representing different types of shapes, specifically `SQUARE` and `CIRCLE`, which are used to categorize and manage shape objects within the application.


---
### Circle<!-- {{#class:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Circle}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Circle` class is a specialized subclass of `Shape` that represents a circle with a specific radius, and it is used within the context of JSON serialization and deserialization in the `RuntimeTypeAdapterFactoryFunctionalTest` class.
- **Fields**:
    - `radius`: `int` The radius of the circle, which is a final integer value.
- **Methods**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Circle.Circle`](#CircleCircle)
- **Extends/Implements**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape`](#RuntimeTypeAdapterFactoryFunctionalTest.Shape)

**Methods**

---
#### Circle\.Circle<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Circle.Circle}} -->
The `Circle` constructor initializes a new `Circle` object with a specified radius and sets its shape type to `CIRCLE`.
- **Modifiers**: ``
- **Inputs**:
    - `radius`: An integer representing the radius of the circle.
- **Control Flow**:
    - The constructor calls the superclass constructor with `ShapeType.CIRCLE` to set the shape type.
    - The `radius` parameter is assigned to the `radius` field of the `Circle` object.
- **Output**:
    - The method does not return a value as it is a constructor.
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Circle`](#RuntimeTypeAdapterFactoryFunctionalTest.Circle)  (Base Class)



---
### Square<!-- {{#class:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Square}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `Square` class is a specialized subclass of `Shape` that represents a square with a specific side length, and it is used within the context of JSON serialization and deserialization in the Gson library.
- **Fields**:
    - `side`: `int` Represents the length of a side of the square.
- **Methods**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Square.Square`](#SquareSquare)
- **Extends/Implements**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Shape`](#RuntimeTypeAdapterFactoryFunctionalTest.Shape)

**Methods**

---
#### Square\.Square<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Square.Square}} -->
The `Square` constructor initializes a new instance of the `Square` class with a specified side length and sets its type to `SQUARE`.
- **Modifiers**: ``
- **Inputs**:
    - `side`: An integer representing the length of the side of the square.
- **Control Flow**:
    - The constructor calls the superclass constructor with `ShapeType.SQUARE` to set the type of the shape.
    - The `side` field of the `Square` instance is set to the provided `side` argument.
- **Output**:
    - The method does not return a value as it is a constructor.
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.Square`](#RuntimeTypeAdapterFactoryFunctionalTest.Square)  (Base Class)



---
### RuntimeTypeAdapterFactory<!-- {{#class:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory}} -->
- **Modifiers**: `static`
- **Description**: The `RuntimeTypeAdapterFactory` class is a custom implementation of the `TypeAdapterFactory` interface that facilitates the serialization and deserialization of polymorphic types in Gson. It allows for the registration of subtypes with unique labels, enabling the Gson library to correctly handle JSON data that represents different subtypes of a base class. The class maintains mappings between labels and subtypes, and uses these mappings to delegate serialization and deserialization tasks to the appropriate `TypeAdapter` instances. This class is particularly useful for scenarios where JSON data includes a type field that indicates the specific subtype of a base class.
- **Fields**:
    - `baseType`: `Class<?>` The base class type for which this factory is creating type adapters.
    - `typeFieldName`: `String` The name of the field in the JSON that indicates the type of the object.
    - `labelToSubtype`: `Map<String, Class<?>>` A map that associates string labels with their corresponding subtype classes.
    - `subtypeToLabel`: `Map<Class<?>, String>` A map that associates subtype classes with their corresponding string labels.
- **Methods**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.of`](#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.of`](#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create`](#RuntimeTypeAdapterFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### RuntimeTypeAdapterFactory\.RuntimeTypeAdapterFactory<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.RuntimeTypeAdapterFactory}} -->
The `RuntimeTypeAdapterFactory` constructor initializes a new instance with a specified base type and type field name, ensuring neither is null.
- **Modifiers**: `protected`
- **Inputs**:
    - `baseType`: The base class type for which the runtime type adapter factory is being created.
    - `typeFieldName`: The name of the field that will hold the type information in JSON serialization and deserialization.
- **Control Flow**:
    - Check if `typeFieldName` or `baseType` is null.
    - If either is null, throw a `NullPointerException`.
    - Assign the `baseType` to the instance variable `this.baseType`.
    - Assign the `typeFieldName` to the instance variable `this.typeFieldName`.
- **Output**:
    - This constructor does not return a value; it initializes the instance variables of the `RuntimeTypeAdapterFactory` object.
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.of<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.of}} -->
The `of` method creates a new instance of `RuntimeTypeAdapterFactory` for a given base type and type field name.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `baseType`: The class type for which the runtime type adapter factory is being created.
    - `typeFieldName`: The name of the field that will be used to determine the type of the object during serialization and deserialization.
- **Control Flow**:
    - The method takes two parameters: `baseType` and `typeFieldName`.
    - It returns a new instance of `RuntimeTypeAdapterFactory` initialized with the provided `baseType` and `typeFieldName`.
- **Output**:
    - A new instance of `RuntimeTypeAdapterFactory<T>` initialized with the specified base type and type field name.
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.of<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.of}} -->
The `of` method creates a new `RuntimeTypeAdapterFactory` instance for a given base type using a default type field name "type".
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `baseType`: The class type for which the `RuntimeTypeAdapterFactory` is being created.
- **Control Flow**:
    - The method takes a single parameter `baseType` of type `Class<T>`.
    - It returns a new instance of `RuntimeTypeAdapterFactory` initialized with the provided `baseType` and a default type field name "type".
- **Output**:
    - A new instance of `RuntimeTypeAdapterFactory<T>` initialized with the specified base type and the default type field name "type".
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.registerSubtype<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.registerSubtype}} -->
The `registerSubtype` method registers a subtype with a unique label for runtime type adaptation.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: A `Class` object representing the subtype to be registered, which must extend the base type `T`.
    - `label`: A `String` representing the unique label associated with the subtype.
- **Control Flow**:
    - Check if either `type` or `label` is null, and throw a `NullPointerException` if so.
    - Check if `type` is already a key in `subtypeToLabel` or if `label` is already a key in `labelToSubtype`, and throw an `IllegalArgumentException` if either is true.
    - Add the `label` and `type` to the `labelToSubtype` map.
    - Add the `type` and `label` to the `subtypeToLabel` map.
    - Return the current instance of `RuntimeTypeAdapterFactory`.
- **Output**:
    - Returns the current instance of `RuntimeTypeAdapterFactory<T>` to allow method chaining.
- **Functions called**:
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.registerSubtype<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.registerSubtype}} -->
The [`registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype) method registers a subtype with its simple class name as the label in the `RuntimeTypeAdapterFactory`.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: A `Class` object representing the subtype to be registered, which must extend the base type `T`.
- **Control Flow**:
    - The method calls another overloaded [`registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype) method, passing the `type` and its simple name obtained via `type.getSimpleName()` as arguments.
- **Output**:
    - Returns the current instance of `RuntimeTypeAdapterFactory<T>` to allow for method chaining.
- **Functions called**:
    - [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype)
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.create<!-- {{#callable:com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory.create}} -->
The `create` method generates a `TypeAdapter` for a specified type if it matches the base type, facilitating serialization and deserialization of JSON objects with polymorphic types.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class used to obtain delegate adapters for serialization and deserialization.
    - `type`: A `TypeToken` representing the type for which a `TypeAdapter` is to be created.
- **Control Flow**:
    - Check if the raw type of the provided `TypeToken` matches the `baseType`; if not, return `null`.
    - Initialize two maps: `labelToDelegate` and `subtypeToDelegate` to store mappings from labels and subtypes to their respective `TypeAdapter` instances.
    - Iterate over the `labelToSubtype` map to populate the `labelToDelegate` and `subtypeToDelegate` maps with `TypeAdapter` instances obtained from the `Gson` instance.
    - Return a new `TypeAdapter` instance with overridden `read` and [`write`](../../../../../../main/java/com/google/gson/internal/Streams.java.driver.md#Streamswrite) methods.
    - In the `read` method, parse the JSON input to a `JsonElement`, retrieve the type label, and use it to find the appropriate `TypeAdapter` for deserialization.
    - In the [`write`](../../../../../../main/java/com/google/gson/internal/Streams.java.driver.md#Streamswrite) method, determine the class of the object to be serialized, find the corresponding type label and `TypeAdapter`, and serialize the object to JSON, ensuring the type label is included.
- **Output**:
    - A `TypeAdapter<R>` instance capable of serializing and deserializing objects of the specified type, or `null` if the type does not match the base type.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.Gson.getDelegateAdapter`](../../../../../../main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.functional.TreeTypeAdaptersTest.Id.getValue`](TreeTypeAdaptersTest.java.driver.md#IdgetValue)
    - [`com.google.gson.functional.MapTest.MapWithoutNoArgsConstructor.put`](MapTest.java.driver.md#MapWithoutNoArgsConstructorput)
    - [`com.google.gson.internal.Streams.parse`](../../../../../../main/java/com/google/gson/internal/Streams.java.driver.md#Streamsparse)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonPrimitive.getAsString`](../../../../../../main/java/com/google/gson/JsonPrimitive.java.driver.md#JsonPrimitivegetAsString)
    - [`com.google.gson.TypeAdapter.fromJsonTree`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJsonTree)
    - [`com.google.gson.TypeAdapter.toJsonTree`](../../../../../../main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJsonTree)
    - [`com.google.gson.JsonObject.has`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas)
    - [`com.google.gson.JsonObject.add`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonObject.entrySet`](../../../../../../main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectentrySet)
    - [`com.google.gson.internal.Streams.write`](../../../../../../main/java/com/google/gson/internal/Streams.java.driver.md#Streamswrite)
- **See also**: [`com.google.gson.functional.RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryFunctionalTest.RuntimeTypeAdapterFactory)  (Base Class)



