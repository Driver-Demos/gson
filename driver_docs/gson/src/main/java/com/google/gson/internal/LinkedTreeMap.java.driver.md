# Purpose
The [`LinkedTreeMap`](#LinkedTreeMapLinkedTreeMap) class is a custom implementation of a map data structure that maintains a collection of key-value pairs, where the keys are comparable. It extends `AbstractMap` and implements `Serializable`, providing a map that preserves the insertion order of elements while also allowing efficient insertion and removal operations. Unlike a standard `TreeMap`, which orders its elements based on their natural ordering or a specified comparator, [`LinkedTreeMap`](#LinkedTreeMapLinkedTreeMap) uses insertion order for iteration, making it similar to a `LinkedHashMap` but with the added benefit of maintaining a balanced tree structure for efficient operations. The class supports null values if specified during instantiation, and it uses a header node to maintain the linked list structure for iteration order.

The class includes several key components: a nested [`Node`](#NodeNode) class representing each entry in the map, methods for adding, removing, and retrieving elements, and mechanisms for maintaining the balance of the tree using AVL rotations. It also provides `EntrySet` and `KeySet` inner classes to support iteration over the map's entries and keys, respectively. The [`LinkedTreeMap`](#LinkedTreeMapLinkedTreeMap) class is designed to be serialized as a `LinkedHashMap` to avoid dependencies on Gson during deserialization, and it explicitly prevents direct deserialization to maintain security. This implementation is part of the internal package of Gson, a popular Java library for converting Java objects to JSON and vice versa, indicating its use in managing JSON data structures efficiently.
# Imports and Dependencies

---
- `com.google.gson.internal`
- `com.google.errorprone.annotations.CanIgnoreReturnValue`
- `java.io.IOException`
- `java.io.InvalidObjectException`
- `java.io.ObjectInputStream`
- `java.io.ObjectStreamException`
- `java.io.Serializable`
- `java.util.AbstractMap`
- `java.util.AbstractSet`
- `java.util.Comparator`
- `java.util.ConcurrentModificationException`
- `java.util.Iterator`
- `java.util.LinkedHashMap`
- `java.util.NoSuchElementException`
- `java.util.Objects`
- `java.util.Set`


# Classes

---
### LinkedTreeMap<!-- {{#class:com.google.gson.internal.LinkedTreeMap}} -->
- **Modifiers**: `public`, `final`
- **Description**: The `LinkedTreeMap` class is a custom implementation of a map that maintains the order of insertion for iteration, similar to a `LinkedHashMap`, but also supports efficient insertion and removal operations using a balanced binary tree structure, akin to a `TreeMap`. It allows for keys to be ordered either naturally or by a provided comparator, and can optionally allow null values. The class is designed to be serializable, though it replaces itself with a `LinkedHashMap` during serialization to avoid dependencies on Gson for deserialization.
- **Fields**:
    - `NATURAL_ORDER`: `Comparator<Comparable>` A static comparator for natural ordering of comparable keys.
    - `comparator`: `Comparator<? super K>` The comparator used to order the keys in the map.
    - `allowNullValues`: `boolean` Indicates whether null values are allowed in the map.
    - `root`: `Node<K, V>` The root node of the tree structure used to store the map entries.
    - `size`: `int` The number of key-value pairs in the map.
    - `modCount`: `int` A count of the number of modifications made to the map, used for fail-fast iteration.
    - `header`: `Node<K, V>` A special node used to maintain the iteration order of the map entries.
    - `entrySet`: `EntrySet` A cached set of the map's entries, used for the entrySet() method.
    - `keySet`: `KeySet` A cached set of the map's keys, used for the keySet() method.
- **Methods**:
    - [`com.google.gson.internal.LinkedTreeMap.compare`](#LinkedTreeMapcompare)
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMap`](#LinkedTreeMapLinkedTreeMap)
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMap`](#LinkedTreeMapLinkedTreeMap)
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMap`](#LinkedTreeMapLinkedTreeMap)
    - [`com.google.gson.internal.LinkedTreeMap.size`](#LinkedTreeMapsize)
    - [`com.google.gson.internal.LinkedTreeMap.get`](#LinkedTreeMapget)
    - [`com.google.gson.internal.LinkedTreeMap.containsKey`](#LinkedTreeMapcontainsKey)
    - [`com.google.gson.internal.LinkedTreeMap.put`](#LinkedTreeMapput)
    - [`com.google.gson.internal.LinkedTreeMap.clear`](#LinkedTreeMapclear)
    - [`com.google.gson.internal.LinkedTreeMap.remove`](#LinkedTreeMapremove)
    - [`com.google.gson.internal.LinkedTreeMap.find`](#LinkedTreeMapfind)
    - [`com.google.gson.internal.LinkedTreeMap.findByObject`](#LinkedTreeMapfindByObject)
    - [`com.google.gson.internal.LinkedTreeMap.findByEntry`](#LinkedTreeMapfindByEntry)
    - [`com.google.gson.internal.LinkedTreeMap.equal`](#LinkedTreeMapequal)
    - [`com.google.gson.internal.LinkedTreeMap.removeInternal`](#LinkedTreeMapremoveInternal)
    - [`com.google.gson.internal.LinkedTreeMap.removeInternalByKey`](#LinkedTreeMapremoveInternalByKey)
    - [`com.google.gson.internal.LinkedTreeMap.replaceInParent`](#LinkedTreeMapreplaceInParent)
    - [`com.google.gson.internal.LinkedTreeMap.rebalance`](#LinkedTreeMaprebalance)
    - [`com.google.gson.internal.LinkedTreeMap.rotateLeft`](#LinkedTreeMaprotateLeft)
    - [`com.google.gson.internal.LinkedTreeMap.rotateRight`](#LinkedTreeMaprotateRight)
    - [`com.google.gson.internal.LinkedTreeMap.entrySet`](#LinkedTreeMapentrySet)
    - [`com.google.gson.internal.LinkedTreeMap.keySet`](#LinkedTreeMapkeySet)
    - [`com.google.gson.internal.LinkedTreeMap.writeReplace`](#LinkedTreeMapwriteReplace)
    - [`com.google.gson.internal.LinkedTreeMap.readObject`](#LinkedTreeMapreadObject)
- **Extends/Implements**:
    - `Serializable`

**Methods**

---
#### LinkedTreeMap\.compare<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.compare}} -->
The `compare` method compares two `Comparable` objects using their natural ordering.
- **Modifiers**: `public`
- **Inputs**:
    - `a`: The first `Comparable` object to be compared.
    - `b`: The second `Comparable` object to be compared.
- **Control Flow**:
    - The method calls the `compareTo` method on the first `Comparable` object `a`, passing the second `Comparable` object `b` as an argument.
- **Output**:
    - An integer result of the comparison, where a negative integer indicates that `a` is less than `b`, zero indicates that `a` is equal to `b`, and a positive integer indicates that `a` is greater than `b`.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.LinkedTreeMap<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.LinkedTreeMap}} -->
The `LinkedTreeMap` constructor initializes a new instance of the `LinkedTreeMap` class with a natural order comparator and allows null values for entries.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The constructor is annotated with `@SuppressWarnings("unchecked")` to suppress warnings about unchecked operations, specifically assuming that the key type `K` is comparable.
    - The constructor calls another constructor of the `LinkedTreeMap` class with two arguments: a natural order comparator and a boolean value `true` to allow null values.
    - The natural order comparator is cast to `Comparator<? super K>` to match the expected type.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.LinkedTreeMap<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.LinkedTreeMap}} -->
The `LinkedTreeMap` constructor initializes a new instance of the `LinkedTreeMap` class with a natural order comparator and a flag indicating whether null values are allowed.
- **Modifiers**: `public`
- **Inputs**:
    - `allowNullValues`: A boolean indicating whether null values are allowed in the map.
- **Control Flow**:
    - The constructor is called with a boolean parameter `allowNullValues`.
    - It invokes another constructor of the `LinkedTreeMap` class, passing a natural order comparator and the `allowNullValues` parameter.
- **Output**:
    - A new instance of the `LinkedTreeMap` class is created with the specified settings.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.LinkedTreeMap<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.LinkedTreeMap}} -->
The `LinkedTreeMap` constructor initializes a new instance of the `LinkedTreeMap` class with a specified comparator and a flag indicating whether null values are allowed.
- **Modifiers**: `public`
- **Inputs**:
    - `comparator`: A `Comparator` object used to order the keys in the map, or `null` to use the natural ordering.
    - `allowNullValues`: A boolean flag indicating whether null values are allowed in the map.
- **Control Flow**:
    - The constructor checks if the provided comparator is not null; if it is null, it defaults to using the `NATURAL_ORDER` comparator.
    - The `allowNullValues` parameter is assigned to the instance variable `allowNullValues`.
    - A new `Node` object is created and assigned to the `header` instance variable, initialized with the `allowNullValues` parameter.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.size<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.size}} -->
The `size` method returns the number of key-value mappings in the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the `size` field, which represents the number of key-value pairs in the map.
- **Output**:
    - The method returns an integer representing the number of entries in the map.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.get<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.get}} -->
The `get` method retrieves the value associated with a given key from the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**:
    - `key`: The key for which the associated value is to be retrieved from the map.
- **Control Flow**:
    - The method calls [`findByObject`](#LinkedTreeMapfindByObject) with the provided key to locate the corresponding node in the map.
    - If a node is found, the method returns the value stored in that node.
    - If no node is found, the method returns `null`.
- **Output**:
    - The method returns the value associated with the specified key, or `null` if the key is not present in the map.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.findByObject`](#LinkedTreeMapfindByObject)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.containsKey<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.containsKey}} -->
The `containsKey` method checks if a specified key exists in the map.
- **Modifiers**: `public`
- **Inputs**:
    - `key`: The key to be checked for existence in the map.
- **Control Flow**:
    - The method calls [`findByObject`](#LinkedTreeMapfindByObject) with the provided key.
    - It checks if the result of [`findByObject`](#LinkedTreeMapfindByObject) is not null.
    - If the result is not null, it returns `true`, indicating the key exists; otherwise, it returns `false`.
- **Output**:
    - A boolean value indicating whether the specified key exists in the map.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.findByObject`](#LinkedTreeMapfindByObject)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.put<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.put}} -->
The `put` method inserts a key-value pair into the map, replacing the existing value if the key already exists, and returns the previous value associated with the key.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `key`: The key to be inserted into the map, which must not be null.
    - `value`: The value to be associated with the key, which must not be null unless null values are allowed.
- **Control Flow**:
    - Check if the key is null and throw a NullPointerException if it is.
    - Check if the value is null and null values are not allowed, then throw a NullPointerException.
    - Call the [`find`](#LinkedTreeMapfind) method with the key and a flag to create a new node if the key does not exist.
    - Store the current value of the found or created node in a variable `result`.
    - Set the value of the found or created node to the new value.
    - Return the previous value stored in `result`.
- **Output**:
    - The method returns the previous value associated with the specified key, or null if there was no mapping for the key.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.find`](#LinkedTreeMapfind)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.clear<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.clear}} -->
The `clear` method resets the LinkedTreeMap by removing all entries and resetting its size and iteration order.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Set the `root` node to `null`, effectively removing all nodes from the tree.
    - Reset the `size` of the map to `0`, indicating that the map is empty.
    - Increment the `modCount` to reflect a structural modification to the map.
    - Reset the iteration order by setting the `header` node's `next` and `prev` pointers to itself, effectively clearing the linked list used for iteration.
- **Output**:
    - The method does not return any value.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.remove<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.remove}} -->
The `remove` method removes a node with the specified key from the map and returns its value.
- **Modifiers**: `public`, `@Override`
- **Inputs**:
    - `key`: The key of the node to be removed from the map.
- **Control Flow**:
    - Call the [`removeInternalByKey`](#LinkedTreeMapremoveInternalByKey) method with the provided key to find and remove the corresponding node from the map.
    - Check if the returned node is not null, indicating that a node was successfully removed.
    - Return the value of the removed node if it exists, otherwise return null.
- **Output**:
    - The value associated with the removed key, or null if the key was not found.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.removeInternalByKey`](#LinkedTreeMapremoveInternalByKey)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.find<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.find}} -->
The `find` method searches for a node with a specified key in the tree, optionally creating it if it doesn't exist.
- **Inputs**:
    - `key`: The key to search for in the tree.
    - `create`: A boolean flag indicating whether to create a new node if the key is not found.
- **Control Flow**:
    - Initialize the comparator and set the nearest node to the root.
    - If the root is not null, determine if the key is comparable and use it to compare with the nearest node's key.
    - If the key matches the nearest node's key, return the nearest node.
    - If the key does not match, traverse the tree to the left or right child based on the comparison result until a null child is found.
    - If the key is not found and `create` is false, return null.
    - If `create` is true, create a new node with the specified key and insert it into the tree.
    - If the tree was empty, set the new node as the root; otherwise, attach it as a left or right child based on the comparison result.
    - Rebalance the tree if necessary, increment the size and modification count, and return the newly created node.
- **Output**:
    - Returns the node with the specified key if found, or the newly created node if `create` is true and the key was not found; otherwise, returns null.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.compare`](#LinkedTreeMapcompare)
    - [`com.google.gson.internal.LinkedTreeMap.rebalance`](#LinkedTreeMaprebalance)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.findByObject<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.findByObject}} -->
The `findByObject` method attempts to locate a node in the map using a given key, returning null if the key is null or not found, or if a ClassCastException occurs.
- **Modifiers**: ``
- **Inputs**:
    - `key`: An Object representing the key to search for in the map.
- **Control Flow**:
    - The method first checks if the key is not null.
    - If the key is not null, it attempts to find the node by casting the key to type K and calling the [`find`](#LinkedTreeMapfind) method with `create` set to false.
    - If the key is null, the method immediately returns null.
    - If a ClassCastException is thrown during the casting or finding process, the method catches the exception and returns null.
- **Output**:
    - The method returns a `Node<K, V>` if the key is found and valid, otherwise it returns null.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.find`](#LinkedTreeMapfind)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.findByEntry<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.findByEntry}} -->
The `findByEntry` method retrieves a node from the map that matches the key and value of a given entry, or returns null if no such node exists.
- **Inputs**:
    - `entry`: An `Entry<?, ?>` object representing the key-value pair to be searched for in the map.
- **Control Flow**:
    - The method calls [`findByObject`](#LinkedTreeMapfindByObject) with the key from the provided entry to locate a node in the map.
    - It checks if the found node is not null and if its value equals the value of the provided entry using the [`equal`](#LinkedTreeMapequal) method.
    - If both conditions are true, it returns the found node; otherwise, it returns null.
- **Output**:
    - Returns a `Node<K, V>` that matches the key and value of the provided entry, or null if no such node exists.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.findByObject`](#LinkedTreeMapfindByObject)
    - [`com.google.gson.internal.LinkedTreeMap.Node.getKey`](#NodegetKey)
    - [`com.google.gson.internal.LinkedTreeMap.equal`](#LinkedTreeMapequal)
    - [`com.google.gson.internal.LinkedTreeMap.Node.getValue`](#NodegetValue)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.equal<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.equal}} -->
The `equal` method checks if two objects are equal using `Objects.equals`.
- **Modifiers**: `private`, `static`
- **Inputs**:
    - `a`: The first object to be compared.
    - `b`: The second object to be compared.
- **Control Flow**:
    - The method uses `Objects.equals(a, b)` to determine if the two objects are equal.
- **Output**:
    - A boolean value indicating whether the two objects are equal.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.removeInternal<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.removeInternal}} -->
The `removeInternal` method removes a specified node from the tree, rearranging the tree's structure as necessary and optionally unlinking it from the iteration linked list.
- **Inputs**:
    - `node`: The node to be removed from the tree.
    - `unlink`: A boolean flag indicating whether the node should also be unlinked from the iteration linked list.
- **Control Flow**:
    - If `unlink` is true, the method updates the `prev` and `next` pointers of the node's neighbors to remove the node from the linked list.
    - The method checks if the node has both left and right children.
    - If both children exist, it finds an adjacent node (either the last node of the left subtree or the first node of the right subtree) to replace the current node.
    - The method recursively calls `removeInternal` on the adjacent node to remove it from its current position.
    - The method updates the left and right children of the adjacent node to be the children of the node being removed, adjusting parent pointers accordingly.
    - The height of the adjacent node is updated based on its new children, and it replaces the node in the parent.
    - If only one child exists, the method replaces the node with its single child in the parent.
    - If no children exist, the method simply removes the node from the parent.
    - The method calls [`rebalance`](#LinkedTreeMaprebalance) on the original parent to ensure the tree remains balanced.
    - The size of the tree is decremented and the modification count is incremented.
- **Output**:
    - The method does not return a value; it modifies the tree structure in place.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.Node.last`](#Nodelast)
    - [`com.google.gson.internal.LinkedTreeMap.Node.first`](#Nodefirst)
    - [`com.google.gson.internal.LinkedTreeMap.replaceInParent`](#LinkedTreeMapreplaceInParent)
    - [`com.google.gson.internal.LinkedTreeMap.rebalance`](#LinkedTreeMaprebalance)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.removeInternalByKey<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.removeInternalByKey}} -->
The `removeInternalByKey` method removes a node from the tree map based on the provided key and returns the removed node.
- **Modifiers**: ``
- **Inputs**:
    - `key`: The key of the node to be removed from the tree map.
- **Control Flow**:
    - Call [`findByObject`](#LinkedTreeMapfindByObject) with the provided key to locate the node in the tree map.
    - If the node is found (i.e., not null), call [`removeInternal`](#LinkedTreeMapremoveInternal) to remove the node from the tree map and unlink it from the iteration linked list.
    - Return the node that was removed, or null if no node was found.
- **Output**:
    - Returns the node that was removed from the tree map, or null if no node with the specified key was found.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.findByObject`](#LinkedTreeMapfindByObject)
    - [`com.google.gson.internal.LinkedTreeMap.removeInternal`](#LinkedTreeMapremoveInternal)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.replaceInParent<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.replaceInParent}} -->
The `replaceInParent` method replaces a given node in the tree with a replacement node, updating parent-child relationships accordingly.
- **Modifiers**: `private`
- **Inputs**:
    - `node`: The node to be replaced in the tree.
    - `replacement`: The node that will replace the original node, or null if the node is to be removed without replacement.
- **Control Flow**:
    - Retrieve the parent of the node to be replaced and set the node's parent to null.
    - If the replacement node is not null, set its parent to the parent of the node being replaced.
    - If the parent of the node is not null, determine if the node is the left or right child and replace it with the replacement node accordingly.
    - If the parent is null, set the root of the tree to the replacement node.
- **Output**:
    - The method does not return any value; it modifies the tree structure in place.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.rebalance<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.rebalance}} -->
The `rebalance` method adjusts the tree structure to maintain AVL balance after an insertion or removal operation.
- **Modifiers**: `private`
- **Inputs**:
    - `unbalanced`: The node from which rebalancing should start, typically the node that became unbalanced due to an insertion or removal.
    - `insert`: A boolean flag indicating whether the imbalance was caused by an insertion (true) or a removal (false).
- **Control Flow**:
    - The method iterates from the unbalanced node up to the root of the tree, checking the balance factor (delta) of each node.
    - If the balance factor is -2, indicating a right-heavy imbalance, it checks the balance of the right child to determine if a single left rotation or a right-left rotation is needed.
    - If the balance factor is 2, indicating a left-heavy imbalance, it checks the balance of the left child to determine if a single right rotation or a left-right rotation is needed.
    - If the balance factor is 0, it updates the node's height and breaks if the imbalance was caused by an insertion, as no further rebalancing is needed.
    - If the balance factor is -1 or 1, it updates the node's height and breaks if the imbalance was caused by a removal, as no further rebalancing is needed.
- **Output**:
    - The method does not return a value; it modifies the tree structure in place to ensure it remains balanced.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.rotateLeft`](#LinkedTreeMaprotateLeft)
    - [`com.google.gson.internal.LinkedTreeMap.rotateRight`](#LinkedTreeMaprotateRight)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.rotateLeft<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.rotateLeft}} -->
The `rotateLeft` method performs a left rotation on a subtree rooted at the given node to maintain AVL tree balance.
- **Modifiers**: `private`
- **Inputs**:
    - `root`: The root node of the subtree to be rotated left.
- **Control Flow**:
    - Initialize local variables for the left child of the root, the pivot (right child of the root), and the left and right children of the pivot.
    - Assign the pivot's left child to the root's right child and update the parent of the pivot's left child if it is not null.
    - Replace the root node with the pivot node in the parent node's reference.
    - Assign the root node to the pivot's left child and update the root's parent to the pivot.
    - Update the height of the root node based on the heights of its children.
    - Update the height of the pivot node based on the heights of its children.
- **Output**:
    - The method does not return a value; it modifies the tree structure in place.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.replaceInParent`](#LinkedTreeMapreplaceInParent)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.rotateRight<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.rotateRight}} -->
The `rotateRight` method performs a right rotation on a subtree rooted at the given node to maintain balance in a binary search tree.
- **Modifiers**: `private`
- **Inputs**:
    - `root`: The root node of the subtree to be rotated right.
- **Control Flow**:
    - Initialize `pivot` as the left child of `root`, `right` as the right child of `root`, `pivotLeft` as the left child of `pivot`, and `pivotRight` as the right child of `pivot`.
    - Assign `pivotRight` to `root.left` and update `pivotRight.parent` to `root` if `pivotRight` is not null.
    - Call [`replaceInParent`](#LinkedTreeMapreplaceInParent) to replace `root` with `pivot` in the parent node.
    - Assign `root` to `pivot.right` and update `root.parent` to `pivot`.
    - Update the height of `root` using the maximum height of its children plus one.
    - Update the height of `pivot` using the maximum height of its children plus one.
- **Output**:
    - The method does not return a value; it modifies the tree structure by rotating the nodes.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.replaceInParent`](#LinkedTreeMapreplaceInParent)
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.entrySet<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.entrySet}} -->
The `entrySet` method returns a set view of the mappings contained in the map, initializing the set if it hasn't been created yet.
- **Modifiers**: `public`, `@Override`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the current `entrySet` instance stored in the `entrySet` field.
    - Check if the `entrySet` is `null`.
    - If `entrySet` is `null`, create a new `EntrySet` instance and assign it to the `entrySet` field.
    - Return the `entrySet` instance.
- **Output**:
    - A `Set` of `Entry<K, V>` representing the mappings contained in the map.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.keySet<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.keySet}} -->
The `keySet` method returns a set view of the keys contained in the map.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method checks if the `keySet` field is null.
    - If `keySet` is null, it initializes it with a new instance of `KeySet`.
    - The method returns the `keySet` instance.
- **Output**:
    - A `Set<K>` representing the keys in the map.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.writeReplace<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.writeReplace}} -->
The `writeReplace` method returns a `LinkedHashMap` representation of the current `LinkedTreeMap` instance for serialization purposes.
- **Modifiers**: `private`
- **Inputs**: None
- **Control Flow**:
    - The method creates a new `LinkedHashMap` instance using the current `LinkedTreeMap` instance (`this`) as the source.
    - The method returns the newly created `LinkedHashMap` instance.
- **Output**:
    - An `Object` that is a `LinkedHashMap` containing the same entries as the current `LinkedTreeMap` instance.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)


---
#### LinkedTreeMap\.readObject<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.readObject}} -->
The `readObject` method prevents the deserialization of the `LinkedTreeMap` class by throwing an `InvalidObjectException`.
- **Modifiers**: `private`
- **Inputs**:
    - `in`: An `ObjectInputStream` from which the object is supposed to be deserialized.
- **Control Flow**:
    - The method immediately throws an `InvalidObjectException` with the message 'Deserialization is unsupported'.
- **Output**:
    - The method does not return any value as it always throws an exception.
- **See also**: [`com.google.gson.internal.LinkedTreeMap`](#LinkedTreeMap)  (Base Class)



---
### Node<!-- {{#class:com.google.gson.internal.LinkedTreeMap.Node}} -->
- **Modifiers**: `static`, `final`
- **Description**: The `Node` class is a static final inner class within the `LinkedTreeMap` class, implementing the `Entry` interface, and represents a node in a binary tree structure used to store key-value pairs. It supports operations such as getting and setting values, checking equality, and computing hash codes. The class also manages tree structure by maintaining references to parent, left, right, next, and previous nodes, and includes methods to find the first and last nodes in a subtree.
- **Fields**:
    - `parent`: `Node<K, V>` Reference to the parent node in the tree.
    - `left`: `Node<K, V>` Reference to the left child node in the tree.
    - `right`: `Node<K, V>` Reference to the right child node in the tree.
    - `next`: `Node<K, V>` Reference to the next node in the linked list for iteration.
    - `prev`: `Node<K, V>` Reference to the previous node in the linked list for iteration.
    - `key`: `K` The key associated with this node, which is final and cannot be changed.
    - `allowNullValue`: `boolean` Indicates whether null values are allowed for this node.
    - `value`: `V` The value associated with this node, which can be changed.
    - `height`: `int` The height of the node in the tree, used for balancing purposes.
- **Methods**:
    - [`com.google.gson.internal.LinkedTreeMap.Node.Node`](#NodeNode)
    - [`com.google.gson.internal.LinkedTreeMap.Node.Node`](#NodeNode)
    - [`com.google.gson.internal.LinkedTreeMap.Node.getKey`](#NodegetKey)
    - [`com.google.gson.internal.LinkedTreeMap.Node.getValue`](#NodegetValue)
    - [`com.google.gson.internal.LinkedTreeMap.Node.setValue`](#NodesetValue)
    - [`com.google.gson.internal.LinkedTreeMap.Node.equals`](#Nodeequals)
    - [`com.google.gson.internal.LinkedTreeMap.Node.hashCode`](#NodehashCode)
    - [`com.google.gson.internal.LinkedTreeMap.Node.toString`](#NodetoString)
    - [`com.google.gson.internal.LinkedTreeMap.Node.first`](#Nodefirst)
    - [`com.google.gson.internal.LinkedTreeMap.Node.last`](#Nodelast)

**Methods**

---
#### Node\.Node<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.Node}} -->
The `Node` constructor initializes a new node with a null key, sets the `allowNullValue` flag, and links the node to itself for both next and previous references.
- **Inputs**:
    - `allowNullValue`: A boolean indicating whether null values are allowed for this node.
- **Control Flow**:
    - Set the `key` field to `null`.
    - Assign the `allowNullValue` parameter to the `allowNullValue` field of the node.
    - Set the `next` and `prev` fields to point to the node itself, creating a self-referential link.
- **Output**:
    - The constructor does not return a value as it is used to initialize a new instance of the `Node` class.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.Node<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.Node}} -->
The `Node` constructor initializes a new node in a doubly-linked list with specified parent, key, and neighboring nodes, and updates the links of the previous and next nodes to include this new node.
- **Inputs**:
    - `allowNullValue`: A boolean indicating whether null values are allowed for this node.
    - `parent`: The parent node of this node in the tree structure.
    - `key`: The key associated with this node.
    - `next`: The next node in the linked list sequence.
    - `prev`: The previous node in the linked list sequence.
- **Control Flow**:
    - Assigns the provided parent node to the `parent` field of the new node.
    - Assigns the provided key to the `key` field of the new node.
    - Sets the `allowNullValue` field to the provided boolean value.
    - Initializes the `height` field of the node to 1.
    - Assigns the provided next node to the `next` field of the new node.
    - Assigns the provided previous node to the `prev` field of the new node.
    - Updates the `next` field of the previous node to point to this new node.
    - Updates the `prev` field of the next node to point to this new node.
- **Output**:
    - The method does not return any value as it is a constructor.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.getKey<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.getKey}} -->
The `getKey` method returns the key associated with a node in the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `key` field of the `Node` class.
- **Output**:
    - The method returns an object of type `K`, which is the key of the node.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.getValue<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.getValue}} -->
The `getValue` method returns the value associated with a node in the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the `value` field of the node.
- **Output**:
    - The method returns the value of type `V` associated with the node.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.setValue<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.setValue}} -->
The `setValue` method updates the value of a node and returns the old value, throwing an exception if the new value is null and null values are not allowed.
- **Modifiers**: `public`
- **Inputs**:
    - `value`: The new value to be set for the node.
- **Control Flow**:
    - Check if the provided value is null and if null values are not allowed, throw a NullPointerException.
    - Store the current value of the node in a variable `oldValue`.
    - Set the node's value to the new provided value.
    - Return the `oldValue`.
- **Output**:
    - The method returns the old value of the node before it was updated.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.equals<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.equals}} -->
The [`equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals) method checks if the current `Entry` object is equal to another object by comparing their keys and values.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: An object to compare with the current `Entry` object.
- **Control Flow**:
    - Check if the input object `o` is an instance of `Entry`.
    - If `o` is an instance of `Entry`, cast it to `Entry<?, ?>` and store it in `other`.
    - Compare the current `Entry`'s key with `other`'s key using [`equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals), handling `null` values appropriately.
    - Compare the current `Entry`'s value with `other`'s value using [`equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals), handling `null` values appropriately.
    - Return `true` if both key and value comparisons are true, otherwise return `false`.
    - If `o` is not an instance of `Entry`, return `false`.
- **Output**:
    - A boolean value indicating whether the current `Entry` object is equal to the input object `o`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.Node.getKey`](#NodegetKey)
    - [`com.google.gson.internal.NonNullElementWrapperList.equals`](NonNullElementWrapperList.java.driver.md#NonNullElementWrapperListequals)
    - [`com.google.gson.internal.LinkedTreeMap.Node.getValue`](#NodegetValue)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.hashCode<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.hashCode}} -->
The `hashCode` method computes a hash code for a node based on its key and value.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method checks if the `key` is `null`; if so, it assigns 0, otherwise it uses the `hashCode` of the `key`.
    - Similarly, it checks if the `value` is `null`; if so, it assigns 0, otherwise it uses the `hashCode` of the `value`.
    - The method returns the result of a bitwise XOR operation between the hash codes of the `key` and `value`.
- **Output**:
    - An integer representing the hash code of the node, calculated using the key and value.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.toString<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.toString}} -->
The `toString` method returns a string representation of a node in the format 'key=value'.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method concatenates the `key` and `value` fields of the `Node` class with an '=' sign in between.
    - It returns the resulting string.
- **Output**:
    - A `String` that represents the node in the format 'key=value'.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.first<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.first}} -->
The `first` method returns the leftmost node in the subtree rooted at the current node.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize `node` to `this` (the current node).
    - Set `child` to the left child of `node`.
    - Enter a loop that continues as long as `child` is not null.
    - Inside the loop, set `node` to `child` and update `child` to the left child of the new `node`.
    - Exit the loop when `child` is null, indicating that `node` is the leftmost node.
    - Return `node`.
- **Output**:
    - The method returns a `Node<K, V>` which is the leftmost node in the subtree.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)


---
#### Node\.last<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.Node.last}} -->
The `last` method returns the last node in the subtree rooted at the current node by traversing the right children.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - Initialize `node` to `this` (the current node).
    - Set `child` to the right child of `node`.
    - While `child` is not null, update `node` to `child` and set `child` to the right child of `node`.
    - Return `node`, which is the last node in the rightmost path of the subtree.
- **Output**:
    - The method returns a `Node<K, V>` which is the last node in the rightmost path of the subtree.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.Node`](#LinkedTreeMap.Node)  (Base Class)



---
### LinkedTreeMapIterator<!-- {{#class:com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator}} -->
- **Modifiers**: `private`, `abstract`
- **Description**: The `LinkedTreeMapIterator` is an abstract class that provides a skeletal implementation of an iterator for the `LinkedTreeMap` class, allowing traversal of the map's nodes in insertion order while ensuring concurrent modification safety.
- **Fields**:
    - `next`: `Node<K, V>` The next node to be returned by the iterator.
    - `lastReturned`: `Node<K, V>` The last node returned by the iterator, used for removal operations.
    - `expectedModCount`: `int` The expected modification count to detect concurrent modifications.
- **Methods**:
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.LinkedTreeMapIterator`](#LinkedTreeMapLinkedTreeMapIterator.LinkedTreeMapIterator)
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.hasNext`](#LinkedTreeMapLinkedTreeMapIterator.hasNext)
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.nextNode`](#LinkedTreeMapLinkedTreeMapIterator.nextNode)
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.remove`](#LinkedTreeMapLinkedTreeMapIterator.remove)

**Methods**

---
#### LinkedTreeMapIterator\.LinkedTreeMapIterator<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.LinkedTreeMapIterator}} -->
The `LinkedTreeMapIterator` constructor initializes an iterator for the `LinkedTreeMap` class.
- **Inputs**: None
- **Control Flow**:
    - The constructor is empty and does not perform any operations.
- **Output**:
    - There is no output as the constructor does not return any value.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator`](#LinkedTreeMap.LinkedTreeMapIterator)  (Base Class)


---
#### LinkedTreeMapIterator\.hasNext<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.hasNext}} -->
The `hasNext` method checks if there are more elements to iterate over in the linked list structure of the map.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - The method compares the `next` node with the `header` node using reference equality.
    - If `next` is not equal to `header`, it returns `true`, indicating there are more elements to iterate.
    - If `next` is equal to `header`, it returns `false`, indicating the end of the iteration.
- **Output**:
    - A boolean value indicating whether there are more elements to iterate over.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator`](#LinkedTreeMap.LinkedTreeMapIterator)  (Base Class)


---
#### LinkedTreeMapIterator\.nextNode<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.nextNode}} -->
The `nextNode` method retrieves the next node in the iteration sequence, ensuring the iteration is valid and consistent with the map's current state.
- **Modifiers**: `final`
- **Inputs**: None
- **Control Flow**:
    - Retrieve the next node in the sequence and assign it to variable `e`.
    - Check if `e` is the header node, and if so, throw a `NoSuchElementException` indicating there are no more elements to iterate over.
    - Verify that the current modification count (`modCount`) matches the expected modification count (`expectedModCount`); if not, throw a `ConcurrentModificationException` to indicate that the map has been modified during iteration.
    - Update the `next` pointer to the next node in the sequence (`e.next`).
    - Set `lastReturned` to the current node `e`.
    - Return the current node `e`.
- **Output**:
    - Returns the next `Node<K, V>` in the iteration sequence.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator`](#LinkedTreeMap.LinkedTreeMapIterator)  (Base Class)


---
#### LinkedTreeMapIterator\.remove<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.remove}} -->
The `remove` method removes the last returned element from the iteration and updates the expected modification count.
- **Modifiers**: `public`, `final`
- **Inputs**: None
- **Control Flow**:
    - Check if `lastReturned` is null; if so, throw an `IllegalStateException`.
    - Call [`removeInternal`](#LinkedTreeMapremoveInternal) with `lastReturned` and `true` to remove the node and unlink it from the iteration list.
    - Set `lastReturned` to null to indicate that the last returned element has been removed.
    - Update `expectedModCount` to match `modCount` to reflect the current state of the map.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.removeInternal`](#LinkedTreeMapremoveInternal)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator`](#LinkedTreeMap.LinkedTreeMapIterator)  (Base Class)



---
### EntrySet<!-- {{#class:com.google.gson.internal.LinkedTreeMap.EntrySet}} -->
- **Description**: The `EntrySet` class is a specialized implementation of `AbstractSet` that represents a set of map entries for the `LinkedTreeMap` class, providing methods to iterate over, check for containment, remove, and clear entries in the map.
- **Methods**:
    - [`com.google.gson.internal.LinkedTreeMap.EntrySet.size`](#EntrySetsize)
    - [`com.google.gson.internal.LinkedTreeMap.EntrySet.iterator`](#EntrySetiterator)
    - [`com.google.gson.internal.LinkedTreeMap.EntrySet.contains`](#EntrySetcontains)
    - [`com.google.gson.internal.LinkedTreeMap.EntrySet.remove`](#EntrySetremove)
    - [`com.google.gson.internal.LinkedTreeMap.EntrySet.clear`](#EntrySetclear)

**Methods**

---
#### EntrySet\.size<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.EntrySet.size}} -->
The `size` method returns the number of key-value mappings in the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the `size` field, which represents the number of key-value pairs in the map.
- **Output**:
    - An integer representing the number of key-value mappings in the map.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.EntrySet`](#LinkedTreeMap.EntrySet)  (Base Class)


---
#### EntrySet\.iterator<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.EntrySet.iterator}} -->
The `iterator` method returns an iterator for the entries in the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method returns a new instance of an anonymous subclass of `LinkedTreeMapIterator` that is parameterized with `Entry<K, V>`.
    - The `next` method of this iterator is overridden to return the next node in the map by calling `nextNode()`.
- **Output**:
    - An `Iterator<Entry<K, V>>` for iterating over the map's entries.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.nextNode`](#LinkedTreeMapLinkedTreeMapIterator.nextNode)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.EntrySet`](#LinkedTreeMap.EntrySet)  (Base Class)


---
#### EntrySet\.contains<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.EntrySet.contains}} -->
The `contains` method checks if a given object is an entry in the map by verifying its type and searching for it using the [`findByEntry`](#LinkedTreeMapfindByEntry) method.
- **Modifiers**: `public`
- **Inputs**:
    - `o`: The object to be checked if it is contained in the map, expected to be an instance of `Entry`.
- **Control Flow**:
    - The method first checks if the input object `o` is an instance of `Entry`.
    - If `o` is an instance of `Entry`, it casts `o` to `Entry<?, ?>` and calls the [`findByEntry`](#LinkedTreeMapfindByEntry) method with this casted entry.
    - The method returns `true` if [`findByEntry`](#LinkedTreeMapfindByEntry) returns a non-null value, indicating the entry is present in the map; otherwise, it returns `false`.
- **Output**:
    - A boolean value indicating whether the specified object is an entry in the map.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.findByEntry`](#LinkedTreeMapfindByEntry)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.EntrySet`](#LinkedTreeMap.EntrySet)  (Base Class)


---
#### EntrySet\.remove<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.EntrySet.remove}} -->
The `remove` method attempts to remove an entry from the map if it matches the given object and returns a boolean indicating success.
- **Modifiers**: `public`, `boolean`
- **Inputs**:
    - `o`: The object to be removed, expected to be an instance of Entry.
- **Control Flow**:
    - Check if the input object `o` is an instance of `Entry`; if not, return `false`.
    - Use [`findByEntry`](#LinkedTreeMapfindByEntry) to locate the node corresponding to the entry `o`; if not found, return `false`.
    - Call [`removeInternal`](#LinkedTreeMapremoveInternal) to remove the node from the map and return `true`.
- **Output**:
    - A boolean value indicating whether the entry was successfully removed (`true`) or not (`false`).
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.findByEntry`](#LinkedTreeMapfindByEntry)
    - [`com.google.gson.internal.LinkedTreeMap.removeInternal`](#LinkedTreeMapremoveInternal)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.EntrySet`](#LinkedTreeMap.EntrySet)  (Base Class)


---
#### EntrySet\.clear<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.EntrySet.clear}} -->
The [`clear`](#LinkedTreeMapclear) method removes all entries from the `LinkedTreeMap`, resetting its size and iteration order.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method sets the `root` of the `LinkedTreeMap` to `null`, effectively removing all nodes from the tree.
    - It resets the `size` of the map to `0`, indicating that the map is now empty.
    - The `modCount` is incremented to reflect the structural modification of the map.
    - The iteration order is cleared by setting the `header` node's `next` and `prev` pointers to itself, maintaining the circular linked list structure.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.clear`](#LinkedTreeMapclear)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.EntrySet`](#LinkedTreeMap.EntrySet)  (Base Class)



---
### KeySet<!-- {{#class:com.google.gson.internal.LinkedTreeMap.KeySet}} -->
- **Modifiers**: `final`
- **Description**: The `KeySet` class is a specialized implementation of `AbstractSet` that represents the set of keys in a `LinkedTreeMap`, providing methods to access, iterate, and manipulate the keys within the map.
- **Methods**:
    - [`com.google.gson.internal.LinkedTreeMap.KeySet.size`](#KeySetsize)
    - [`com.google.gson.internal.LinkedTreeMap.KeySet.iterator`](#KeySetiterator)
    - [`com.google.gson.internal.LinkedTreeMap.KeySet.contains`](#KeySetcontains)
    - [`com.google.gson.internal.LinkedTreeMap.KeySet.remove`](#KeySetremove)
    - [`com.google.gson.internal.LinkedTreeMap.KeySet.clear`](#KeySetclear)

**Methods**

---
#### KeySet\.size<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.KeySet.size}} -->
The `size` method returns the number of key-value mappings in the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method directly returns the value of the `size` field, which represents the number of key-value pairs in the map.
- **Output**:
    - The method returns an integer representing the number of entries in the map.
- **See also**: [`com.google.gson.internal.LinkedTreeMap.KeySet`](#LinkedTreeMap.KeySet)  (Base Class)


---
#### KeySet\.iterator<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.KeySet.iterator}} -->
The `iterator` method returns an iterator over the keys of the `LinkedTreeMap`.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method returns a new instance of an anonymous subclass of `LinkedTreeMapIterator<K>`.
    - The `next` method of this iterator is overridden to return the key of the next node in the map.
- **Output**:
    - An `Iterator<K>` that iterates over the keys of the `LinkedTreeMap`.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.LinkedTreeMapIterator.nextNode`](#LinkedTreeMapLinkedTreeMapIterator.nextNode)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.KeySet`](#LinkedTreeMap.KeySet)  (Base Class)


---
#### KeySet\.contains<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.KeySet.contains}} -->
The `contains` method checks if a specified object is a key in the map.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `o`: The object to check for presence as a key in the map.
- **Control Flow**:
    - The method calls [`containsKey`](#LinkedTreeMapcontainsKey) with the provided object `o`.
    - It returns the result of the [`containsKey`](#LinkedTreeMapcontainsKey) method, which checks if the object is a key in the map.
- **Output**:
    - A boolean value indicating whether the specified object is a key in the map.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.containsKey`](#LinkedTreeMapcontainsKey)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.KeySet`](#LinkedTreeMap.KeySet)  (Base Class)


---
#### KeySet\.remove<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.KeySet.remove}} -->
The `remove` method removes a node with the specified key from the map and returns the value of the removed node.
- **Modifiers**: `public`, `override`
- **Inputs**:
    - `key`: The key of the node to be removed from the map.
- **Control Flow**:
    - The method calls [`removeInternalByKey`](#LinkedTreeMapremoveInternalByKey) with the provided key to find and remove the node associated with that key.
    - It checks if the result of [`removeInternalByKey`](#LinkedTreeMapremoveInternalByKey) is not null, indicating that a node was successfully removed.
- **Output**:
    - Returns the value of the removed node if it was found and removed, otherwise returns null.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.removeInternalByKey`](#LinkedTreeMapremoveInternalByKey)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.KeySet`](#LinkedTreeMap.KeySet)  (Base Class)


---
#### KeySet\.clear<!-- {{#callable:com.google.gson.internal.LinkedTreeMap.KeySet.clear}} -->
The [`clear`](#LinkedTreeMapclear) method removes all entries from the `LinkedTreeMap`, resetting its size and iteration order.
- **Modifiers**: `public`
- **Inputs**: None
- **Control Flow**:
    - The method calls the [`clear`](#LinkedTreeMapclear) method of the enclosing `LinkedTreeMap` instance.
    - This sets the `root` to `null`, resets the `size` to 0, and increments the `modCount`.
    - It also resets the iteration order by setting the `header` node's `next` and `prev` pointers to itself.
- **Output**:
    - The method does not return any value.
- **Functions called**:
    - [`com.google.gson.internal.LinkedTreeMap.clear`](#LinkedTreeMapclear)
- **See also**: [`com.google.gson.internal.LinkedTreeMap.KeySet`](#LinkedTreeMap.KeySet)  (Base Class)



