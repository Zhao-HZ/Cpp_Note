# Here is the example

```c++
//Include Libraries
#include<openopencv.hpp>
#include<iostream>

// Namespace nullifies the use of cv::function(); 
using namespace std;
using namespace cv;

// Read an image 
Mat img_grayscale = imread("test.jpg", 0);

// Display the image.
imshow("grayscale image", img_grayscale); 

// Wait for a keystroke.   
waitKey(0);  

// Destroys all the windows created                         
destroyAllWindows();

// Write the image in the same directory
imwrite("grayscale.jpg", img_grayscale);
```

## Reading an Image

```
imread(filename, flags)
```

`filename` is a qualified pathname to the file
`flags` is an <u>optional</u> flag that lets you specify how the image should be represented.
There are two flags

- IMREAD_UNCHANGED or -1 
- IMREAD_GRAYSCALE or 0 
- IMREAD_COLOR or 1 

But the default value for flags is 1, which will read in the image as a Colored image

## Displaying an Image

```c++
imshow(window_name,  image)
```

`window_name` is the window name that will be displayed on the window
`image` is the image that you want to display

## Write an Image
```c++
imwrite(filename, image)
```
`filename` is a filename, which must include the filename extension(png, jpg).
`image` is the image you want to save.The function returns True if the image is saved successfully.