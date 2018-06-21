[wekakt](../../index.md) / [com.github.stevenlang.wekakt.extensions](../index.md) / [weka.core.Instances](index.md) / [sliceAttributes](./slice-attributes.md)

# sliceAttributes

`fun `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)`.sliceAttributes(range: `[`IntRange`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.ranges/-int-range/index.html)`): `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)

Slice the given range of attributes out of the dataset.

``` kotlin
//Unresolved: sampleSliceAttributesRange
```

### Parameters

`range` - Range of ints indicating the slice interval

**Return**
Subset of this dataset, that is only the attributes in the given range are in the result

`fun `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)`.sliceAttributes(vararg indices: `[`Int`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-int/index.html)`): `[`Instances`](http://weka.sourceforge.net/doc.stable/weka/core/Instances.html)

Get the subset of attributes with the given indices.

``` kotlin
//Unresolved: sampleSliceAttributeIndices
```

### Parameters

`indices` - List of indices to return the attributes of

**Return**
Subset of this dataset containing only the attributes specified in [indices](slice-attributes.md#com.github.stevenlang.wekakt.extensions$sliceAttributes(weka.core.Instances, kotlin.IntArray)/indices)
