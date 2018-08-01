#Bitmap如何压缩

##Bitmap.compress()
质量压缩：
它是在保持像素的前提下改变图片的位深及透明度等，来达到压缩图片的目的，不会减少图片的像素。进过它压缩的图片文件大小会变小，但是解码成bitmap后占得内存是不变的。

##BitmapFactory.Options.inSampleSize
```
public static Bitmap decodeSampledBitmapFromResource(Resources res, int resId,
        int reqWidth, int reqHeight) {
    // 设置inJustDecodeBounds属性为true，只获取Bitmap原始宽高，不分配内存；
    final BitmapFactory.Options options = new BitmapFactory.Options();
    options.inJustDecodeBounds = true;
    BitmapFactory.decodeResource(res, resId, options);
    // 计算inSampleSize值；
    options.inSampleSize = calculateInSampleSize(options, reqWidth, reqHeight);
    // 真实加载Bitmap；
    options.inJustDecodeBounds = false;
    return BitmapFactory.decodeResource(res, resId, options);
}

public static int calculateInSampleSize(
            BitmapFactory.Options options, int reqWidth, int reqHeight) {
    // Raw height and width of image
    final int height = options.outHeight;
    final int width = options.outWidth;
    int inSampleSize = 1;
    if (height > reqHeight || width > reqWidth) {
        final int halfHeight = height / 2;
        final int halfWidth = width / 2;
        // 宽和高比需要的宽高大的前提下最大的inSampleSize
        while ((halfHeight / inSampleSize) >= reqHeight
                && (halfWidth / inSampleSize) >= reqWidth) {
            inSampleSize *= 2;
        }
    }
    return inSampleSize;
}

```

作者：双十二技术哥
链接：https://www.jianshu.com/p/e49ec7d053b3
來源：简书
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。