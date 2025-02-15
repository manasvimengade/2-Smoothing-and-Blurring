# 2-Smoothing-and-Blurring
When working with images, sometimes they appear too sharp or have rough edges that need to be smoothed for better quality. Other times, images may have harsh edges that need softening to make them more usable. In OpenCV, there are several methods available to blur or smooth an image. Let's go through them one by one.

Method 1: With 2D Convolution [exp2.1]
Syntax: filter2D(sourceImage, ddepth, kernel)
=> This method gives us full control over the smoothing process because we create a custom kernel (a small 2D matrix using a NumPy array). The kernel assigns specific weights to each pixel in the image and calculates a new pixel value by averaging its neighboring pixels. This process helps reduce image clarity, making it appear smoother or blurred. By applying 2D convolution, we can easily soften sharp details in an image.

Method 2:  With pre-built functions 
OpenCV comes with many prebuilt blurring and smoothing functions.

1. Averaging: [exp2-2.1]
   Syntax: cv2.blur(image, shapeOfTheKernel)
   Image– The image you need to smoothen
   shapeOfTheKernel– The shape of the matrix-like 3 by 3 / 5 by 5
   In this method, we use a **kernel** (a small matrix) of a chosen shape, like **3x3 or 5x5**, to blur the image. This method works similarly to **2D convolution**, where the center pixel’s value is replaced with
   the **average of its surrounding pixels**. This helps in **reducing noise** by blending pixels with similar colors, making the image smoother.
   The kernel used in this method is a matrix filled with **1s**, and its values are divided by the total number of elements in the matrix. This ensures that each pixel's new value is an average of its neighboring
   pixels, effectively blurring the image.

2. Gaussian Blur: [exp2-2.2]
   Syntax: cv2. GaussianBlur(image, shapeOfTheKernel, sigmaX )
   Image– the image you need to blur
   shapeOfTheKernel– The shape of the matrix-like 3 by 3 / 5 by 5
   sigmaX– The Gaussian kernel standard deviation which is the default set to 0
   Unlike simple averaging, Gaussian blur uses a weighted mean instead of a box filter with equal values. The pixels closer to the center of the kernel have higher weights, while the ones further away have lower
   weights.This results in a smoother, more natural blur because it preserves edges better than simple averaging. Instead of just averaging the pixel values, Gaussian blur applies a specific weighting system,
   making the blur effect look more realistic. For example, in a 3x3 kernel, the total sum of weights is typically 16, ensuring proper normalization.

3. Median blur: [exp2-2.3]
   Syntax: cv. medianBlur(image, kernel size)
   Image– The image we need to apply the smoothening
   KernelSize– the size of the kernel as it always takes a square matrix the value must be a positive integer more than 2.
   The **Median Blur** method is a smoothing technique where the center pixel of a selected kernel window is replaced with the **median value** of all the surrounding pixels. Unlike Gaussian or box blur, where
   new pixel values are computed as weighted or simple averages (which can introduce colors that were not originally in the image), median blur ensures that the replaced pixel value is **always present in the
   image**, making the blur effect look more natural. This method is particularly effective in **removing noise**, such as salt-and-pepper noise, while preserving edges better than other blurring techniques.
   Additionally, the kernel size used must be a **positive odd integer** greater than **2**, such as **3x3, 5x5, or 7x7**.

4. Bilateral blur: [exp2-2.4]
   Syntax: cv2.bilateralFilter(image, diameter, sigmaColor, sigmaSpace)
   Image– The image we need to apply the smoothening
   Diameter– similar to the size of the kernel
   SigmaColor– The number of colors to be considered in the given range of pixels [the higher value represents the increase in the number of colors in the given area of pixels]—Should not keep very high
   SigmaSpace – the space between the biased pixel and the neighbor pixel higher value means the pixels far out from the pixel will manipulate in the pixel value
   The Bilateral Blur technique is a smoothing method that helps reduce noise while preserving edges, unlike other blur techniques that may cause edge loss. It works by considering both color similarity and
   spatial distance when filtering an image.
