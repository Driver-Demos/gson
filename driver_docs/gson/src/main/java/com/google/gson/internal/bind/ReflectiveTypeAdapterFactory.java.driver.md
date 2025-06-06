# Purpose
The provided Java source code defines the [`ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactoryReflectiveTypeAdapterFactory) class, which is part of the Gson library, a popular Java library for converting Java objects to JSON and vice versa. This class implements the `TypeAdapterFactory` interface and is responsible for creating type adapters that use reflection to serialize and deserialize Java objects. The primary purpose of this class is to facilitate the conversion of Java objects to JSON and back by reflecting over the fields and methods of a class, allowing Gson to handle a wide variety of object types, including those with complex structures.

The [`ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactoryReflectiveTypeAdapterFactory) class is composed of several key components, including a constructor that initializes various strategies and filters, such as `ConstructorConstructor`, `FieldNamingStrategy`, `Excluder`, and `JsonAdapterAnnotationTypeAdapterFactory`. These components are used to control how fields are named, excluded, or adapted during the serialization and deserialization process. The class also defines inner classes like [`BoundField`](#BoundFieldBoundField), [`Adapter`](#AdapterAdapter), [`FieldReflectionAdapter`](#FieldReflectionAdapterFieldReflectionAdapter), and [`RecordAdapter`](#RecordAdapterRecordAdapter), which encapsulate the logic for handling individual fields and records, ensuring that the correct values are read from or written to JSON. The factory supports handling Java records and provides mechanisms to deal with access restrictions through reflection access filters, making it a versatile and essential part of the Gson library's functionality.
# Imports and Dependencies

---
- `com.google.gson.internal.bind`
- `com.google.gson.FieldNamingStrategy`
- `com.google.gson.Gson`
- `com.google.gson.JsonIOException`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonSyntaxException`
- `com.google.gson.ReflectionAccessFilter`
- `com.google.gson.ReflectionAccessFilter.FilterResult`
- `com.google.gson.TypeAdapter`
- `com.google.gson.TypeAdapterFactory`
- `com.google.gson.annotations.JsonAdapter`
- `com.google.gson.annotations.SerializedName`
- `com.google.gson.internal.ConstructorConstructor`
- `com.google.gson.internal.Excluder`
- `com.google.gson.internal.GsonTypes`
- `com.google.gson.internal.ObjectConstructor`
- `com.google.gson.internal.Primitives`
- `com.google.gson.internal.ReflectionAccessFilterHelper`
- `com.google.gson.internal.TroubleshootingGuide`
- `com.google.gson.internal.reflect.ReflectionHelper`
- `com.google.gson.reflect.TypeToken`
- `com.google.gson.stream.JsonReader`
- `com.google.gson.stream.JsonToken`
- `com.google.gson.stream.JsonWriter`
- `java.io.IOException`
- `java.lang.reflect.AccessibleObject`
- `java.lang.reflect.Constructor`
- `java.lang.reflect.Field`
- `java.lang.reflect.InvocationTargetException`
- `java.lang.reflect.Member`
- `java.lang.reflect.Method`
- `java.lang.reflect.Modifier`
- `java.lang.reflect.Type`
- `java.util.ArrayList`
- `java.util.Arrays`
- `java.util.Collections`
- `java.util.HashMap`
- `java.util.LinkedHashMap`
- `java.util.List`
- `java.util.Map`


# Classes

---
### ReflectiveTypeAdapterFactory<!-- {{#class:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `ReflectiveTypeAdapterFactory` class is a final implementation of the `TypeAdapterFactory` interface in the Gson library, designed to create type adapters that use reflection to serialize and deserialize Java objects. It handles various complexities such as field naming strategies, exclusion policies, and reflection access filters, and supports both traditional Java classes and records. The factory can create adapters that either use field reflection or, for JVMs that support it, record adapters that utilize canonical constructors. It also includes mechanisms to handle inaccessible fields and duplicate field names, ensuring robust JSON serialization and deserialization.
- **Fields**:
    - `constructorConstructor`: `ConstructorConstructor` Responsible for constructing instances of objects using reflection.
    - `fieldNamingPolicy`: `FieldNamingStrategy` Defines the strategy for naming fields during serialization and deserialization.
    - `excluder`: `Excluder` Determines which fields should be excluded from serialization and deserialization.
    - `jsonAdapterFactory`: `JsonAdapterAnnotationTypeAdapterFactory` Handles the creation of type adapters based on `@JsonAdapter` annotations.
    - `reflectionFilters`: `List<ReflectionAccessFilter>` A list of filters that control access to fields and methods during reflection.
- **Methods**:
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactoryReflectiveTypeAdapterFactory)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.includeField`](#ReflectiveTypeAdapterFactoryincludeField)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.getFieldNames`](#ReflectiveTypeAdapterFactorygetFieldNames)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.create`](#ReflectiveTypeAdapterFactorycreate)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.checkAccessible`](#ReflectiveTypeAdapterFactorycheckAccessible)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createBoundField`](#ReflectiveTypeAdapterFactorycreateBoundField)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createDuplicateFieldException`](#ReflectiveTypeAdapterFactorycreateDuplicateFieldException)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.getBoundFields`](#ReflectiveTypeAdapterFactorygetBoundFields)
- **Extends/Implements**:
    - [`com.google.gson.TypeAdapterFactory`](../../TypeAdapterFactory.java.driver.md#TypeAdapterFactory)

**Methods**

---
#### ReflectiveTypeAdapterFactory\.ReflectiveTypeAdapterFactory<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.ReflectiveTypeAdapterFactory}} -->
The ReflectiveTypeAdapterFactory constructor initializes a new instance of the ReflectiveTypeAdapterFactory class with specified parameters for constructing type adapters using reflection.
- **Modifiers**: `public`
- **Inputs**:
    - `constructorConstructor`: An instance of ConstructorConstructor used to create object constructors for types.
    - `fieldNamingPolicy`: A FieldNamingStrategy that defines the policy for naming fields.
    - `excluder`: An Excluder instance that determines which fields or classes should be excluded from serialization or deserialization.
    - `jsonAdapterFactory`: A JsonAdapterAnnotationTypeAdapterFactory used to create type adapters based on @JsonAdapter annotations.
    - `reflectionFilters`: A list of ReflectionAccessFilter instances that define access control policies for reflection.
- **Control Flow**:
    - The constructor assigns the provided ConstructorConstructor to the instance variable constructorConstructor.
    - The provided FieldNamingStrategy is assigned to the instance variable fieldNamingPolicy.
    - The Excluder instance is assigned to the instance variable excluder.
    - The JsonAdapterAnnotationTypeAdapterFactory is assigned to the instance variable jsonAdapterFactory.
    - The list of ReflectionAccessFilter instances is assigned to the instance variable reflectionFilters.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the ReflectiveTypeAdapterFactory class.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)


---
#### ReflectiveTypeAdapterFactory\.includeField<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.includeField}} -->
The `includeField` method determines if a given field should be included based on the exclusion criteria defined by the `Excluder`.
- **Modifiers**: `private`
- **Inputs**:
    - `f`: The `Field` object representing the field to be checked for inclusion.
    - `serialize`: A boolean indicating whether the field is being considered for serialization (true) or deserialization (false).
- **Control Flow**:
    - The method calls `excluder.excludeField(f, serialize)` to check if the field should be excluded.
    - It returns the negation of the result from `excluder.excludeField(f, serialize)`, meaning it returns true if the field is not excluded.
- **Output**:
    - A boolean value indicating whether the field should be included (true) or excluded (false).
- **Functions called**:
    - [`com.google.gson.internal.Excluder.excludeField`](../Excluder.java.driver.md#ExcluderexcludeField)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)


---
#### ReflectiveTypeAdapterFactory\.getFieldNames<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.getFieldNames}} -->
The `getFieldNames` method retrieves a list of field names for a given `Field`, considering any `SerializedName` annotation present.
- **Modifiers**: `private`
- **Inputs**:
    - `f`: The `Field` object for which the method retrieves the field names.
- **Control Flow**:
    - Check if the `Field` has a `SerializedName` annotation.
    - If the annotation is present, use its value as the field name and its alternates as the alternate names.
    - If the annotation is not present, use the `fieldNamingPolicy` to translate the field name and get alternate names.
    - If there are no alternate names, return a singleton list containing just the field name.
    - If there are alternate names, create a new list, add the field name, and then add all alternate names to this list.
    - Return the list of field names.
- **Output**:
    - A `List<String>` containing the primary field name followed by any alternate names.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonAdapterAnnotationTypeAdapterFactory.getAnnotation`](JsonAdapterAnnotationTypeAdapterFactory.java.driver.md#JsonAdapterAnnotationTypeAdapterFactorygetAnnotation)
    - [`com.google.gson.FieldNamingStrategy.translateName`](../../FieldNamingStrategy.java.driver.md#FieldNamingStrategytranslateName)
    - [`com.google.gson.FieldNamingStrategy.alternateNames`](../../FieldNamingStrategy.java.driver.md#FieldNamingStrategyalternateNames)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)


---
#### ReflectiveTypeAdapterFactory\.create<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.create}} -->
The `create` method generates a `TypeAdapter` for a given type using reflection, handling special cases for primitive types, anonymous or local classes, and Java records.
- **Modifiers**: `public`
- **Inputs**:
    - `gson`: An instance of the `Gson` class used for JSON serialization and deserialization.
    - `type`: A `TypeToken` representing the type for which a `TypeAdapter` is to be created.
- **Control Flow**:
    - Retrieve the raw class type from the `TypeToken`.
    - Check if the raw type is not assignable from `Object`, returning `null` if it is a primitive type.
    - Check if the raw type is an anonymous or non-static local class, returning a `TypeAdapter` that serializes and deserializes `null` if true.
    - Retrieve the `FilterResult` for the raw type using `ReflectionAccessFilterHelper` and throw a `JsonIOException` if reflection is blocked for the type.
    - Check if the raw type is a Java record, returning a `RecordAdapter` if true.
    - Retrieve an `ObjectConstructor` for the type and return a `FieldReflectionAdapter` using the constructor and bound fields.
- **Output**:
    - A `TypeAdapter<T>` for the specified type, or `null` if the type is a primitive.
- **Functions called**:
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isAnonymousOrNonStaticLocal`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperisAnonymousOrNonStaticLocal)
    - [`com.google.gson.stream.JsonReader.skipValue`](../../stream/JsonReader.java.driver.md#JsonReaderskipValue)
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.getFilterResult`](../ReflectionAccessFilterHelper.java.driver.md#ReflectionAccessFilterHelpergetFilterResult)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isRecord`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperisRecord)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.getBoundFields`](#ReflectiveTypeAdapterFactorygetBoundFields)
    - [`com.google.gson.internal.ConstructorConstructor.get`](../ConstructorConstructor.java.driver.md#ConstructorConstructorget)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)


---
#### ReflectiveTypeAdapterFactory\.checkAccessible<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.checkAccessible}} -->
The `checkAccessible` method verifies if a given member of an object is accessible and throws a `JsonIOException` if it is not accessible and cannot be made accessible due to reflection access filters.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `object`: The object instance whose member's accessibility is being checked; can be null if the member is static.
    - `member`: The member (field or method) of the object whose accessibility is being checked; must implement both `AccessibleObject` and `Member` interfaces.
- **Control Flow**:
    - Check if the member can be accessed using `ReflectionAccessFilterHelper.canAccess`, passing the member and the object (or null if the member is static).
    - If the member cannot be accessed, retrieve a description of the member using `ReflectionHelper.getAccessibleObjectDescription`.
    - Throw a `JsonIOException` with a message indicating that the member is not accessible and suggesting possible solutions.
- **Output**:
    - The method does not return a value; it throws a `JsonIOException` if the member is not accessible and cannot be made accessible.
- **Functions called**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.canAccess`](../ReflectionAccessFilterHelper.java.driver.md#ReflectionAccessFilterHelpercanAccess)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isStatic`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperisStatic)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getAccessibleObjectDescription`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpergetAccessibleObjectDescription)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)


---
#### ReflectiveTypeAdapterFactory\.createBoundField<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createBoundField}} -->
The `createBoundField` method creates a `BoundField` object for a given field, handling serialization and deserialization logic based on the field's characteristics and annotations.
- **Modifiers**: `private`
- **Inputs**:
    - `context`: An instance of `Gson` used to obtain type adapters for serialization and deserialization.
    - `field`: The `Field` object representing the field to be bound.
    - `accessor`: A `Method` object that acts as an accessor for the field, used primarily for records.
    - `serializedName`: The name to be used for the field in JSON serialization.
    - `fieldType`: A `TypeToken` representing the type of the field.
    - `serialize`: A boolean indicating whether the field should be serialized.
    - `blockInaccessible`: A boolean indicating whether access to inaccessible fields should be blocked.
- **Control Flow**:
    - Determine if the field type is primitive using `Primitives.isPrimitive`.
    - Check if the field is static and final using `Modifier.isStatic` and `Modifier.isFinal`.
    - Retrieve any `JsonAdapter` annotation on the field and obtain a `TypeAdapter` using `jsonAdapterFactory` if present.
    - If no `JsonAdapter` is present, use the `Gson` context to get a default `TypeAdapter` for the field type.
    - Create a `TypeAdapterRuntimeTypeWrapper` if serialization is required and no `JsonAdapter` is present.
    - Return a new `BoundField` instance with overridden [`write`](../../TypeAdapter.java.driver.md#TypeAdapterwrite), `readIntoArray`, and `readIntoField` methods to handle JSON serialization and deserialization.
- **Output**:
    - A `BoundField` object that encapsulates the logic for reading and writing the field to and from JSON.
- **Functions called**:
    - [`com.google.gson.internal.Primitives.isPrimitive`](../Primitives.java.driver.md#PrimitivesisPrimitive)
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isStatic`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperisStatic)
    - [`com.google.gson.internal.bind.JsonAdapterAnnotationTypeAdapterFactory.getAnnotation`](JsonAdapterAnnotationTypeAdapterFactory.java.driver.md#JsonAdapterAnnotationTypeAdapterFactorygetAnnotation)
    - [`com.google.gson.internal.bind.JsonAdapterAnnotationTypeAdapterFactory.getTypeAdapter`](JsonAdapterAnnotationTypeAdapterFactory.java.driver.md#JsonAdapterAnnotationTypeAdapterFactorygetTypeAdapter)
    - [`com.google.gson.Gson.getAdapter`](../../Gson.java.driver.md#GsongetAdapter)
    - [`com.google.gson.reflect.TypeToken.getType`](../../reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.checkAccessible`](#ReflectiveTypeAdapterFactorycheckAccessible)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getAccessibleObjectDescription`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpergetAccessibleObjectDescription)
    - [`com.google.gson.stream.JsonWriter.name`](../../stream/JsonWriter.java.driver.md#JsonWritername)
    - [`com.google.gson.TypeAdapter.write`](../../TypeAdapter.java.driver.md#TypeAdapterwrite)
    - [`com.google.gson.TypeAdapter.read`](../../TypeAdapter.java.driver.md#TypeAdapterread)
    - [`com.google.gson.stream.JsonReader.getPath`](../../stream/JsonReader.java.driver.md#JsonReadergetPath)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)


---
#### ReflectiveTypeAdapterFactory\.createDuplicateFieldException<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createDuplicateFieldException}} -->
The `createDuplicateFieldException` method throws an `IllegalArgumentException` when a class declares multiple JSON fields with the same name.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `declaringType`: The `Class<?>` object representing the class that declares the duplicate fields.
    - `duplicateName`: A `String` representing the name of the duplicate JSON field.
    - `field1`: The first `Field` object involved in the conflict.
    - `field2`: The second `Field` object involved in the conflict.
- **Control Flow**:
    - The method constructs an error message detailing the class name, the duplicate field name, and the conflicting fields using their string representations.
    - It then throws an `IllegalArgumentException` with the constructed error message.
- **Output**:
    - The method does not return any value as it always throws an `IllegalArgumentException`.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.fieldToString`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperfieldToString)
    - [`com.google.gson.internal.TroubleshootingGuide.createUrl`](../TroubleshootingGuide.java.driver.md#TroubleshootingGuidecreateUrl)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)


---
#### ReflectiveTypeAdapterFactory\.getBoundFields<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.getBoundFields}} -->
The `getBoundFields` method retrieves and constructs a `FieldsData` object containing mappings of field names to `BoundField` objects for serialization and deserialization of a given class type, considering accessibility and record-specific logic.
- **Modifiers**: `private`
- **Inputs**:
    - `context`: An instance of `Gson` used for context in creating `BoundField` objects.
    - `type`: A `TypeToken<?>` representing the type of the class for which fields are being bound.
    - `raw`: A `Class<?>` object representing the raw class type for which fields are being bound.
    - `blockInaccessible`: A boolean indicating whether inaccessible fields should be blocked from being accessed.
    - `isRecord`: A boolean indicating whether the class type is a Java Record.
- **Control Flow**:
    - Check if the class `raw` is an interface; if so, return an empty `FieldsData` object.
    - Initialize two `LinkedHashMap` objects to store deserialized and serialized fields.
    - Iterate over the class hierarchy starting from `raw` up to `Object.class`.
    - For each class, retrieve its declared fields and check access permissions if the class is not the original raw class.
    - For each field, determine if it should be serialized or deserialized using [`includeField`](#ReflectiveTypeAdapterFactoryincludeField).
    - If the class is a record, handle accessor methods and check for `@SerializedName` annotations on accessors.
    - Make fields or accessors accessible unless `blockInaccessible` is true.
    - Resolve the field type and get field names using [`getFieldNames`](#ReflectiveTypeAdapterFactorygetFieldNames).
    - Create a `BoundField` object for each field and add it to the appropriate map (deserialized or serialized) based on its properties.
    - Check for duplicate field names and throw an exception if found.
    - Continue to the superclass of the current class and repeat the process.
    - Return a new `FieldsData` object containing the deserialized and serialized fields.
- **Output**:
    - A `FieldsData` object containing mappings of field names to `BoundField` objects for both deserialization and serialization.
- **Functions called**:
    - [`com.google.gson.internal.ReflectionAccessFilterHelper.getFilterResult`](../ReflectionAccessFilterHelper.java.driver.md#ReflectionAccessFilterHelpergetFilterResult)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.includeField`](#ReflectiveTypeAdapterFactoryincludeField)
    - [`com.google.gson.internal.reflect.ReflectionHelper.isStatic`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperisStatic)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getAccessor`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpergetAccessor)
    - [`com.google.gson.internal.reflect.ReflectionHelper.makeAccessible`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpermakeAccessible)
    - [`com.google.gson.internal.bind.JsonAdapterAnnotationTypeAdapterFactory.getAnnotation`](JsonAdapterAnnotationTypeAdapterFactory.java.driver.md#JsonAdapterAnnotationTypeAdapterFactorygetAnnotation)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getAccessibleObjectDescription`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpergetAccessibleObjectDescription)
    - [`com.google.gson.internal.GsonTypes.resolve`](../GsonTypes.java.driver.md#GsonTypesresolve)
    - [`com.google.gson.reflect.TypeToken.getType`](../../reflect/TypeToken.java.driver.md#TypeTokengetType)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.getFieldNames`](#ReflectiveTypeAdapterFactorygetFieldNames)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createBoundField`](#ReflectiveTypeAdapterFactorycreateBoundField)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](JsonTreeWriter.java.driver.md#JsonTreeWriterput)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createDuplicateFieldException`](#ReflectiveTypeAdapterFactorycreateDuplicateFieldException)
    - [`com.google.gson.reflect.TypeToken.getRawType`](../../reflect/TypeToken.java.driver.md#TypeTokengetRawType)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory`](#ReflectiveTypeAdapterFactory)  (Base Class)



---
### FieldsData<!-- {{#class:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldsData}} -->
- **Modifiers**: `private`, `static`
- **Description**: The `FieldsData` class is a utility class used to store mappings between JSON member names and their corresponding `BoundField` objects for both deserialization and serialization processes. It provides a static instance `EMPTY` for cases where no fields are present, and it holds two main collections: a map for deserialized fields and a list for serialized fields, which are initialized through its constructor.
- **Fields**:
    - `deserializedFields`: `Map<String, BoundField>` A map that associates JSON member names with their corresponding `BoundField` objects for deserialization.
    - `serializedFields`: `List<BoundField>` A list of `BoundField` objects that are used during the serialization process.
- **Methods**:
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldsData.FieldsData`](#FieldsDataFieldsData)

**Methods**

---
#### FieldsData\.FieldsData<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldsData.FieldsData}} -->
The `FieldsData` constructor initializes an instance with specified maps of deserialized and serialized fields.
- **Modifiers**: `public`
- **Inputs**:
    - `deserializedFields`: A map that associates JSON member names with their corresponding `BoundField` objects for deserialization.
    - `serializedFields`: A list of `BoundField` objects that are used for serialization.
- **Control Flow**:
    - Assigns the `deserializedFields` parameter to the instance variable `this.deserializedFields`.
    - Assigns the `serializedFields` parameter to the instance variable `this.serializedFields`.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldsData`](#ReflectiveTypeAdapterFactory.FieldsData)  (Base Class)



---
### BoundField<!-- {{#class:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField}} -->
- **Modifiers**: `abstract`, `static`
- **Description**: The `BoundField` class is an abstract representation of a field in a Java object that is used for JSON serialization and deserialization, providing methods to write the field's value to a JSON writer, read the value into an array, and set the value on a target object using reflection.
- **Fields**:
    - `serializedName`: `String` Name used for serialization, but not for deserialization.
    - `field`: `Field` The actual field object that this BoundField represents.
    - `fieldName`: `String` Name of the underlying field.
- **Methods**:
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.BoundField`](#BoundFieldBoundField)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.write`](#BoundFieldwrite)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.readIntoArray`](#BoundFieldreadIntoArray)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.readIntoField`](#BoundFieldreadIntoField)

**Methods**

---
#### BoundField\.BoundField<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.BoundField}} -->
The `BoundField` constructor initializes a `BoundField` object with a serialized name and a field, setting the field name to the name of the field.
- **Modifiers**: `protected`
- **Inputs**:
    - `serializedName`: A `String` representing the name used for serialization.
    - `field`: A `Field` object representing the field to be bound.
- **Control Flow**:
    - Assigns the `serializedName` parameter to the `serializedName` field of the object.
    - Assigns the `field` parameter to the `field` field of the object.
    - Sets the `fieldName` field to the name of the `field` using `field.getName()`.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of the `BoundField` class.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField`](#ReflectiveTypeAdapterFactory.BoundField)  (Base Class)


---
#### BoundField\.write<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.write}} -->
The `write` method serializes a field value from a source object into a JSON format using a `JsonWriter`.
- **Modifiers**: `abstract`
- **Inputs**:
    - `writer`: A `JsonWriter` object used to write JSON data.
    - `source`: An `Object` from which the field value is extracted and serialized.
- **Control Flow**:
    - If `blockInaccessible` is true, it checks if the field or accessor is accessible; if not, it throws a `JsonIOException`.
    - Retrieves the field value from the source object using either a method accessor or direct field access.
    - If the field value is the same as the source object, it returns to avoid recursion.
    - Writes the field name to the `JsonWriter`.
    - Uses a `TypeAdapter` to write the field value to the `JsonWriter`.
- **Output**:
    - The method does not return a value; it writes JSON data to the provided `JsonWriter`.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField`](#ReflectiveTypeAdapterFactory.BoundField)  (Base Class)


---
#### BoundField\.readIntoArray<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.readIntoArray}} -->
The `readIntoArray` method reads a JSON value from a `JsonReader` and stores it into a specified index of a target array, ensuring that null values are not assigned to primitive types.
- **Modifiers**: `abstract`
- **Inputs**:
    - `reader`: A `JsonReader` object from which the JSON value is read.
    - `index`: An integer representing the index in the target array where the value should be stored.
    - `target`: An array of `Object` where the read value will be stored at the specified index.
- **Control Flow**:
    - The method reads a value from the `JsonReader` using a `TypeAdapter` specific to the field type.
    - If the read value is `null` and the field type is a primitive, a `JsonParseException` is thrown to prevent assigning `null` to a primitive type.
    - The read value is then stored in the `target` array at the specified `index`.
- **Output**:
    - The method does not return a value; it modifies the `target` array by setting the value at the specified index.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField`](#ReflectiveTypeAdapterFactory.BoundField)  (Base Class)


---
#### BoundField\.readIntoField<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.readIntoField}} -->
The `readIntoField` method reads a JSON value from a `JsonReader` and assigns it to a specified field of a target object using reflection.
- **Modifiers**: `abstract`
- **Inputs**:
    - `reader`: A `JsonReader` object from which the JSON value is read.
    - `target`: The target object whose field is to be set with the value read from the JSON.
- **Control Flow**:
    - The method reads a value from the `JsonReader` using a `TypeAdapter` associated with the field's type.
    - If the read value is not null or the field is not of a primitive type, it proceeds to set the field on the target object.
    - If `blockInaccessible` is true, it checks if the field is accessible and throws an exception if it is not.
    - If the field is `static final`, it throws a `JsonIOException` because such fields cannot be set via reflection.
    - Finally, it sets the field on the target object with the value read from the JSON.
- **Output**:
    - The method does not return a value; it modifies the target object's field directly.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField`](#ReflectiveTypeAdapterFactory.BoundField)  (Base Class)



---
### Adapter<!-- {{#class:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter}} -->
- **Modifiers**: `public`, `abstract`, `static`
- **Description**: The `Adapter` class is an abstract static class that extends `TypeAdapter` and provides a framework for serializing and deserializing JSON objects by reflecting over the fields and methods of a class. It uses a generic type `T` for the object type and `A` for an accumulator used during deserialization. The class manages the reading and writing of JSON data through the `JsonReader` and `JsonWriter` classes, handling null values and exceptions related to illegal access. It requires subclasses to implement methods for creating an accumulator, reading fields into the accumulator, and finalizing the accumulator into an instance of `T`. The class is part of a larger framework for handling JSON serialization and deserialization, likely within the context of the Gson library.
- **Fields**:
    - `fieldsData`: `FieldsData` Holds the serialized and deserialized fields data for the adapter.
- **Methods**:
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.Adapter`](#AdapterAdapter)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.write`](#Adapterwrite)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.read`](#Adapterread)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.createAccumulator`](#AdaptercreateAccumulator)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.readField`](#AdapterreadField)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.finalize`](#Adapterfinalize)

**Methods**

---
#### Adapter\.Adapter<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.Adapter}} -->
The `Adapter` constructor initializes an instance of the `Adapter` class with a given `FieldsData` object.
- **Inputs**:
    - `fieldsData`: An instance of the `FieldsData` class that contains serialized and deserialized fields information.
- **Control Flow**:
    - The constructor assigns the provided `fieldsData` parameter to the instance variable `this.fieldsData`.
- **Output**:
    - This constructor does not return any value as it is a constructor for initializing an object.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter`](#ReflectiveTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.write<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.write}} -->
The [`write`](#BoundFieldwrite) method serializes a given object into JSON format using a `JsonWriter`, handling null values and potential access exceptions.
- **Modifiers**: `public`
- **Inputs**:
    - `out`: A `JsonWriter` object used to write the JSON output.
    - `value`: The object of type `T` to be serialized into JSON.
- **Control Flow**:
    - Check if the `value` is null; if so, write a null value to the `JsonWriter` and return.
    - Begin writing a JSON object using the `JsonWriter`.
    - Iterate over each `BoundField` in `fieldsData.serializedFields`.
    - For each `BoundField`, call its [`write`](#BoundFieldwrite) method to serialize the field value into the JSON output.
    - Catch any `IllegalAccessException` that occurs during field access and throw a new exception using `ReflectionHelper.createExceptionForUnexpectedIllegalAccess`.
    - End the JSON object writing using the `JsonWriter`.
- **Output**:
    - The method does not return a value; it writes the serialized JSON representation of the object to the provided `JsonWriter`.
- **Functions called**:
    - [`com.google.gson.stream.JsonWriter.nullValue`](../../stream/JsonWriter.java.driver.md#JsonWriternullValue)
    - [`com.google.gson.stream.JsonWriter.beginObject`](../../stream/JsonWriter.java.driver.md#JsonWriterbeginObject)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.BoundField.write`](#BoundFieldwrite)
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForUnexpectedIllegalAccess`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpercreateExceptionForUnexpectedIllegalAccess)
    - [`com.google.gson.stream.JsonWriter.endObject`](../../stream/JsonWriter.java.driver.md#JsonWriterendObject)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter`](#ReflectiveTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.read<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.read}} -->
The `read` method deserializes a JSON object from a `JsonReader` into an instance of type `T` using reflection.
- **Modifiers**: `public`
- **Inputs**:
    - `in`: A `JsonReader` object from which the JSON data is read.
- **Control Flow**:
    - Check if the next token in the `JsonReader` is `JsonToken.NULL`; if so, consume it and return `null`.
    - Create an accumulator object using `createAccumulator()` to store field values during deserialization.
    - Retrieve the map of deserialized fields from `fieldsData`.
    - Begin reading the JSON object using `in.beginObject()`.
    - Iterate over each field in the JSON object using `in.hasNext()`.
    - For each field, retrieve its name using `in.nextName()` and find the corresponding `BoundField` from the deserialized fields map.
    - If the `BoundField` is `null`, skip the value using `in.skipValue()`.
    - If the `BoundField` is not `null`, read the field value into the accumulator using `readField(accumulator, in, field)`.
    - Handle potential exceptions: `IllegalStateException` is wrapped in a `JsonSyntaxException`, and `IllegalAccessException` is wrapped using `ReflectionHelper.createExceptionForUnexpectedIllegalAccess(e)`.
    - End reading the JSON object using `in.endObject()`.
    - Finalize the accumulator into an instance of type `T` using `finalize(accumulator)` and return it.
- **Output**:
    - Returns an instance of type `T` that represents the deserialized JSON object, or `null` if the JSON object is `null`.
- **Functions called**:
    - [`com.google.gson.stream.JsonReader.peek`](../../stream/JsonReader.java.driver.md#JsonReaderpeek)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextNull`](JsonTreeReader.java.driver.md#JsonTreeReadernextNull)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.createAccumulator`](#AdaptercreateAccumulator)
    - [`com.google.gson.internal.bind.JsonTreeReader.beginObject`](JsonTreeReader.java.driver.md#JsonTreeReaderbeginObject)
    - [`com.google.gson.internal.bind.JsonTreeReader.hasNext`](JsonTreeReader.java.driver.md#JsonTreeReaderhasNext)
    - [`com.google.gson.internal.bind.JsonTreeReader.nextName`](JsonTreeReader.java.driver.md#JsonTreeReadernextName)
    - [`com.google.gson.internal.ConstructorConstructor.get`](../ConstructorConstructor.java.driver.md#ConstructorConstructorget)
    - [`com.google.gson.internal.bind.JsonTreeReader.skipValue`](JsonTreeReader.java.driver.md#JsonTreeReaderskipValue)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.readField`](#AdapterreadField)
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForUnexpectedIllegalAccess`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpercreateExceptionForUnexpectedIllegalAccess)
    - [`com.google.gson.internal.bind.JsonTreeReader.endObject`](JsonTreeReader.java.driver.md#JsonTreeReaderendObject)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.finalize`](#Adapterfinalize)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter`](#ReflectiveTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.createAccumulator<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.createAccumulator}} -->
The `createAccumulator` method is an abstract method intended to create an accumulator object used during the deserialization process.
- **Modifiers**: `abstract`
- **Inputs**: None
- **Control Flow**:
    - The method is abstract and does not contain any implementation details.
    - It is intended to be overridden by subclasses to provide specific logic for creating an accumulator object.
- **Output**:
    - An object of type `A`, which serves as an accumulator during deserialization.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter`](#ReflectiveTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.readField<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.readField}} -->
The `readField` method reads a JSON field from a `JsonReader` and stores its value into an accumulator using a `BoundField`.
- **Modifiers**: `abstract`
- **Inputs**:
    - `accumulator`: An object of type A that accumulates the values read from the JSON.
    - `in`: A `JsonReader` object that provides the JSON input to be read.
    - `field`: A `BoundField` object that represents the field to be read from the JSON.
- **Control Flow**:
    - The method is abstract, so its implementation is not provided in the code snippet.
    - It is expected to read a value from the `JsonReader` corresponding to the `BoundField`.
    - The value read is then stored into the provided accumulator.
- **Output**:
    - The method does not return a value; it modifies the accumulator by adding the field's value.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter`](#ReflectiveTypeAdapterFactory.Adapter)  (Base Class)


---
#### Adapter\.finalize<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter.finalize}} -->
The `finalize` method converts an accumulator object into a final instance of type T.
- **Modifiers**: `abstract`
- **Inputs**:
    - `accumulator`: An object of type A that holds accumulated data to be converted into a final instance of type T.
- **Control Flow**:
    - The method takes an accumulator of type A as input.
    - It processes the accumulator to produce a final instance of type T.
    - The specific implementation details are left to subclasses, as this is an abstract method.
- **Output**:
    - An instance of type T, which is the final result of processing the accumulator.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.Adapter`](#ReflectiveTypeAdapterFactory.Adapter)  (Base Class)



---
### FieldReflectionAdapter<!-- {{#class:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `FieldReflectionAdapter` class is a specialized adapter that extends the `Adapter` class to facilitate the reflection-based serialization and deserialization of fields in a Java object. It utilizes an `ObjectConstructor` to create instances of the object type `T` and manages the reading and writing of fields using reflection, allowing for dynamic handling of JSON data with the Gson library.
- **Fields**:
    - `constructor`: `ObjectConstructor<T>` An `ObjectConstructor` instance used to create new instances of the type `T`.
- **Methods**:
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.FieldReflectionAdapter`](#FieldReflectionAdapterFieldReflectionAdapter)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.createAccumulator`](#FieldReflectionAdaptercreateAccumulator)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.readField`](#FieldReflectionAdapterreadField)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.finalize`](#FieldReflectionAdapterfinalize)

**Methods**

---
#### FieldReflectionAdapter\.FieldReflectionAdapter<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.FieldReflectionAdapter}} -->
The `FieldReflectionAdapter` constructor initializes a new instance of the `FieldReflectionAdapter` class with a given object constructor and fields data.
- **Inputs**:
    - `constructor`: An `ObjectConstructor<T>` instance used to construct objects of type `T`.
    - `fieldsData`: A `FieldsData` instance containing the mapping of field names to `BoundField` objects for serialization and deserialization.
- **Control Flow**:
    - The constructor calls the superclass constructor with `fieldsData` as an argument.
    - It assigns the `constructor` parameter to the instance variable `this.constructor`.
- **Output**:
    - This constructor does not return a value as it is used to initialize an instance of the `FieldReflectionAdapter` class.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter`](#ReflectiveTypeAdapterFactory.FieldReflectionAdapter)  (Base Class)


---
#### FieldReflectionAdapter\.createAccumulator<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.createAccumulator}} -->
The `createAccumulator` method constructs and returns a new instance of type `T` using a predefined constructor.
- **Modifiers**: ``
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`construct`](../ObjectConstructor.java.driver.md#ObjectConstructorconstruct) method on the `constructor` object, which is an instance of `ObjectConstructor<T>`, to create a new instance of type `T`.
- **Output**:
    - A new instance of type `T` is returned.
- **Functions called**:
    - [`com.google.gson.internal.ObjectConstructor.construct`](../ObjectConstructor.java.driver.md#ObjectConstructorconstruct)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter`](#ReflectiveTypeAdapterFactory.FieldReflectionAdapter)  (Base Class)


---
#### FieldReflectionAdapter\.readField<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.readField}} -->
The `readField` method reads a JSON field from a `JsonReader` and assigns its value to a specified field in an accumulator object.
- **Modifiers**: `void`
- **Inputs**:
    - `accumulator`: The object into which the field value will be read and stored.
    - `in`: The `JsonReader` instance from which the JSON field value is read.
    - `field`: The `BoundField` object representing the field to be read and set in the accumulator.
- **Control Flow**:
    - The method calls `field.readIntoField(in, accumulator)` to read the JSON field value from the `JsonReader` and set it into the specified field of the accumulator object.
- **Output**:
    - This method does not return any value; it modifies the state of the accumulator object by setting the field value.
- **Functions called**:
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createBoundField.readIntoField`](#ReflectiveTypeAdapterFactorycreateBoundField.readIntoField)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter`](#ReflectiveTypeAdapterFactory.FieldReflectionAdapter)  (Base Class)


---
#### FieldReflectionAdapter\.finalize<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter.finalize}} -->
The `finalize` method returns the given accumulator without any modifications.
- **Modifiers**: ``
- **Inputs**:
    - `accumulator`: The input parameter of generic type T, which is intended to be the object or data structure being finalized or processed.
- **Control Flow**:
    - The method takes a single parameter named `accumulator` of generic type T.
    - It directly returns the `accumulator` parameter without performing any operations on it.
- **Output**:
    - The method returns the same object that was passed in as the `accumulator` parameter.
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.FieldReflectionAdapter`](#ReflectiveTypeAdapterFactory.FieldReflectionAdapter)  (Base Class)



---
### RecordAdapter<!-- {{#class:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter}} -->
- **Modifiers**: `private`, `static`, `final`
- **Description**: The `RecordAdapter` class is a specialized adapter for handling Java Record types in the Gson library, allowing for serialization and deserialization of record components by reflecting over their canonical constructor and ensuring that primitive fields are initialized with default values.
- **Fields**:
    - `PRIMITIVE_DEFAULTS`: `Map<Class<?>, Object>` A static map that holds default values for primitive types.
    - `constructor`: `Constructor<T>` The canonical constructor of the record type being adapted.
    - `constructorArgsDefaults`: `Object[]` An array of default argument values for the record's constructor, ensuring non-null values for primitives.
    - `componentIndices`: `Map<String, Integer>` A map that associates record component names with their respective indices in the constructor's argument list.
- **Methods**:
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.RecordAdapter`](#RecordAdapterRecordAdapter)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.primitiveDefaults`](#RecordAdapterprimitiveDefaults)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.createAccumulator`](#RecordAdaptercreateAccumulator)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.readField`](#RecordAdapterreadField)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.finalize`](#RecordAdapterfinalize)

**Methods**

---
#### RecordAdapter\.RecordAdapter<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.RecordAdapter}} -->
The `RecordAdapter` constructor initializes a type adapter for Java records, ensuring accessibility and setting default values for primitive fields.
- **Modifiers**: ``
- **Inputs**:
    - `raw`: The `Class<T>` object representing the record type to be adapted.
    - `fieldsData`: An instance of `FieldsData` containing the fields to be serialized and deserialized.
    - `blockInaccessible`: A boolean indicating whether to block access to inaccessible fields and methods.
- **Control Flow**:
    - The constructor calls the superclass constructor with `fieldsData`.
    - It retrieves the canonical constructor of the record using `ReflectionHelper.getCanonicalRecordConstructor(raw)`.
    - If `blockInaccessible` is true, it checks the accessibility of the constructor using [`checkAccessible`](#ReflectiveTypeAdapterFactorycheckAccessible); otherwise, it makes the constructor accessible using `ReflectionHelper.makeAccessible`.
    - It retrieves the record component names using `ReflectionHelper.getRecordComponentNames(raw)` and maps each component name to its index in the constructor's parameter list.
    - It initializes an array `constructorArgsDefaults` to hold default values for the constructor's parameters, setting non-null defaults for primitive types using `PRIMITIVE_DEFAULTS`.
- **Output**:
    - The method does not return a value as it is a constructor.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.getCanonicalRecordConstructor`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpergetCanonicalRecordConstructor)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.checkAccessible`](#ReflectiveTypeAdapterFactorycheckAccessible)
    - [`com.google.gson.internal.reflect.ReflectionHelper.makeAccessible`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpermakeAccessible)
    - [`com.google.gson.internal.reflect.ReflectionHelper.getRecordComponentNames`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpergetRecordComponentNames)
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](JsonTreeWriter.java.driver.md#JsonTreeWriterput)
    - [`com.google.gson.internal.ConstructorConstructor.get`](../ConstructorConstructor.java.driver.md#ConstructorConstructorget)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter`](#ReflectiveTypeAdapterFactory.RecordAdapter)  (Base Class)


---
#### RecordAdapter\.primitiveDefaults<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.primitiveDefaults}} -->
The `primitiveDefaults` method creates and returns a map associating Java primitive types with their default values.
- **Modifiers**: `private`, `static`
- **Inputs**: None
- **Control Flow**:
    - A new `HashMap` is instantiated to store the default values of primitive types.
    - The method populates the map with entries for each primitive type: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, and `boolean`, associating each with its default value.
    - The populated map is returned.
- **Output**:
    - A `Map<Class<?>, Object>` containing primitive types as keys and their default values as values.
- **Functions called**:
    - [`com.google.gson.internal.bind.JsonTreeWriter.put`](JsonTreeWriter.java.driver.md#JsonTreeWriterput)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter`](#ReflectiveTypeAdapterFactory.RecordAdapter)  (Base Class)


---
#### RecordAdapter\.createAccumulator<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.createAccumulator}} -->
The `createAccumulator` method returns a clone of the `constructorArgsDefaults` array.
- **Modifiers**: `@Override`
- **Inputs**: None
- **Control Flow**:
    - The method simply returns a clone of the `constructorArgsDefaults` array using the `clone()` method.
- **Output**:
    - An `Object[]` array which is a clone of the `constructorArgsDefaults` array.
- **Functions called**:
    - [`com.google.gson.internal.Excluder.clone`](../Excluder.java.driver.md#Excluderclone)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter`](#ReflectiveTypeAdapterFactory.RecordAdapter)  (Base Class)


---
#### RecordAdapter\.readField<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.readField}} -->
The `readField` method reads a JSON field into an accumulator array using a specified `BoundField` and `JsonReader`, ensuring the field corresponds to a constructor argument index.
- **Modifiers**: `@Override`
- **Inputs**:
    - `accumulator`: An array of Objects used to accumulate field values for constructing an object.
    - `in`: A `JsonReader` instance used to read JSON data.
    - `field`: A `BoundField` object representing the field to be read from the JSON.
- **Control Flow**:
    - Retrieve the component index for the field using its name from the `componentIndices` map.
    - If the component index is null, throw an `IllegalStateException` indicating the field name could not be matched to a constructor argument.
    - Invoke the [`readIntoArray`](#ReflectiveTypeAdapterFactorycreateBoundField.readIntoArray) method on the `field` object, passing the `JsonReader`, component index, and accumulator array to read the field value into the accumulator.
- **Output**:
    - The method does not return a value; it modifies the `accumulator` array by setting the field value at the appropriate index.
- **Functions called**:
    - [`com.google.gson.internal.ConstructorConstructor.get`](../ConstructorConstructor.java.driver.md#ConstructorConstructorget)
    - [`com.google.gson.internal.reflect.ReflectionHelper.constructorToString`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperconstructorToString)
    - [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.createBoundField.readIntoArray`](#ReflectiveTypeAdapterFactorycreateBoundField.readIntoArray)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter`](#ReflectiveTypeAdapterFactory.RecordAdapter)  (Base Class)


---
#### RecordAdapter\.finalize<!-- {{#callable:com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter.finalize}} -->
The `finalize` method attempts to create a new instance of a record using a constructor and an array of arguments, handling various exceptions that may occur during this process.
- **Modifiers**: `override`
- **Inputs**:
    - `accumulator`: An array of `Object` that contains the arguments to be passed to the constructor for creating a new instance.
- **Control Flow**:
    - The method attempts to create a new instance of a record by invoking the constructor with the provided `accumulator` array using `constructor.newInstance(accumulator)`.
    - If an `IllegalAccessException` is caught, it throws a new exception created by `ReflectionHelper.createExceptionForUnexpectedIllegalAccess(e)`.
    - If an `InstantiationException` or `IllegalArgumentException` is caught, it throws a `RuntimeException` with a message indicating the failure to invoke the constructor, including the constructor's string representation and the arguments.
    - If an `InvocationTargetException` is caught, it throws a `RuntimeException` with a message indicating the failure to invoke the constructor, including the constructor's string representation and the arguments, and uses the cause of the caught exception.
- **Output**:
    - Returns an instance of type `T` created by invoking the constructor with the provided arguments.
- **Functions called**:
    - [`com.google.gson.internal.reflect.ReflectionHelper.createExceptionForUnexpectedIllegalAccess`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelpercreateExceptionForUnexpectedIllegalAccess)
    - [`com.google.gson.internal.reflect.ReflectionHelper.constructorToString`](../reflect/ReflectionHelper.java.driver.md#ReflectionHelperconstructorToString)
    - [`com.google.gson.TypeAdapter.NullSafeTypeAdapter.toString`](../../TypeAdapter.java.driver.md#NullSafeTypeAdaptertoString)
- **See also**: [`com.google.gson.internal.bind.ReflectiveTypeAdapterFactory.RecordAdapter`](#ReflectiveTypeAdapterFactory.RecordAdapter)  (Base Class)



