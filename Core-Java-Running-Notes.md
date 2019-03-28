
## Difference b/w Sorted and Ordered collections:
1. Ordered: means you can predict the traversal/access of the data in the data structure/collection like a fifo or lifo.
2. Sorted: a special case of ordering, where the ds in question follows a special ordeing algo. to sort like asc or desc or alphabetical.
3. Sorting dependes upon the type of the data in the ds.
4. If a collection is sorted then it means it is by default ordered.
5. Examples of ordered collections: ArrayList, LinkedList, LinkedHashSet, LinkedHashMap
6. Ex. of sorted collections: TreeSet, TreeMap.
7. Ex, of unordered colelctions: Set, Map

## LinkedHashMap vs HashMap
1. LinkedHashMap is ordered and maintains an insertion order and hence at the same time it will take more memory compared to an HashMap.
2. The LinkedHashMap uses a doubly linked-list to keep track of insertions and hence this will take more memory compared to HashMap.

## Marking constants final and final vs static-final
1. It's a good practice to mark all constants as final.
2. This clearly gives a message to the reader of the code that this field/variable cannot be modified.
3. This encourages type-safety.
4. Some tools like PMD also gives you indications where all fields can be marked as final.
5. And, moreover, it is better to mark final fields as static-final because then there will be only one copy of the final field per class and not per instance.
6. There is ideally no meaning in marking a field final and not static. Because, final means, no changes and it means it should be the same for all instances, so why not explictily mark it static as well?

