---
title: "How Do Image Loading Libraries work internally In Android?"
seoTitle: "How do Image Loading libraries like Glide in android work internally?"
seoDescription: "How do Image loading libraries like glide Picasso works internally in Android?"
datePublished: Wed Mar 29 2023 22:28:47 GMT+0000 (Coordinated Universal Time)
cuid: clfu9dtpd000d0amn3m0q0g2h
slug: how-do-image-loading-libraries-work-internally-in-android
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680809108782/fa8bfbdb-b1fe-45b5-9d6c-876907567b37.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1680473357589/412a59a3-b202-483d-9469-90b584aa41b8.png
tags: android-app-development, android, android-apps, imageloadinglibrary, glide

---

### Why Does A Image Loading Library Exist?

Why utilize an external library should be the first question that pops into your head. Is it only because we want to write fewer lines of code? perhaps it has additional aspects. Let's learn the fundamentals of loading an image from a URL.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680809251984/dc8a2dc5-3aac-40f0-95f3-8678246d5d91.png align="center")

It appears simple. This approach will work for the app's single image. However, as the number of images increases, you will begin to experience these issues.

* **The app will feel unresponsive and Laggy** - Because a large amount of memory will be allocated to these images in the heap, and the [GC](https://developer.android.com/topic/performance/memory-overview#gc) will attempt to release the memory whenever this image view is off the screen.
    
* **Out Of Memory and App crash** - Because our heap has a limited amount of memory if we keep assigning it multiple images, eventually it will run out of memory and the app will crash.
    
* **Slow Loading of Images and Poor UX** - Since we will be loading images one at a time, this method will slow down the loading of the images.
    
    As an example, if there are 20 images on the screen and the user scrolls to image number 20, the first 19 images will load before the 20th one. Additionally, the user wants to view the image of the spot where he is now, so this is an awful user experience.
    

Now let's see how these libraries fix these problems for us and make our life easier.

### 1\. How does Image Loading Library add Responsiveness to the App?

The Answer is BitmapPool.

In Android, a Bitmap Pool is a cache that keeps reusable Bitmap objects in memory. The purpose of a Bitmap Pool is to reduce the frequency of garbage collection and improve performance by recycling Bitmaps that are no longer being used.

When you load Bitmaps in your Android application, the system allocates memory for each Bitmap object. When the Bitmap is no longer needed, the memory used by the Bitmap is released and can be reused by the system.

However, allocating new memory for Bitmaps can be expensive and cause performance issues if done frequently.

By using a Bitmap Pool, you can reuse Bitmaps that are no longer being used instead of allocating new memory each time. This can improve the performance of your application and reduce the frequency of [garbage collection](https://developer.android.com/topic/performance/memory-overview#gc).

Here's an example of how to create and use a Bitmap Pool in Android:

```java
// Create a Bitmap Pool with the desired size
BitmapPool bitmapPool = new LruBitmapPool(maxSizeBytes);

// Load a Bitmap into memory
Bitmap bitmap = BitmapFactory.decodeResource(resources, resourceId);

// Get a Bitmap from the pool, or allocate a new one
Bitmap pooledBitmap = bitmapPool.get(bitmap.getWidth(), bitmap.getHeight(), Bitmap.Config.ARGB_8888);

// Set the pixels of the pooled Bitmap to match the original Bitmap
pooledBitmap.setPixels(bitmap.getPixels(), 0, bitmap.getWidth(), 0, 0, bitmap.getWidth(), bitmap.getHeight());

// Use the Bitmap

// When the Bitmap is no longer needed, return it to the pool
bitmapPool.put(pooledBitmap);
```

In the above example, a Bitmap Pool is created using the LruBitmapPool implementation with the maximum size in bytes that the pool can hold.

The code then loads a Bitmap and retrieves a Bitmap object from the pool using the `get()` method. If there is no available Bitmap in the pool, a new Bitmap is allocated.

The pixels of the new Bitmap is set to match the original Bitmap, and the pooled Bitmap is used for the intended purpose. When the Bitmap is no longer needed, it should be returned to the pool using the `put()` method.

For example, if our bitmap pool is capable of holding 20 bitmaps and the user is scrolling through a list of 40 images when the user will reach the 21st position, the memory of the 1st bitMap will be reused to store the 21st bitmap

```java
final BitmapFactory.Options options = new BitmapFactory.Options();
options.inJustDecodeBounds = true;

//Decoding bitmap from file
BitmapFactory.decodeFile(filePathTwntyOne, options); 
options.inMutable = true;

//attempt to reuse bitmapOne when loading content
options.inBitmap = bitmapOne;
options.inJustDecodeBounds = false;

Bitmap bitmapTwentyOne = BitmapFactory.decodeFile(filePathTwntyOne, options);
imageView.setImageBitmap(bitmapTwentyOne);
```

You can read more about BitmapFactory [here](https://developer.android.com/reference/android/graphics/BitmapFactory).

### 2\. How do Image Loading Libraries solve OutOfMemory issues?

The Answer is the downsampling of the image.

Image downsampling is the process of decreasing the resolution of a digital image. Downsampling is done by reducing the number of pixels in the image, which in turn reduces the amount of information stored in the image.

The process of downsampling can be used to reduce the file size of an image or to create a smaller version of the same image.

Downsampling can be achieved by removing every other pixel in a specified direction, or by taking an average of adjacent pixels to create a new, smaller image. Image downsampling can also be referred to as image resampling or image scaling.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680809556970/a1fa13b6-f5ea-4588-85d3-dbd3d8eb26b4.png align="center")

After Downloading the Entire image File from the URL The Library Downsample it to the size of imageView.

As an example, the downloaded image resolution may be 1920\*1080 but our imageView size is 420\*270. So we don't need to decode the whole image in 1920\*1080 resolution which will waste resources unless you have explicitly told the library not to downsample it. So it gets downsampled to 420\*270 and sent to imageView.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680809525464/11f70e93-cc17-4517-814e-e59e464cd898.png align="center")

```java
public Bitmap getResizedBitmap(int targetW, int targetH,  String imagePath) {

    // Get the dimensions of the bitmap
    BitmapFactory.Options bmOptions = new BitmapFactory.Options();

    //inJustDecodeBounds = true <-- will not load the bitmap into memory
    bmOptions.inJustDecodeBounds = true;
    BitmapFactory.decodeFile(imagePath, bmOptions);
    int photoW = bmOptions.outWidth;
    int photoH = bmOptions.outHeight;

    // Determine how much to scale down the image
    int scaleFactor = Math.min(photoW/targetW, photoH/targetH);

    // Decode the image file into a Bitmap sized to fill the View
    bmOptions.inJustDecodeBounds = false;
    bmOptions.inSampleSize = scaleFactor;

    Bitmap bitmap = BitmapFactory.decodeFile(imagePath, bmOptions);
    return(bitmap);
}
```

### **3\. How Image Loading Libraries solve the Slow loading issue?**

Here 2 things come into the picture. **Prioritizing** and **deprioritizing** the image request and **Cache Management**.

**Prioritizing Request**

Multiple image requests may be added to the queue when switching from one page to another. However, we must load the images where the user is at the moment according to the precedence.

As we provide the context to the imageLoading request it exactly knows what is the exact position of the user. And based on that it prioritizes the request. As a result, the current screen images load as soon as possible.

---

**Cache Management**

Memory caching and disk caching are two different types of caching mechanisms used in image-loading libraries:

**Memory Caching:** It is the process of temporarily storing data (in this case, images) in the device's RAM or memory. When the data is accessed again, it can be loaded more quickly since it's stored in memory.

Memory caching is ideal for frequently accessed data, such as images that are repeatedly displayed on the screen.

The drawback of memory caching is that it can consume a lot of RAM, leading to memory overflow and crashes. This is why we use the Bitmap pool as discussed above.

**Disk Caching:** It is the process of saving data (in this case, images) to the device's local storage. When the data is accessed again, it's loaded from the disk instead of being downloaded from the internet or server, which can be slower.

Disk caching is ideal for infrequently accessed data since it doesn't consume memory as memory caching does. The drawback of disk caching is that it requires more storage space on the device, and the read/write operations can also be slow.

whenever a new request is introduced to the queue it first looks for the image in-memory cache. If it is not found, look in the disc cache. If that fails, go to the source URL to obtain the downsample and set it as the imageView.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680809581881/a51ab46b-5e15-449c-b8ad-72197dbf39b7.png align="center")

### Conclusion

As we have seen, image-loading libraries not only allow us to write less code but also directly address several more difficult problems, making the lives of developers much simpler.

Here is an LLD of these libraries.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681065881831/2b523cc3-2d15-42ab-b9ea-839ca6b73ece.png align="center")

Some of the popular Image loading libraries are [Glide](https://github.com/bumptech/glide), [Picasso](https://github.com/square/picasso), [Freso](https://frescolib.org/), and [COIL](https://coil-kt.github.io/coil/).