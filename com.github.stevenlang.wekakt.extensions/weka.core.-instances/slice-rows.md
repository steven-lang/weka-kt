[wekakt](../../index.md) / [com.github.stevenlang.wekakt.extensions](../index.md) / [weka.core.Instances](index.md) / [sliceRows](./slice-rows.md)

# sliceRows

`fun `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)`.sliceRows(range: `[`IntRange`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.ranges/-int-range/index.html)`): `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)

Slice the given range of rows out of the dataset.

``` kotlin
//Unresolved: sampleSliceRowsRange
```

### Parameters

`range` - Range of ints indicating the slice interval

**Return**
Subset of this dataset, that is only the rows in the given range are in the result

`fun `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)`.sliceRows(vararg indices: `[`Int`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-int/index.html)`): `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)

Get the subset of rows with the given indices.

``` kotlin
//Unresolved: sampleSliceRowsIndices
```

### Parameters

`indices` - List of indices to return the rows of

**Return**
Subset of this dataset containing only the rows specified in [indices](slice-rows.md#com.github.stevenlang.wekakt.extensions$sliceRows(weka.core.Instances, kotlin.IntArray)/indices)
