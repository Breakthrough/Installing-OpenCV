
## Migrating Code from OpenCV 2.4.x to 3.0+

There are some changes made in the Python `cv2` interface in OpenCV 3.0 that will cause errors in some programs written for older versions (OpenCV 2.4.11 and prior).  Changes to the `cv2` module itself are discussed below, and should demonstrate what changes need to be made to existing programs for them to run properly with newer versions of OpenCV (`>= 3.0.0`).

It is recommended that you check the version installed at runtime (using `cv2.__version__`), and take appropriate action if an older version is present - anything prior to OpenCV 3.0 - and you happen to use some of the constructs which were changed.

Note that this section of the document is still under development, and more differences will be added as they are found.  Viewing all properties of the `cv2` module (using `dir(cv2)` in a Python shell) is helpful.

------------------------------------------------------

## Changes to the `cv2` Module


------------------------------------------------------

#### Removal of Legacy `cv2.cv` Module

Any code referencing `cv2.cv` must be changed to work with OpenCV 3.0.  Most of the constants that were defined there, however, have simply been moved directly into the `cv2` module.  In some cases, you can simply replace instances of `cv2.cv` with `cv2`.  For example:

```python
cap = cv2.VideoCapture("some_video.mp4")

# Pre-3.0 Way (<= OpenCV 2.4.11) - WILL NOT WORK ANYMORE
framerate = cap.get(cv2.cv.CV_CAP_PROP_FPS)

# New Way (OpenCV >= 3.0)
framerate = cap.get(cv.CV_CAP_PROP_FPS)
```

------------------------------------------------------


#### Changes to Video I/O API

When setting the FourCC codec ID, there is no cv2.CV_FOURCC anymore.  This appears to be a capture property that must be set with the VideoCapture `set` method now.
