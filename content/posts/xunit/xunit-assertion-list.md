---
title: 'xUnit - List of Assertions'
date: 2020-05-03T22:24:44+03:00
author: 'codevictory'
description: 'List of assertion functions available in xUnit.'
draft: false
---

| Name                 | Description                                                                                                                                         |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| All                  | Verifies that all items in the collection pass when executed against action.                                                                        |
| Collection           | Verifies that a collection contains exactly a given number of elements, which meet the criteria provided by the element inspectors.                 |
| Contains             | Verifies that a collection contains a given object.                                                                                                 |
| DoesNotContain       | Verifies that a collection does not contain a given object.                                                                                         |
| DoesNotMatch         | Verifies that a string does not match a regular expression.                                                                                         |
| Empty                | Verifies that a collection is empty.                                                                                                                |
| EndsWith             | Verifies that a string ends with a given string, using the current culture.                                                                         |
| Equals               | Verifies that two sequences are equivalent, using a default comparer.                                                                               |
| False                | Verifies that the condition is false.                                                                                                               |
| InRange              | Verifies that a value is within a given range.                                                                                                      |
| IsAssignableFrom     | Verifies that an object is of the given type or a derived type.                                                                                     |
| IsNotType            | Verifies that an object is not exactly the given type.                                                                                              |
| IsType               | Verifies that an object is exactly the given type (and not a derived type).                                                                         |
| Matches              | Verifies that a string matches a regular expression.                                                                                                |
| NotEmpty             | Verifies that a collection is not empty.                                                                                                            |
| NotEqual             | Verifies that two sequences are not equivalent, using a default comparer.                                                                           |
| NotInRange           | Verifies that a value is not within a given range, using the default comparer.                                                                      |
| NotNull              | Verifies that an object reference is not null.                                                                                                      |
| NotSame              | Verifies that two objects are not the same instance.                                                                                                |
| NotStrictEqual       | Verifies that two objects are strictly not equal, using the type's default comparer.                                                                |
| Null                 | Verifies that an object reference is null.                                                                                                          |
| ProperSubset         | Verifies that a set is a proper subset of another set.                                                                                              |
| ProperSuperset       | Verifies that a set is a proper superset of another set.                                                                                            |
| PropertyChanged      | Verifies that the provided object raised System.ComponentModel.INotifyPropertyChanged.PropertyChanged as a result of executing the given test code. |
| PropertyChangedAsync | Verifies that the provided object raised System.ComponentModel.INotifyPropertyChanged.PropertyChanged as a result of executing the given test code. |
| Raises               | Verifies that a event with the exact event args is raised.                                                                                          |
| RaisesAny            | Verifies that an event with the exact or a derived event args is raised.                                                                            |
| RaisesAnyAsync       | Verifies that an event with the exact or a derived event args is raised.                                                                            |
| RaisesAsync          | Verifies that a event with the exact event args (and not a derived type) is raised.                                                                 |
| ReferenceEquals      | Do not call this method. (_this is actually from the source code comment_)                                                                          |
| Same                 | Verifies that two objects are the same instance.                                                                                                    |
| Single               | Verifies that the given collection contains only a single element of the given type.                                                                |
| StartsWith           | Verifies that a string starts with a given string, using the current culture.                                                                       |
| StrictEqual          | Verifies that two objects are strictly equal, using the type's default comparer.                                                                    |
| Sunset               | Verifies that a set is a subset of another set.                                                                                                     |
| Superset             | Verifies that a set is a superset of another set.                                                                                                   |
| Throws               | Verifies that the exact exception is thrown (and not a derived exception type).                                                                     |
| ThrowsAny            | Verifies that the exact exception or a derived exception type is thrown.                                                                            |
| ThrowsAnyAsync       | Verifies that the exact exception or a derived exception type is thrown.                                                                            |
| ThrowsAsync          | Verifies that the exact exception is thrown (and not a derived exception type).                                                                     |
| True                 | Verifies that an expression is true.                                                                                                                |
