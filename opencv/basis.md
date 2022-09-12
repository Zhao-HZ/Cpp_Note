# Here is the example

```
#include <opencv2/opencv.hpp>
#include "stdio.h"

using namespace std;
using namespace cv;

int main(int argc, char const *argv[])
{
    Mat img_grayscale = imread(argv[1], 0);
    if (argc > 1) {
        imshow("gray scale image", img_grayscale);
        waitKey(0);
        destroyAllWindows();    
    } else {
        cout << "No image" << endl;
        return 0;
    }
    return 0;
}
```

## Reading an Image
```
imread(filename, flags)
```
`filename` is a qualified pathname to the file
`flags` is an <u>optional</u> flag that lets you specify how the image should be represented.
There are two flags
- `cv2::IMREAD_UNCHANGED or -1` 
- `cv2::IMREAD_GRAYSCALE or 0`
- `cv2::IMREAD_COLOR or 1` 

But the default value for flags is 1, which will read in the image as a Colored image
## Displaying an Image
```
imshow(window_name,  image)
```
`window_name` is the window name that will be displayed on the window
`image` is the image that you want to display

The `imshow` is designed to be used along with the `waitKey(0)` and `destroyAllWindows` or `destroyWindow()` function.
If 0 is passed, the program waits indefinitely for a keystroke.

## Write an Image
```
imwrite(filename, image)
```
`filename` is a filename, which must include the filename extension(png, jpg).
`image` is the image you want to save.The function returns True if the image is saved successfully.
