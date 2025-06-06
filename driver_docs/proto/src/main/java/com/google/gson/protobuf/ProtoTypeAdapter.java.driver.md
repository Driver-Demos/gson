# Purpose
The provided Java source code defines a class [`ProtoTypeAdapter`](#ProtoTypeAdapterProtoTypeAdapter) that serves as a type adapter for Google's GSON library, specifically designed to handle serialization and deserialization of Protocol Buffers (protobuf) messages. This class implements both `JsonSerializer<Message>` and `JsonDeserializer<Message>`, allowing it to convert protobuf messages to JSON format and vice versa. The primary functionality of this adapter is to manage the serialization of protobuf enums and fields, offering flexibility in how these elements are represented in JSON. It supports serialization of enums by either their numeric values or names and allows customization of field names through extensions and case format conversions. The adapter can be configured using a nested [`Builder`](#BuilderBuilder) class, which provides methods to set serialization preferences, such as enum serialization strategy, field name formats, and custom extensions for field and enum value names.

The [`ProtoTypeAdapter`](#ProtoTypeAdapterProtoTypeAdapter) class is a comprehensive solution for integrating protobuf with JSON in Java applications, providing a customizable interface for developers to define how protobuf messages are serialized into JSON. It includes mechanisms to handle custom field and enum value names, leveraging protobuf extensions and annotations. The class also supports concurrent access through the use of `ConcurrentMap` for caching reflection methods, ensuring efficient performance in multi-threaded environments. This adapter is particularly useful in scenarios where JSON is used as a data interchange format, and there is a need to maintain consistency with existing protobuf definitions, allowing for seamless integration between JSON and protobuf data models.
# Imports and Dependencies

---
- `com.google.gson.protobuf`
- `java.util.Objects.requireNonNull`
- `com.google.common.base.CaseFormat`
- `com.google.common.collect.MapMaker`
- `com.google.common.reflect.TypeToken`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `com.google.gson.JsonArray`
- `com.google.gson.JsonDeserializationContext`
- `com.google.gson.JsonDeserializer`
- `com.google.gson.JsonElement`
- `com.google.gson.JsonObject`
- `com.google.gson.JsonParseException`
- `com.google.gson.JsonSerializationContext`
- `com.google.gson.JsonSerializer`
- `com.google.protobuf.DescriptorProtos.EnumValueOptions`
- `com.google.protobuf.DescriptorProtos.FieldOptions`
- `com.google.protobuf.Descriptors.Descriptor`
- `com.google.protobuf.Descriptors.EnumDescriptor`
- `com.google.protobuf.Descriptors.EnumValueDescriptor`
- `com.google.protobuf.Descriptors.FieldDescriptor`
- `com.google.protobuf.DynamicMessage`
- `com.google.protobuf.Extension`
- `com.google.protobuf.Message`
- `java.lang.reflect.Field`
- `java.lang.reflect.Method`
- `java.lang.reflect.Type`
- `java.util.ArrayList`
- `java.util.Collection`
- `java.util.HashSet`
- `java.util.List`
- `java.util.Map`
- `java.util.Set`
- `java.util.concurrent.ConcurrentMap`


# Classes

---
### ProtoTypeAdapter<!-- {{#class:com.google.gson.protobuf.ProtoTypeAdapter}} -->
- **Modifiers**: `public`
- **Description**: The `ProtoTypeAdapter` class is a GSON type adapter designed for protocol buffers, enabling the serialization and deserialization of protocol buffer messages to and from JSON. It supports custom serialization of enum values either by their names or numbers and allows for custom proto field names through extensions. The class provides a builder pattern for configuration, allowing users to specify case formats for field names and to add custom extensions for serialized names and enum values. It also includes functionality to handle JSON name field options and ensures compatibility with generated protocol buffer messages.
- **Fields**:
    - `ENUM_TYPE`: `FieldDescriptor.Type` A static final field representing the type of enum fields in protocol buffers.
    - `mapOfMapOfMethods`: `ConcurrentMap<String, ConcurrentMap<Class<?>, Method>>` A static final concurrent map caching methods for reflection purposes, organized by method name and class type.
    - `enumSerialization`: `EnumSerialization` A final field indicating the method of enum serialization, either by name or number.
    - `protoFormat`: `CaseFormat` A final field specifying the case format of proto field names.
    - `jsonFormat`: `CaseFormat` A final field specifying the case format of JSON field names.
    - `serializedNameExtensions`: `Set<Extension<FieldOptions, String>>` A final set of extensions for custom serialized field names.
    - `serializedEnumValueExtensions`: `Set<Extension<EnumValueOptions, String>>` A final set of extensions for custom serialized enum values.
    - `shouldUseJsonNameFieldOption`: `boolean` A final boolean indicating whether to use the JSON name field option for serialization.
- **Methods**:
    - [`com.google.gson.protobuf.ProtoTypeAdapter.newBuilder`](#ProtoTypeAdapternewBuilder)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.ProtoTypeAdapter`](#ProtoTypeAdapterProtoTypeAdapter)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.serialize`](#ProtoTypeAdapterserialize)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.deserialize`](#ProtoTypeAdapterdeserialize)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedName`](#ProtoTypeAdaptergetCustSerializedName)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedEnumValue`](#ProtoTypeAdaptergetCustSerializedEnumValue)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getEnumValue`](#ProtoTypeAdaptergetEnumValue)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.findValueByNameAndExtension`](#ProtoTypeAdapterfindValueByNameAndExtension)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCachedMethod`](#ProtoTypeAdaptergetCachedMethod)

**Methods**

---
#### ProtoTypeAdapter\.newBuilder<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.newBuilder}} -->
The `newBuilder` method creates and returns a new `Builder` instance with default settings for enum serialization and field name conversion.
- **Modifiers**: `public`, `static`
- **Inputs**: None
- **Control Flow**:
    - The method instantiates a new `Builder` object.
    - It passes `EnumSerialization.NAME`, `CaseFormat.LOWER_UNDERSCORE`, and `CaseFormat.LOWER_CAMEL` as arguments to the `Builder` constructor.
    - The method returns the newly created `Builder` instance.
- **Output**:
    - A new `Builder` instance configured with default settings for enum serialization and field name conversion.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.ProtoTypeAdapter<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.ProtoTypeAdapter}} -->
The `ProtoTypeAdapter` constructor initializes a new instance with specified serialization settings and extensions for handling protocol buffer fields and enums.
- **Modifiers**: `private`
- **Inputs**:
    - `enumSerialization`: Determines how enum values should be serialized, either by name or number.
    - `protoFormat`: Specifies the case format used for proto field names.
    - `jsonFormat`: Specifies the case format used for JSON field names.
    - `serializedNameExtensions`: A set of extensions for custom serialized field names.
    - `serializedEnumValueExtensions`: A set of extensions for custom serialized enum values.
    - `shouldUseJsonNameFieldOption`: A boolean flag indicating whether to use the json_name field option for serialization.
- **Control Flow**:
    - Assigns the provided `enumSerialization` to the instance variable `this.enumSerialization`.
    - Assigns the provided `protoFormat` to the instance variable `this.protoFormat`.
    - Assigns the provided `jsonFormat` to the instance variable `this.jsonFormat`.
    - Assigns the provided `serializedNameExtensions` to the instance variable `this.serializedNameExtensions`.
    - Assigns the provided `serializedEnumValueExtensions` to the instance variable `this.serializedEnumValueExtensions`.
    - Assigns the provided `shouldUseJsonNameFieldOption` to the instance variable `this.shouldUseJsonNameFieldOption`.
- **Output**:
    - This constructor does not return a value; it initializes the state of a `ProtoTypeAdapter` instance.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.serialize<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.serialize}} -->
The [`serialize`](../../../../../../../../gson/src/main/java/com/google/gson/JsonSerializationContext.java.driver.md#JsonSerializationContextserialize) method converts a Protocol Buffer `Message` object into a JSON representation using custom serialization rules for field names and enum values.
- **Modifiers**: `public`
- **Inputs**:
    - `src`: The `Message` object to be serialized into JSON.
    - `typeOfSrc`: The type of the source object, typically used for generic type information.
    - `context`: The `JsonSerializationContext` used to serialize the fields of the `Message` object.
- **Control Flow**:
    - Initialize a `JsonObject` to hold the serialized data.
    - Retrieve all fields from the `Message` object using `getAllFields()`.
    - Iterate over each field in the `Message` object.
    - For each field, determine its custom serialized name using `getCustSerializedName()`.
    - Check if the field type is `ENUM_TYPE`.
    - If the field is an enum and a collection, create a `JsonArray` and serialize each enum value using `getEnumValue()` and add it to the array.
    - If the field is a single enum value, serialize it using `getEnumValue()` and add it to the `JsonObject`.
    - For non-enum fields, serialize the field value directly and add it to the `JsonObject`.
    - Return the `JsonObject` containing the serialized data.
- **Output**:
    - A `JsonElement` representing the serialized JSON object of the `Message`.
- **Functions called**:
    - [`com.google.gson.JsonObject.entrySet`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectentrySet)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedName`](#ProtoTypeAdaptergetCustSerializedName)
    - [`com.google.gson.JsonObject.add`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectadd)
    - [`com.google.gson.JsonSerializationContext.serialize`](../../../../../../../../gson/src/main/java/com/google/gson/JsonSerializationContext.java.driver.md#JsonSerializationContextserialize)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getEnumValue`](#ProtoTypeAdaptergetEnumValue)
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.deserialize<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.deserialize}} -->
The [`deserialize`](../../../../../../../../gson/src/main/java/com/google/gson/JsonDeserializationContext.java.driver.md#JsonDeserializationContextdeserialize) method converts a JSON element into a Protocol Buffer `Message` object by mapping JSON fields to their corresponding Protocol Buffer fields.
- **Modifiers**: `public`
- **Inputs**:
    - `json`: A `JsonElement` representing the JSON data to be deserialized.
    - `typeOfT`: A `Type` object representing the type of the Protocol Buffer message to be deserialized into.
    - `context`: A `JsonDeserializationContext` used to facilitate the deserialization of JSON elements into Java objects.
- **Control Flow**:
    - Convert the input `JsonElement` to a `JsonObject`.
    - Cast the `typeOfT` to a `Class` object representing the Protocol Buffer message class.
    - Check if the class is a `DynamicMessage` and throw an `IllegalStateException` if true, as only generated messages are supported.
    - Invoke the `newBuilder` method on the Protocol Buffer class to get a `Message.Builder` instance.
    - Invoke the `getDefaultInstance` method to get a default instance of the message.
    - Invoke the `getDescriptor` method to get the message's `Descriptor`.
    - Iterate over each `FieldDescriptor` in the message's descriptor.
    - For each field, retrieve the corresponding JSON element using a custom serialized name.
    - If the JSON element is not null, determine the field type and deserialize accordingly:
    - For enum fields, handle both single values and arrays, converting JSON values to `EnumValueDescriptor` objects.
    - For repeated fields, determine the field type and deserialize the JSON array into a list.
    - For other fields, use the default instance to determine the field type and deserialize the JSON element.
    - Set the deserialized field value on the `Message.Builder`.
    - Build and return the `Message` object from the `Message.Builder`.
    - Catch any exceptions and throw a `JsonParseException` with an error message.
- **Output**:
    - Returns a `Message` object that represents the deserialized Protocol Buffer message.
- **Functions called**:
    - [`com.google.gson.JsonElement.getAsJsonObject`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonObject)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCachedMethod`](#ProtoTypeAdaptergetCachedMethod)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedName`](#ProtoTypeAdaptergetCustSerializedName)
    - [`com.google.gson.JsonObject.get`](../../../../../../../../gson/src/main/java/com/google/gson/JsonObject.java.driver.md#JsonObjectget)
    - [`com.google.gson.JsonElement.isJsonNull`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementisJsonNull)
    - [`com.google.gson.JsonElement.isJsonArray`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementisJsonArray)
    - [`com.google.gson.JsonElement.getAsJsonArray`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsJsonArray)
    - [`com.google.gson.JsonArray.size`](../../../../../../../../gson/src/main/java/com/google/gson/JsonArray.java.driver.md#JsonArraysize)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.findValueByNameAndExtension`](#ProtoTypeAdapterfindValueByNameAndExtension)
    - [`com.google.gson.JsonDeserializationContext.deserialize`](../../../../../../../../gson/src/main/java/com/google/gson/JsonDeserializationContext.java.driver.md#JsonDeserializationContextdeserialize)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.build`](#Builderbuild)
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.getCustSerializedName<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedName}} -->
The `getCustSerializedName` method retrieves a custom serialized name for a given field descriptor, using extensions or JSON name options if available, or defaults to a formatted field name.
- **Modifiers**: `private`
- **Inputs**:
    - `fieldDescriptor`: An instance of `FieldDescriptor` representing the field for which the custom serialized name is to be retrieved.
- **Control Flow**:
    - Retrieve the `FieldOptions` from the provided `FieldDescriptor`.
    - Iterate over the `serializedNameExtensions` set to check if any extension is present in the `FieldOptions`.
    - If an extension is found, return the corresponding extension value from the `FieldOptions`.
    - If `shouldUseJsonNameFieldOption` is true and the `FieldDescriptor` has a JSON name, return the JSON name.
    - If no custom name is found, convert the field name using `protoFormat` to `jsonFormat` and return the result.
- **Output**:
    - Returns a `String` representing the custom serialized name for the field, or a formatted default name if no custom name is found.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.getCustSerializedEnumValue<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedEnumValue}} -->
The `getCustSerializedEnumValue` method retrieves a custom serialized enum value from the given options or returns a default value if no custom value is found.
- **Modifiers**: `private`
- **Inputs**:
    - `options`: An instance of `EnumValueOptions` which may contain custom serialized enum value extensions.
    - `defaultValue`: A `String` representing the default value to return if no custom serialized enum value is found in the options.
- **Control Flow**:
    - Iterates over each `Extension<EnumValueOptions, String>` in `serializedEnumValueExtensions`.
    - Checks if the `options` has the current `extension` using `options.hasExtension(extension)`.
    - If the `options` has the extension, returns the custom serialized enum value using `options.getExtension(extension)`.
    - If no custom serialized enum value is found after iterating through all extensions, returns the `defaultValue`.
- **Output**:
    - Returns a `String` which is either the custom serialized enum value found in the options or the provided default value.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.getEnumValue<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.getEnumValue}} -->
The `getEnumValue` method returns the serialized value of an enum based on the specified serialization strategy.
- **Modifiers**: `private`
- **Inputs**:
    - `enumDesc`: An `EnumValueDescriptor` object representing the enum value to be serialized.
- **Control Flow**:
    - Check if the `enumSerialization` is set to `EnumSerialization.NAME`.
    - If true, call [`getCustSerializedEnumValue`](#ProtoTypeAdaptergetCustSerializedEnumValue) with the enum's options and name to get the custom serialized name.
    - If false, return the enum's number using `enumDesc.getNumber()`.
- **Output**:
    - Returns an `Object` which is either the custom serialized name of the enum or its numeric value, depending on the serialization strategy.
- **Functions called**:
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedEnumValue`](#ProtoTypeAdaptergetCustSerializedEnumValue)
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.findValueByNameAndExtension<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.findValueByNameAndExtension}} -->
The `findValueByNameAndExtension` method retrieves an `EnumValueDescriptor` from an `EnumDescriptor` based on a JSON element, using either the enum's name or number depending on the serialization setting.
- **Modifiers**: `private`
- **Inputs**:
    - `desc`: An `EnumDescriptor` object representing the enumeration type to search within.
    - `jsonElement`: A `JsonElement` object containing the JSON representation of the enum value, either as a name or a number.
- **Control Flow**:
    - Check if the `enumSerialization` is set to `EnumSerialization.NAME` to determine if the search should be by name.
    - If searching by name, iterate over the values in `desc` and compare the custom serialized enum value or the default name with the string value of `jsonElement`.
    - If a match is found, return the corresponding `EnumValueDescriptor`.
    - If no match is found by name, throw an `IllegalArgumentException` indicating an unrecognized enum name.
    - If not searching by name, find the enum value by its number using `desc.findValueByNumber` with the integer value of `jsonElement`.
    - If a match is found by number, return the corresponding `EnumValueDescriptor`.
    - If no match is found by number, throw an `IllegalArgumentException` indicating an unrecognized enum value.
- **Output**:
    - Returns an `EnumValueDescriptor` that matches the JSON element's value, either by name or number, or throws an `IllegalArgumentException` if no match is found.
- **Functions called**:
    - [`com.google.gson.protobuf.ProtoTypeAdapter.getCustSerializedEnumValue`](#ProtoTypeAdaptergetCustSerializedEnumValue)
    - [`com.google.gson.JsonElement.getAsString`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsString)
    - [`com.google.gson.JsonElement.getAsInt`](../../../../../../../../gson/src/main/java/com/google/gson/JsonElement.java.driver.md#JsonElementgetAsInt)
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)


---
#### ProtoTypeAdapter\.getCachedMethod<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.getCachedMethod}} -->
The `getCachedMethod` method retrieves a cached `Method` object for a specified class and method name, or fetches and caches it if not already present.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `clazz`: The `Class<?>` object representing the class from which the method is to be retrieved.
    - `methodName`: The name of the method to be retrieved as a `String`.
    - `methodParamTypes`: A varargs parameter representing the parameter types of the method to be retrieved.
- **Control Flow**:
    - Retrieve the `ConcurrentMap` of methods associated with the given `methodName` from `mapOfMapOfMethods`.
    - If the map is `null`, create a new map using `MapMaker` and attempt to put it in `mapOfMapOfMethods` if absent, updating the map reference accordingly.
    - Retrieve the `Method` object from the map using the `clazz` as the key.
    - If the `Method` is `null`, use `clazz.getMethod` to fetch the method with the specified name and parameter types, then cache it in the map using `putIfAbsent`.
    - Return the `Method` object.
- **Output**:
    - Returns a `Method` object representing the method of the specified class with the given name and parameter types.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter`](#ProtoTypeAdapter)  (Base Class)



---
### EnumSerialization<!-- {{#class:com.google.gson.protobuf.ProtoTypeAdapter.EnumSerialization}} -->
- **Modifiers**: `public`
- **Description**: The `EnumSerialization` enum defines two strategies for serializing and deserializing enum values in JSON: using their numeric value (`NUMBER`) or their name (`NAME`). This enum is part of the `ProtoTypeAdapter` class, which is a GSON type adapter for protocol buffers, allowing customization of how enums and field names are serialized and deserialized in JSON.


---
### Builder<!-- {{#class:com.google.gson.protobuf.ProtoTypeAdapter.Builder}} -->
- **Modifiers**: `public`, `static`
- **Description**: The `Builder` class is a static inner class of `ProtoTypeAdapter` that provides a fluent API for configuring and constructing instances of `ProtoTypeAdapter`. It allows users to specify how enums and field names should be serialized and deserialized, including custom extensions for field and enum value names. The builder supports setting the serialization format for field names, adding custom serialized name extensions, and configuring whether to use the `json_name` field option for serialization.
- **Fields**:
    - `serializedNameExtensions`: `Set<Extension<FieldOptions, String>>` A set of extensions for custom serialized field names.
    - `serializedEnumValueExtensions`: `Set<Extension<EnumValueOptions, String>>` A set of extensions for custom serialized enum value names.
    - `enumSerialization`: `EnumSerialization` Specifies how enum values should be serialized, either by name or number.
    - `protoFormat`: `CaseFormat` The format used for reading proto field names.
    - `jsonFormat`: `CaseFormat` The format used for serializing field names to JSON.
    - `shouldUseJsonNameFieldOption`: `boolean` A flag indicating whether to use the `json_name` field option for serialization.
- **Methods**:
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.Builder`](#BuilderBuilder)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.setEnumSerialization`](#BuildersetEnumSerialization)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.setFieldNameSerializationFormat`](#BuildersetFieldNameSerializationFormat)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.addSerializedNameExtension`](#BuilderaddSerializedNameExtension)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.addSerializedEnumValueExtension`](#BuilderaddSerializedEnumValueExtension)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.setShouldUseJsonNameFieldOption`](#BuildersetShouldUseJsonNameFieldOption)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.build`](#Builderbuild)

**Methods**

---
#### Builder\.Builder<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.Builder.Builder}} -->
The `Builder` constructor initializes a new instance of the `Builder` class with specified enum serialization and field name formats, and sets up default configurations for serialized name extensions and JSON name field options.
- **Modifiers**: `private`
- **Inputs**:
    - `enumSerialization`: An `EnumSerialization` value that determines how enum values should be serialized, either by name or number.
    - `fromFieldNameFormat`: A `CaseFormat` value representing the format of the proto field names to be converted from.
    - `toFieldNameFormat`: A `CaseFormat` value representing the format of the proto field names to be converted to.
- **Control Flow**:
    - Initialize `serializedNameExtensions` as a new `HashSet` to store field options for custom serialized names.
    - Initialize `serializedEnumValueExtensions` as a new `HashSet` to store enum value options for custom serialized values.
    - Call [`setEnumSerialization`](#BuildersetEnumSerialization) method with `enumSerialization` to set the enum serialization strategy.
    - Call [`setFieldNameSerializationFormat`](#BuildersetFieldNameSerializationFormat) method with `fromFieldNameFormat` and `toFieldNameFormat` to set the field name serialization formats.
    - Set `shouldUseJsonNameFieldOption` to `false` as the default configuration.
- **Output**:
    - This constructor does not return any value as it is used to initialize an instance of the `Builder` class.
- **Functions called**:
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.setEnumSerialization`](#BuildersetEnumSerialization)
    - [`com.google.gson.protobuf.ProtoTypeAdapter.Builder.setFieldNameSerializationFormat`](#BuildersetFieldNameSerializationFormat)
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter.Builder`](#ProtoTypeAdapter.Builder)  (Base Class)


---
#### Builder\.setEnumSerialization<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.Builder.setEnumSerialization}} -->
The `setEnumSerialization` method sets the enum serialization strategy for the builder and returns the builder instance.
- **Modifiers**: `public`
- **Inputs**:
    - `enumSerialization`: An instance of `EnumSerialization` that specifies the strategy for serializing enum values, either by their number or name.
- **Control Flow**:
    - The method assigns the provided `enumSerialization` to the builder's `enumSerialization` field after ensuring it is not null using `requireNonNull`.
    - The method then returns the current instance of the `Builder` class.
- **Output**:
    - The method returns the current `Builder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter.Builder`](#ProtoTypeAdapter.Builder)  (Base Class)


---
#### Builder\.setFieldNameSerializationFormat<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.Builder.setFieldNameSerializationFormat}} -->
The `setFieldNameSerializationFormat` method sets the formats for converting field names between proto and JSON representations.
- **Modifiers**: `public`
- **Inputs**:
    - `fromFieldNameFormat`: The `CaseFormat` representing the format of the proto field names to be converted from.
    - `toFieldNameFormat`: The `CaseFormat` representing the format of the JSON field names to be converted to.
- **Control Flow**:
    - Assigns the `fromFieldNameFormat` to the `protoFormat` field of the `Builder` class.
    - Assigns the `toFieldNameFormat` to the `jsonFormat` field of the `Builder` class.
    - Returns the current instance of the `Builder` class.
- **Output**:
    - Returns the current `Builder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter.Builder`](#ProtoTypeAdapter.Builder)  (Base Class)


---
#### Builder\.addSerializedNameExtension<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.Builder.addSerializedNameExtension}} -->
The `addSerializedNameExtension` method adds a serialized name extension to the set of extensions used for customizing field name serialization in a `ProtoTypeAdapter` builder.
- **Modifiers**: `public`
- **Inputs**:
    - `serializedNameExtension`: An `Extension` object of type `FieldOptions` and `String` that specifies a custom serialized name for a proto field.
- **Control Flow**:
    - The method first ensures that the `serializedNameExtension` argument is not null using `requireNonNull`.
    - It then adds the `serializedNameExtension` to the `serializedNameExtensions` set.
    - Finally, it returns the current `Builder` instance to allow for method chaining.
- **Output**:
    - The method returns the current `Builder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter.Builder`](#ProtoTypeAdapter.Builder)  (Base Class)


---
#### Builder\.addSerializedEnumValueExtension<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.Builder.addSerializedEnumValueExtension}} -->
The `addSerializedEnumValueExtension` method adds a given serialized enum value extension to the set of extensions and returns the Builder instance.
- **Modifiers**: `public`
- **Inputs**:
    - `serializedEnumValueExtension`: An `Extension<EnumValueOptions, String>` object representing the serialized enum value extension to be added.
- **Control Flow**:
    - The method calls `requireNonNull` on the `serializedEnumValueExtension` to ensure it is not null.
    - The non-null `serializedEnumValueExtension` is added to the `serializedEnumValueExtensions` set.
    - The method returns the current instance of the `Builder` class.
- **Output**:
    - The method returns the current `Builder` instance, allowing for method chaining.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter.Builder`](#ProtoTypeAdapter.Builder)  (Base Class)


---
#### Builder\.setShouldUseJsonNameFieldOption<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.Builder.setShouldUseJsonNameFieldOption}} -->
The `setShouldUseJsonNameFieldOption` method sets a flag indicating whether to use the `json_name` field option for serialization and returns the Builder instance.
- **Modifiers**: `public`
- **Inputs**:
    - `shouldUseJsonNameFieldOption`: A boolean flag indicating whether the `json_name` field option should be used for serialization.
- **Control Flow**:
    - Assigns the input boolean value to the `shouldUseJsonNameFieldOption` field of the Builder instance.
    - Returns the current Builder instance.
- **Output**:
    - Returns the current Builder instance, allowing for method chaining.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter.Builder`](#ProtoTypeAdapter.Builder)  (Base Class)


---
#### Builder\.build<!-- {{#callable:com.google.gson.protobuf.ProtoTypeAdapter.Builder.build}} -->
The `build` method constructs and returns a new `ProtoTypeAdapter` instance using the current configuration of the `Builder`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method creates a new `ProtoTypeAdapter` object by passing the current state of the `Builder`'s fields as arguments to the `ProtoTypeAdapter` constructor.
    - The fields passed include `enumSerialization`, `protoFormat`, `jsonFormat`, `serializedNameExtensions`, `serializedEnumValueExtensions`, and `shouldUseJsonNameFieldOption`.
    - The method then returns the newly created `ProtoTypeAdapter` instance.
- **Output**:
    - A new instance of `ProtoTypeAdapter` configured with the current state of the `Builder`.
- **See also**: [`com.google.gson.protobuf.ProtoTypeAdapter.Builder`](#ProtoTypeAdapter.Builder)  (Base Class)



