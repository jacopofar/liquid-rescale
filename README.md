Java liquid rescale
===

A small library with no dependencies to implement [seam carving](https://en.wikipedia.org/wiki/Seam_carving) (aka liquid rescale) in pure Java (Java 6 or later).

Given a BufferedImage, the static methods in this class reduce its width by a given amount of pixels, trying to remove the pixels less likely to be relevant.
Pixel relevance is calculated as a weighted average between the difference of two consecutive pixels in a path and the magnitude of the gradient of one of them.

The software does not work on Android, since the BufferedImage (and the whole java.awt.* package as well) is not present. We should use a [Bitmap](https://developer.android.com/reference/android/graphics/Bitmap.html) instead, but that's not present in Java SE.

Usage
-----

The simplest use case is this:

    //open the image, from a File, an URL or an InputStream
	BufferedImage imgIn = ImageIO.read(new File("picture.jpg"));
	//reduce the width by 125 pixels, with steps of 10 pixels
	BufferedImage imgOut = rescaleImageInSteps(imgIn,125,10);
	//save it to local filesystem
	ImageIO.write(imgOut, "JPEG", new File("rescaled.jpg"));

the greater the step (in this case 10), the more accurate but slower is the rescaling. Try yourself to see which one fits your needs.

You can also get an heatmap representing the relevance of pixels (blue=less relevant, red=most relevant):

     BufferedImage imgIn = ImageIO.read(new File("picture.jpg"));
     int[][] minVarianceValue = getMinVarianceMatrix(imgIn);
     BufferedImage imgVariance =getColorScaleVarianceMatrix(minVarianceValue);
     ImageIO.write(imgVariance, "JPEG", new File("variance_values.jpg"));

look at the Javadoc for a better explanation.

Examples and further explanaion
-------
[see here](http://jacopofar.wordpress.com/2014/10/18/seam-carving-in-pure-java/)

