
# Structure
There are three main parts of a PopAnim file: `image`, `sprite`, `main_sprite`.

## `image`
A list of objects, each with three properties:  

### `name`
The name of the image.

_The name is separated into two parts by_ `|` _. These names are used to provide reference to the separated atlas textures which have the same name. Strangely, these atlas textures use a different path name (specified on the left side of the bar) and id name (specified on the right side of the bar)._

### `size`
The size of the image in pixels.  
  
_This is NOT the same as the actual texture size in pixels. Thus the images must be rescaled to this size. The scaling factor is `a / b` both where `a` is the actual size of the image (in pixels) and `b` is the size specified in this property (also in pixels). This is applicable both horizontally and vertically)._  

### `transform`
The transform of the image.

_This property specifies an Affine Transform used in ActionScript, Flash and CSS very often. It is an array of 2, 3 or 6 items, each corresponding to a different transform parameter. In this case however, all cases of this property in `image` are only seen to have 6 items each._

## `sprite`
It gets a little more interesting in this part.

# Details
## Affine Transform
There are three different cases of an Affine Transform array. The positions have pixels as their units, whereas other variables are unitless (i.e., they work the same despite the object size as they are relative to the object size and hence independent of it).

### Case 1: A 6 Element Array
This is the simplest case of this transform.  
The 6 parameters correspond to `scaleX`, `skewY`, `skewX`, `scaleY`, `positionX` and `positionY` respectively. 
It is equivalent to the following Affine Transform:
```C#
float[] affineTransform = new float[] {
  scaleX, 
  skewY, 
  skewX, 
  scaleY, 
  positionX, 
  positionY 
};
```

### Case 2: A 3 Element Array
Also a simple case of this transform.  
The 3 parameters correspond to `rotation`, `positionX` and `positionY` respectively.  
It is equivalent to the following Affine Transform:
```C#
float[] affineTransform = new float[] {
  Mathf.Cos(rotation * Mathf.PI / 1000), 
  -Mathf.Sin(rotation * Mathf.PI / 1000), 
  Mathf.Sin(rotation * Mathf.PI / 1000),
  Mathf.Cos(rotation * Mathf.PI / 1000), 
  positionX, 
  positionY 
};
```

### Case 3: A 2 Element Array
This case is a bit complicated to implement. In this Transform, only the positions are changed, whereas the remaining parameters are kept the same as before. This was not the case in the previous two cases, where all 6 parameters are replaced.  
It is equivalent to the following Affine Transform:
```C#
float[] affineTransform = new float[] {
  previousScaleX, 
  previousSkewY, 
  previousSkewX, 
  previousScaleY, 
  positionX, 
  positionY
};
```

### A More Detailed Look

