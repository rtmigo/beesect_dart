![Generic badge](https://img.shields.io/badge/status-it_works-ok.svg)
[![Pub Package](https://img.shields.io/pub/v/bisection.svg)](https://pub.dev/packages/bisection)
[![pub points](https://badges.bar/bisection/pub%20points)](https://pub.dev/packages/bisection/score)
![Generic badge](https://img.shields.io/badge/testing_on-Windows_|_Linux-blue.svg)
![Generic badge](https://img.shields.io/badge/testing_on-VM_|_Node_|_Chrome-blue.svg)

# [bisection](https://github.com/rtmigo/bisection_dart)

Library for searching in sorted lists and adding elements to sorted lists while
maintaining the order of the elements.

Port of the Python [bisect](https://docs.python.org/3/library/bisect.html) with
[search functions](https://docs.python.org/3/library/bisect.html#searching-sorted-lists)
.

## Use bisect functions

```dart
import 'package:bisection/bisect.dart';

void main() {
  // The list must be sorted
  final arr = ['A', 'B', 'C', 'E'];

  // Find the index of an item in a sorted list
  print(bisect(arr, 'B')); // 2

  // Find the future index for a non-existent item
  print(bisect_left(arr, 'D')); // 3

  // Add an item to the list while keeping the list sorted
  insort(arr, 'D');
  print(arr); // [A, B, C, D, E]

  // Find leftmost value greater than 'B'
  print(find_gt(arr, 'B')); // C
}
```

## Use list extensions

```dart
import 'package:bisection/extension.dart';

void main() {
  // The list must be sorted
  final arr = ['A', 'B', 'C', 'E'];

  // Find the index of an item in a sorted list
  print(arr.bisectRight('B'));  // 2

  // Find the future index for a non-existent item
  print(arr.bisectLeft('D'));  // 3

  // Add an item to the list while keeping the list sorted
  arr.insortRight('D');
  print(arr);  // [A, B, C, D, E]

  // Locate leftmost value greater than 'B'
  print(arr.bsearchGreaterThan('B'));  // 2
}
```

Python `bisect`        | Dart `bisection` extension methods
-----------------------|--------------------------------------
`bisect(arr, x)`       | `arr.bisectRight(x)`
`bisect_left(arr, x)`  | `arr.bisectLeft(x)`
`bisect_right(arr, x)` | `arr.bisectRight(x)`
`insort(arr, x)`       | `arr.insortRight(x)`
`insort_left(arr, x)`  | `arr.insortLeft(x)`
`insort_right(arr, x)` | `arr.insortRight(x)`
`index(arr, x)`        | `arr[arr.bsearch(x)]]`
`find_lt(arr, x)`      | `arr[arr.bsearchLessThan(x)]`
`find_le(arr, x)`      | `arr[arr.bsearchLessThanOrEqualTo(x)]`
`find_gt(arr, x)`      | `arr[arr.bsearchGreaterThan(x)]`
`find_ge(arr, x)`      | `arr[arr.bsearchGreaterThanOrEqualTo(x)]`

## Differences from Python bisect

The library is written with the intention of repeating the results of Python
functions as accurately as possible. The consistency of the results is
by [Dart unit tests](https://github.com/rtmigo/bisection_dart/blob/dev/test/generated/bisect_test.dart)
, generated
by [Python scripts](https://github.com/rtmigo/bisection_dart/tree/dev/test/generators)
.

The only difference is that this library does not accept negative values of the
`hi` argument. If the value is negative, an exception will be thrown. In the case
of Python, a rather mysterious value would be returned.
