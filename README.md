# [beesect](https://github.com/rtmigo/beesect_dart)

My early 🚧 port of the Python `bisect` library to the Dart language.

Unit tests in Dart are automatically generated by Python
module `test/bisect_test_generator.py`. Therefore, I expect a high degree of
conformity of the results to the original.

# Depend

Add the following to`pubspec.yaml`:

```yaml
dependencies:
  beesect:
    git:
      url: https://github.com/rtmigo/beesect_dart
      ref: staging
```

# Import

```dart
import 'package:beesect/beesect.dart';
```

# Example

```dart
import 'package:beesect/beesect.dart';

void main() {
  // the list must be sorted
  var list = ['A', 'B', 'C', 'E'];

  // Find the index of an item in a sorted list
  print(bisectLeft(list, 'B'));  // prints 1

  // find the future index for a non-existent item
  print(bisectLeft(list, 'D'));  // prints 3

  // add an item to the list while keeping the list sorted
  insortLeft(list, 'D');
  print(list);  // [A, B, C, D, E]
}
```

# Lists of numbers

`beesect` functions work with lists of objects implementing the `Comparable` class.

Although numbers like int do not implement this class, the problem is easily solved as follows.

```dart
List<int> numbers = [1, 2, 3];

// insortRight(numbers, 4); // does not compile: cannot guess the item type
// insortRight<int>(numbers, 4); // does not compile: int is not a Comparable

insort<num>(numbers, 4);  // this works: num is a Comparable
```