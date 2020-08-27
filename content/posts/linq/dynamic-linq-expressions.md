---
title: "Dynamic LINQ Expressions"
date: 2020-08-25T18:15:40+03:00
author: "codevictory"
description: ""
draft: false
---

There is many situations when LINQ-expressions are not known during the build time. Luckily there is .NET standard library [System.Linq.Expressions](https://www.nuget.org/packages/System.Linq.Expressions/) available to satisfy just that need. Here's a quick look on how to create and use it effectively with C#.

## Basic use cases

Let say we want to query some data storage with rules collected from the user in real time. There is no way to know what kind of LINQ expressions are needed to give the right answer during build-time. 

Other common situation is when the quering rules are somewhere else than in the source code eg. database. In other words this means launching the program first and getting the rules afterwords. Again we end up in the sitaution where LINQ clause cannot be known during the build-time.

## Structure of the LINQ clause

In order to understand how `System.Linq.Expressions` works we first need to look at the abstract structure of the LINQ method itself. 

Eventhough there are two ways to write LINQ clause, query and method syntax, I find it much more straight-forward to use method syntax when dealing with dynamic expressions.

Method syntax consist of **method** to which **predicate** (lambda form in this article) is given as a parameter. Predicate is a C# delegate consisting of **parameter**(s) which is given to be compared by one or more **expressions**. Expressions can also be inside each other thus forming so called [Expression Tree](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/expression-trees/). One expression typically contains **member**, **operator** and **constant**. Member represents a property of the lambda parameter object. Operator is what defines the comparison like &&, || or >. And finally constant is a value on the other side of the operator which member is compared to.

All this might be very confusing for a casual LINQ user (like me) at first but hopefully the following pseudo code explanation clears it out a little bit.

LINQ method:
```csharp
Where(emperor => emperor.StartOfReign > 70 && emperor.Dynasty == Dynasty.Flavian)
```

Explanation:
```csharp
METHOD[
    Where(PREDICATE[
        PARAMETER[emperor] => EXPRESSION[
            EXPRESSION[emperor.StartOfReign > 70] && 
            EXPRESSION[emperor.Dynasty == Dynasty.Flavian]
        ]
    ])
]
```

## Usage of System.Linq.Expressions

Purpose of `System.Linq.Expressions` is to build predicates for LINQ methods like `Where`.

For example above method's predicate can be build dynamically as follows:

```csharp
var parameter = Expression.Parameter(typeof(Emperor));

// StartOfReign (SOR) expression.
var SOR_member = Expression.Property(parameter, "StartOfReign");
var SOR_constant = Expression.Contant(70);
var SOR_expression = Expression.GreaterThan(startOfReign_member, SOR_constant);

// Dynasty expression.
var dynasty_member = Expression.Property(parameter, "Dynasty");
var dynasty_constant = Expression.Contant(Dynasty.Flavian);
var dynasty_expression = Expression.Equal(dynasty_member, dynasty_constant);

// Final predicate
Expression.And(SOR_expression, dynasty_expression);
```

As you can see `Expression` library's functions are simply just instantiating different parts of the lambda clause. These instances can be used, in turn, to instantiate the other expressions like `Expression.Equal`.

Something I found a bit confusing (and hard to debug) is how `Expression.Property` should be used. It feels intuitive that it doesn't matter which instance of the property you use while the type you use is the same. But this is not true. It is actually the same, one and only lambda parameter you should be referring to every time a new expression is added.

For example the following produces an error:

```csharp
// StartOfReign (SOR) expression.
var SOR_member = Expression.Property(Expression.Parameter(typeof(Emperor)), "StartOfReign");
var SOR_constant = Expression.Contant(70);
var SOR_expression = Expression.GreaterThan(startOfReign_member, SOR_constant);

// Dynasty expression.
var dynasty_member = Expression.Property(Expression.Parameter(typeof(Emperor)), "Dynasty");
var dynasty_constant = Expression.Contant(Dynasty.Flavian);
var dynasty_expression = Expression.Equal(dynasty_member, dynasty_constant);

// Final predicate
Expression.And(SOR_expression, dynasty_expression); //throws exception
```

This is because final expressions are referring to a different parameter instances while they should share one and the same.

## Try out yourself

I made a little console application to play around with this in practice. Source code and installation guide can be found in my GitHub repo: [github.com/codevictory/dynamic-linq-expressions](https://github.com/codevictory/dynamic-linq-expressions). Have fun!