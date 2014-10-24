StereoTest-Bundle
=================

Master project for tools I used for testing OpenCV's stereo vision. As a top-level project it is responsible for some boilerplate elements as well as finishing touch.

It requires a single file from OpenCV sources -- `stereo_calib.cpp` (in addition to compiled library). In OpenCV 2.4.9 (only officialy supported version) it is located in `samples/cpp` directory.

This tool bndle consists of:
 - program for acquisition of calibration data;
 - program for calibrating stereo camra;
 - program running stereo algorithm on live cameras feed or static images.

For details about included tools read their specific readmes.
