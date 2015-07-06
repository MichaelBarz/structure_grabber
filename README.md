#structure_grabber

Grabber for [Structure Sensor](http://structure.io/) (Depth and Infrared) using [OpenNI2](http://structure.io/openni) (optionally, [OpenCV](http://opencv.org/) and [PointCloudLibrary](http://pointclouds.org/))

##Requirement

* [OpenNI2](http://structure.io/openni)
* [OpenCV 3](http://opencv.org/)
* [PointCloudLibrary (PCL)](http://pointclouds.org/) or use this [installer](http://unanancyowen.com/?p=1255&lang=en)
* [CMake](http://www.cmake.org/)

## Usage

### Preparation

1. Create the project by `cmake`
2. Edit the file `CMakeLists.txt`: Edit the OpenCV folders according to your OpenCV installation

### Basic

1. Include "structure_grabber.h".
2. To start, write:
```
StructureGrabber grabber;
grabber.open();
```
3. To capture, write:
```
grabber.acquire();
```
4. To get raw data, write:
```
unsigned short *depth_data, *infrared_data;
grabber.copyDepthDataTo(depth_data);
grabber.copyInfraredDataTo(infrared_data);
```

### With OpenCV

1. Include OpenCV headers before including "structure_grabber.h".
2. To get `IplImage` or `cv::Mat`, write:
```
cv::Mat depth_image, infrared_image;
grabber.acquire();
grabber.copyDepthImageTo(depth_image);
grabber.copyInfraredImageTo(infrared_image)
```

### With PCL

1. Include PCL headers before including "structure_grabber.h".
2. To get `pcl::PointCloud`, write:
```
pcl::PointCloud<pcl::PointXYZ> cloud;
grabber.acquire();
grabber.copyPointCloudTo(cloud);
```


&copy; 2014 kenken.
