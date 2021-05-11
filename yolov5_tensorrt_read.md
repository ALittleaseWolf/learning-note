
```
# structure
├── CMakeLists.txt
├── coco.names
├── common
│   ├── common.cpp
│   ├── common.h
│   ├── common.hpp
│   ├── logging.h
│   ├── model.cpp
│   └── model.h
├── config6.yaml
├── config.yaml
├── export_onnx.py
├── main.cpp
├── README.md
├── samples(图片)
├── yaml-cpp(yaml工具)
├── yolov5.cpp
└── yolov5.h
```

> main.cpp

YOLOv5 YOLOv5(confile_file); 

YOLOv5.LoadEngine();
> yolov5.cpp


YOLOv5.InferenceFolder(folder_name);




