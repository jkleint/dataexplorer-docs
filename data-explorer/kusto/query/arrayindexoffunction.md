---
title: array_index_of() - Azure Data Explorer
description: This article describes array_index_of() in Azure Data Explorer.
services: data-explorer
author: orspod
ms.author: orspodek
ms.reviewer: alexans
ms.service: data-explorer
ms.topic: reference
ms.date: 01/22/2020
---
# array_index_of()

Searches the array for the specified item, and returns its position.

## Syntax

`array_index_of(`*array*,*lookup*`)`

## Arguments

* *array*: Input array to search.
* *lookup*: Value to lookup. The value should be of type long, integer, double, datetime, timespan, decimal, string, or guid.
* *start_index*: Search start position. Optional.
* *length*: Number of values to examine. A value of -1 means unlimited length. Optional.
* *occurrence*: The number of the occurrence. Default 1. Optional.

## Returns

Zero-based index position of lookup.
Returns -1 if the value isn't found in the array.

For irrelevant inputs (*start_index* < 0, *occurrence* < 0 or  *length* < -1) - returns *null*.

## Example

```
let arr=dynamic(["this", "is", "an", "example", "an", "example"]);
print
 idx1 = array_index_of(arr,"an")    // lookup found in input string
 , idx2 = array_index_of(arr,"example",1,3) // lookup found in researched range 
 , idx3 = array_index_of(arr,"example",1,2) // search starts from index 1, but stops after 2 values, so lookup can't be found
 , idx4 = array_index_of(arr,"is",2,4) // search starts after occurrence of lookup
 , idx5 = array_index_of(arr,"example",2,-1)  // lookup found
 , idx6 = array_index_of(arr, "an", 1, -1, 2)   // second occurrence found in input range
 , idx7 = array_index_of(arr, "an", 1, -1, 3)   // no third occurrence in input array
```

|idx1|idx2|idx3|idx4|idx5|idx6|idx7|
|----|----|----|----|----|----|----|
|2   |3   |-1  |-1   |3   |4   |-1  |

## See also

If you only want to check whether a value exists in an array,
but you are not interested in its position, you can use
[set_has_element(`arr`, `value`)](sethaselementfunction.md). This function will improve the readability of your query. Both functions have the same performance.
