This script perform removing the sinusoidal noise in image, with the steps specified.

The procedure follows the main flow: 


Image --- `FFT` ---> Fourier Transform of image --- `centering` ---> FFT-ed and centered image --- `enhancement` ---> Enhanced FFT image --- `iFFT` ---> Enhanced image

Note that information of noise are represented on the `real` part of the transformed image, so any transformation will be performed on this section. The `imaginary` part only contains knowledge about the phases.

The sinusoidal noise are represented by white points on the transformed image, which are all local maximas. The positions of the maximas affect the direction and frequency of the sinusoidal noise. The farther the points from origin, the more frequent is the sinusoidal. 

The noise is also additive: Multiple points of max value on a frame create a set of noise signals. However, they can also be mistakenly recognized as normal points (or vice versa). Therefore, it is exhausted to find and remove them manually.

However, we can apply blurring filter in order to smooth the image before finding the peaks. Any bluring filter can be applied for this purpose. After that, when the peak can be found more easily, They can be picked out easily by different peak-finding function.

These points are eliminated by setting their value to 0. In order to the action to be more effective, a `mask` can be created and applied. Usually, a small circle mask is used. In this case, for simplicity, we use a cross mask to hide the points.

By doing this, users are not limited by finding all the peaks manually, but automatically finding all suspicious points and remove them, i.e remove the sinusoidal noise in any direction and frequency.

After removing the noise, the image can be enhanced further by improving light, contrast to prepare for other (e.g counting) operations.

The script is written using basic math functions of `matplotlib` library to perform peak seeking and Fourier transformation. 
