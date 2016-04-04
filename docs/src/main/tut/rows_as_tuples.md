---
layout: default
title:  "Decoding rows as tuples"
section: tutorial
sort: 3
---

In a [previous tutorial](rows_as_collections.html), we saw how to deal with CSV data composed of rows of homogeneous
types. While a common enough scenario, you'll also find yourself having to deal with heterogeneous data types fairly
often.

Take, for instance, the [wikipedia CSV example](https://en.wikipedia.org/wiki/Comma-separated_values#Example), which
we'll get from this project's resources:

```tut:silent
val rawData: java.net.URL = getClass.getResource("/wikipedia.csv")
```

This is what this data looks like:

```tut
scala.io.Source.fromURL(rawData).mkString
```

One way of representing each row could be as a tuple. Let's declare it as a type alias, for brevity's sake:

```tut:silent
type Car = (Int, String, String, Option[String], Float)
```

kantan.csv has out of the box support for decoding tuples, so you can simply pass the corresponding type to
[`asCsvReader`]:

```tut:silent
import kantan.csv.ops._ // Brings in the kantan.csv syntax.

val reader = rawData.asCsvReader[Car](',', true)
```

And now that we have a [`CsvReader`] on the data, we can simply iterate through it:

```tut
reader.foreach(println _)
```

## What to read next
If you want to learn more about:

* [decoding rows as case classes](rows_as_case_classes.html)
* [how `CsvReader` guessed how to turn CSV rows into `Car` instances](rows_as_arbitrary_types.html) 
* [encoding tuples as rows](collections_as_rows.html)
* [how we were able to turn a `URL` into CSV data](csv_sources.html)
 

[`asCsvReader`]:{{ site.baseurl }}/api/#kantan.csv.ops$$CsvInputOps@asCsvReader[B](sep:Char,header:Boolean)(implicitevidence$3:kantan.csv.RowDecoder[B],implicitai:kantan.csv.CsvInput[A],implicite:kantan.csv.engine.ReaderEngine):kantan.csv.CsvReader[kantan.csv.ReadResult[B]]
[`CsvReader`]:{{ site.baseurl }}/api/#kantan.csv.CsvReader