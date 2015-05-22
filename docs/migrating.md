
## Updating Code from OpenCV 2.4.x to 3.0+

`This section is still under development.`

There are some changes made in the Python `cv2` interface in OpenCV 3.0 that will cause errors in some programs written for the older version (2.4.x).  It is recommended that you check the version installed at runtime (using `cv2.__version__`), and take appropriate action if an older version (< 3.0) is present.

Changes to the `cv2` module itself are discussed below, and should help with what changes need to be made to existing programs for them to run smoothly in newer versions of OpenCV (>= 3.0).

## Changes to the `cv2` Module

### Removal of Legacy `cv2.cv` Module

### Changes to Video I/O API
