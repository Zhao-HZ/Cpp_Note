# Here is the example
```c++
// Include Libraries
#include<open/open.hpp>
#include<iostream>

// Namespace to nullify use of :function(); syntax
using namespace std;
using namespace cv 

int main()
{
	// initialize a video capture object
	VideoCapture vid_capture("Resources/Cars.mp4");

	// Print error message if the stream is invalid
	if (!vid_capture.isOpened())
	{
		cout << "Error opening video stream or file" << endl;
	}

	else
	{
		// Obtain fps and frame count by get() method and print
		// You can replace 5 with CAP_PROP_FPS as well, they are enumerations
		int fps = vid_capture.get(5);
		cout << "Frames per second :" << fps;

		// Obtain frame_count using openbuilt in frame count reading method
		// You can replace 7 with CAP_PROP_FRAME_COUNT as well, they are enumerations
		int frame_count = vid_capture.get(7);
		cout << "  Frame count :" << frame_count;
	}


	// Read the frames to the last frame
	while (vid_capture.isOpened())
	{
		// Initialise frame matrix
		Mat frame;

	    // Initialize a boolean to check if frames are there or not
		bool isSuccess = vid_capture.read(frame);

		// If frames are present, show it
		if(isSuccess == true)
		{
			//display frames
			imshow("Frame", frame);
		}

		// If frames are not there, close it
		if (isSuccess == false)
		{
			cout << "Video camera is disconnected" << endl;
			break;
		}
		
		//wait 20 ms between successive frames and break the loop if key q is pressed
		int key = waitKey(20);
		if (key == 'q')
		{
			cout << "q key is pressed by the user. Stopping the video" << endl;
			break;
		}


	}
	// Release the video capture object
	vid_capture.release();
	destroyAllWindows();
	return 0;
}
```
## Reading Video From a File
`VideoCapture(path, apiPreference)` 
It can create a `VideoCapture` object
`path` is the filename/path to the video file
`apiPreference` is optional
Create a video object.
`VideoCapture vid_capture('./res/test.mp4')`
Then we can use the `isOpened()` method to confirm the video file was opened  successfully
Assuming the video file was opened successfully,we can use the `get()` method to retrive important metadata associated with the video stream.
Notice that this method does not apply to web cameras.
In the example, 5 and 7 correspond to the frame rate(CAP_PROP_FPS) and frame count(CAP_PROP_FRAME_COUNT).
```c++
int fps = vid_capture.get(5) // Get frame rate information
int frame_count = vid_capture.get(7) // Get frame count
```
In order to read each image frame from the file, we creat a loop and read one frame at a time from the video stream using the `vid_capture.read()` method which returns a tuple, <u>where the first element is a boolean and the next element is the actual video frame<u>.
<u>when the first element is true, it indicates the video stream contains a frame to read</u>
At the end you need to release the Video_Capture object and close the window

```C++
vid_capture.release();
destroyAllWindows();
```
## Reading an Image Sequence
## Reading Video from a Webcam
You need to give a video capture device index, as shown below
- If your system has a built-in webcam, then device index == 0 
- If you have more than one camera connected to your system, then the device index associated with each additional camera is incremented(e.g. 1, 2, etc)

```C++
VideoCapture vid_capture(0);
```
`CAP_DSHOW` is an optional argument, it is short for directshow via video input

## Writing the Video
- Retrieve the image frame height and width,using the `get()` method
- Initialize a video capture object, to read the video stream into memory, using any of the sources previously described
- Create a video writer object.
- Use the video write object to save the video stream to disk.
``` C++
// Obtain frame size information using get() method
int frame_width = static_cast<int>(vid_capture.get(3)); // CAP_PROP_FRAME_WIDTH    
int frame_height = static_cast<int>(vid_capture.get(4)); // CAP_PROP_FRAME_HEIGHT
Size frame_size(frame_width,frame_height);
int fps = 20;
```
## Syntax
``` C++
VideoWriter(filename, apiPreference, fourcc, fps, frameSize[, isColor])
```
- `filename`: pathname for the output video file
- `apiPreference`:  API backends identifier
- `fourcc`: 4-character code of codec, used to compress the frames (fourcc)
- `fps`: Frame rate of the created video stream
- `frame_size`: Size of the video frames
- `isColor`: If not zero, the encoder will expect and encode color frames. Else it will work with grayscale frames (the flag is currently supported on Windows only).
For second argument for VideoWriter
```C++
VideoWriter::fourcc('M', 'J', 'P', 'G') // AVI 
VideoWriter::fourcc(*'XVID') // MP4
```
How to initialize video writer object
```c++
VideoWriter output('./res/output.avi', VideoWriter::fourcc('M', 'J', 'P', 'G'), frame_per_second, frame_size)
``` 
```C++
while (vid_capture.isOpened())
{
        // Initialize frame matrix
        Mat frame;

          // Initialize a boolean to check if frames are there or not
        bool isSuccess = vid_capture.read(frame);

        // If frames are not there, close it
        if (isSuccess == false)
        {
            cout << "Stream disconnected" << endl;
            break;
        }
        // If frames are present
        if(isSuccess == true)
        {
            //display frames
            output.write(frame);
                  // display frames
                  imshow("Frame", frame);
                  // wait for 20 ms between successive frames and break        
                  // the loop if key q is pressed
                  int key = waitKey(20);
                  if (key == 'q')
                  {
                      cout << "Key q key is pressed by the user. 
                      Stopping the video" << endl;
                      break;
                  }
        }
        vid_capture.release();
        output.release();
 }
```