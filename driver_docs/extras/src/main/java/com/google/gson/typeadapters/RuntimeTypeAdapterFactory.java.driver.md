# Purpose
The provided Java source code defines a class [`RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory) within the `com.google.gson.typeadapters` package. This class is a custom implementation of the `TypeAdapterFactory` interface from the Gson library, designed to handle the serialization and deserialization of polymorphic objects. The primary purpose of this class is to manage situations where the runtime type of an object may differ from its declared type, which is a common scenario in object-oriented programming when dealing with inheritance hierarchies. By adding type information to the serialized JSON, this class ensures that the correct subtype is instantiated during deserialization, thus resolving the ambiguity that arises when a field's type is not the same as the type that should be created.

The [`RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory) class provides a mechanism to register subtypes of a base type, associating each subtype with a unique label. This label is used as a type identifier in the JSON representation. The class offers methods to create a new type adapter factory for a given base type, register subtypes with or without explicit labels, and handle subtype recognition. The class also includes a nested `TypeAdapter` implementation that overrides the [`read`](#createread) and [`write`](#createwrite) methods to manage the JSON conversion process, ensuring that the type information is correctly handled. This functionality is crucial for applications that require precise control over JSON serialization and deserialization, particularly when dealing with complex data models involving polymorphism.
# Imports and Dependencies

---
- `com.google.gson.typeadapters`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.Gson`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonPrimitive`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.util.LinkedHashMap`
- `java.util.Map`


# Classes

---
### RuntimeTypeAdapterFactory<!-- {{#class:com.google.gson.typeadapters.RuntimeTypeAdapterFactory}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `RuntimeTypeAdapterFactory` class is a custom Gson `TypeAdapterFactory` that facilitates the serialization and deserialization of polymorphic objects by adding type information to JSON. It allows for the registration of subtypes of a base type, associating each subtype with a unique label, which is used to identify the subtype during JSON serialization and deserialization. This class is particularly useful when dealing with fields whose runtime type may differ from their declared type, ensuring that the correct subtype is instantiated when deserializing JSON data.
- **Fields**:
    - `baseType`: `Class<?>` The base class type for which this factory is created.
    - `typeFieldName`: `String` The name of the field in JSON that holds the type information.
    - `labelToSubtype`: `Map<String, Class<?>>` A map associating type labels with their corresponding subtype classes.
    - `subtypeToLabel`: `Map<Class<?>, String>` A map associating subtype classes with their corresponding type labels.
    - `maintainType`: `boolean` A flag indicating whether the type field should be included in deserialized objects.
    - `recognizeSubtypes`: `boolean` A flag indicating whether subtypes of the base type should be recognized.
- **Methods**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactoryRuntimeTypeAdapterFactory)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of`](#RuntimeTypeAdapterFactoryof)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.recognizeSubtypes`](#RuntimeTypeAdapterFactoryrecognizeSubtypes)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype)
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.create`](#RuntimeTypeAdapterFactorycreate)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### RuntimeTypeAdapterFactory\.RuntimeTypeAdapterFactory<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.RuntimeTypeAdapterFactory}} -->
The `RuntimeTypeAdapterFactory` constructor initializes a new instance with a specified base type, type field name, and a flag indicating whether to maintain the type field in deserialized objects.
- **Modifiers**: `private`
- **Inputs**:
    - `baseType`: The base class type for which the runtime type adapter is being created.
    - `typeFieldName`: The name of the field in the JSON that will hold the type information.
    - `maintainType`: A boolean flag indicating whether the type field should be included in deserialized objects.
- **Control Flow**:
    - Check if `typeFieldName` or `baseType` is null, and if so, throw a `NullPointerException`.
    - Assign the `baseType` parameter to the instance variable `this.baseType`.
    - Assign the `typeFieldName` parameter to the instance variable `this.typeFieldName`.
    - Assign the `maintainType` parameter to the instance variable `this.maintainType`.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of `RuntimeTypeAdapterFactory`.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.of<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of}} -->
The `of` method creates a new instance of `RuntimeTypeAdapterFactory` with specified base type, type field name, and a flag indicating whether to maintain the type field in deserialized objects.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `baseType`: The base class type for which the runtime type adapter factory is being created.
    - `typeFieldName`: The name of the field in JSON that will hold the type information.
    - `maintainType`: A boolean flag indicating whether the type field should be included in deserialized objects.
- **Control Flow**:
    - The method takes three parameters: `baseType`, `typeFieldName`, and `maintainType`.
    - It returns a new instance of `RuntimeTypeAdapterFactory` initialized with the provided parameters.
- **Output**:
    - A new instance of `RuntimeTypeAdapterFactory` configured with the specified base type, type field name, and maintain type flag.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.of<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of}} -->
The `of` method creates a new `RuntimeTypeAdapterFactory` for a specified base type and type field name, with an option to maintain the type field in deserialized objects.
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `baseType`: The class type that serves as the base type for the runtime type adapter.
    - `typeFieldName`: The name of the field in the JSON that will hold the type information.
- **Control Flow**:
    - The method calls the constructor of `RuntimeTypeAdapterFactory` with the provided `baseType`, `typeFieldName`, and a default `maintainType` value of `false`.
- **Output**:
    - A new instance of `RuntimeTypeAdapterFactory` configured with the specified base type and type field name.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.of<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.of}} -->
The `of` method creates a new `RuntimeTypeAdapterFactory` for a given base type using a default type field name "type".
- **Modifiers**: `public`, `static`
- **Inputs**:
    - `baseType`: The class type for which the runtime type adapter factory is being created.
- **Control Flow**:
    - The method calls the constructor of `RuntimeTypeAdapterFactory` with the provided `baseType`, a default type field name "type", and `false` for the `maintainType` parameter.
    - The constructor initializes a new `RuntimeTypeAdapterFactory` instance with these parameters.
- **Output**:
    - A new instance of `RuntimeTypeAdapterFactory` configured for the specified base type with a default type field name.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.recognizeSubtypes<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.recognizeSubtypes}} -->
The `recognizeSubtypes` method enables the `RuntimeTypeAdapterFactory` to handle not only the specified base type but also any of its subtypes.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Sets the `recognizeSubtypes` boolean field to `true`, indicating that subtypes should be recognized.
    - Returns the current instance of `RuntimeTypeAdapterFactory` to allow method chaining.
- **Output**:
    - Returns the current instance of `RuntimeTypeAdapterFactory<T>`.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.registerSubtype<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype}} -->
The `registerSubtype` method registers a subtype with a unique label for serialization and deserialization purposes.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: A `Class` object representing the subtype to be registered, which must extend the base type `T`.
    - `label`: A `String` representing the unique label associated with the subtype for identification during serialization and deserialization.
- **Control Flow**:
    - Check if either `type` or `label` is null, and throw a `NullPointerException` if so.
    - Check if the `type` is already registered in `subtypeToLabel` or if the `label` is already registered in `labelToSubtype`, and throw an `IllegalArgumentException` if either is true.
    - Add the `label` and `type` to the `labelToSubtype` and `subtypeToLabel` maps respectively.
    - Return the current instance of `RuntimeTypeAdapterFactory` to allow method chaining.
- **Output**:
    - Returns the current instance of `RuntimeTypeAdapterFactory<T>` to allow for method chaining.
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.registerSubtype<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype}} -->
The [`registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype) method registers a subtype with its simple name as the label in the `RuntimeTypeAdapterFactory`.
- **Modifiers**: `public`
- **Inputs**:
    - `type`: A `Class` object representing the subtype to be registered, which must extend the base type `T`.
- **Control Flow**:
    - The method calls `registerSubtype(Class<? extends T> type, String label)` with the provided `type` and its simple name as the label.
- **Output**:
    - Returns the `RuntimeTypeAdapterFactory` instance, allowing for method chaining.
- **Functions called**:
    - [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory.registerSubtype`](#RuntimeTypeAdapterFactoryregisterSubtype)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)


---
#### RuntimeTypeAdapterFactory\.create<!-- {{#callable:com.google.gson.typeadapters.RuntimeTypeAdapterFactory.create}} -->
The `create` method generates a `TypeAdapter` for a given type, handling polymorphic serialization and deserialization based on registered subtypes and type labels.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of `Gson` used to obtain adapters for JSON elements and subtypes.
    - `type`: A `TypeToken` representing the type for which a `TypeAdapter` is to be created.
- **Control Flow**:
    - Check if the `type` is null; if so, return null.
    - Determine if the `rawType` of the `type` should be handled based on `recognizeSubtypes` and `baseType`.
    - If the `rawType` is not handled, return null.
    - Create a `TypeAdapter` for `JsonElement` using the provided `Gson` instance.
    - Initialize maps to associate type labels and subtypes with their respective `TypeAdapter` instances.
    - Iterate over `labelToSubtype` entries to populate `labelToDelegate` and `subtypeToDelegate` maps with `TypeAdapter` instances for each subtype.
    - Return a new `TypeAdapter` instance that overrides [`read`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterread) and [`write`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite) methods for deserialization and serialization, respectively.
    - In [`read`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterread), use the `jsonElementAdapter` to read a `JsonElement` and extract the type label, throwing a `JsonParseException` if the label is missing or unregistered.
    - In [`write`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite), determine the type label and `TypeAdapter` for the given value, throwing a `JsonParseException` if the type is unregistered, and serialize the object, optionally maintaining the type field.
- **Output**:
    - A `TypeAdapter<R>` instance capable of serializing and deserializing objects of the specified type, handling polymorphic types based on registered subtypes and type labels.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../../../../../../../gson/src/main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.Gson.getAdapter`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.JsonObject.entrySet`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectentrySet)
    - [`com.google.gson.Gson.getDelegateAdapter`](../../../../../../../../gson/src/main/java/com/google/gson/Gson.java.driver.md#GsongetDelegateAdapter)
    - [`com.google.gson.reflect.TypeToken.get`](../../../../../../../../gson/src/main/java/com/google/gson/reflect/TypeToken.java.driver.md#TypeTokenget)
    - [`com.google.gson.TypeAdapter.nullSafe`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapternullSafe)
    - [`com.google.gson.TypeAdapter.read`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.JsonObject.get`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonObject.remove`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectremove)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
    - [`com.google.gson.TypeAdapter.fromJsonTree`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterfromJsonTree)
    - [`com.google.gson.TypeAdapter.toJsonTree`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdaptertoJsonTree)
    - [`com.google.gson.TypeAdapter.write`](../../../../../../../../gson/src/main/java/com/google/gson/TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.JsonObject.has`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjecthas)
    - [`com.google.gson.JsonObject.add`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
- **See also**: [`com.google.gson.typeadapters.RuntimeTypeAdapterFactory`](#RuntimeTypeAdapterFactory)  (Base Class)



