###### 個人自製簡易教學，僅提及其中幾種基本功能使用

---

# Simple Makefile Tutorial

---
## Compile Program
在Linux環境下，當我們想使用GNU Compiler編譯C++程式碼時，會在命令列輸入：
```bash
    g++ -o out main.cpp
```
g++是Compiler名稱，-o out代表輸出檔案到out裡，main.cpp 是原始碼檔案。Compile完成後，輸入：
```bash
    ./out
```
即可使用該檔案。

當今天有多個檔案，main.cpp，resource.cpp，resource.h，則需告訴Compiler我們還有其他檔案，此時會輸入：
```bash
	g++ -o test main.cpp resource.cpp
```

如果還有使用其他Library的檔案，則Compile過程，還需要加入include路徑、lib路徑…等，每次需要輸入的指令就會非常冗長，
此時就可以使用Makefile來使我們每次的Compile變簡單。

---
## Makefile
Makefile並沒有什麼特別的功能，你只需把你會用到的指令先寫進去，然後每次修改完原始碼需要重新Compile的時候，只要鍵入你設定的代號就可以進行那項指令。

首先在你程式碼所在的資料夾，建立一個新檔案，名為makefile，然後再裡面輸入：
```make
	all: main.cpp
	<Tab>g++ -o test main.cpp resource.cpp
```
all是一個自訂的代號，在冒號後方輸入的檔案名稱，代表當其檔案有變更，才會去進行下一行的指令。而下一行的指令，必須在最前方鍵入一個Tab。

存檔後，在命令列輸入`make`或是`make all`，即可完成編譯動作。

如果你今天程式有很多版本，可以在makefile裡頭先輸入多項自訂指令，例如：
```make
	all: main.cpp
	<Tab>g++ -o test main.cpp resource.cpp
	
	test: main.cpp
	<Tab>g++ -o test1 main.cpp resource2.cpp

	test2: main.cpp
	<Tab>g++ -o test2 main.cpp resource3.cpp
```
之後在編譯時，就可以選擇，`make all`或`make test`或`make test2`，自己想要的動作。

在Makefile中，若有重複使用的指令，可用自訂變數去儲存他。
自訂變數時，先輸入變數名稱，接著在等號後方加上他的內容，例如：
```make
	COMPILER = g++
	TARGET = test
	TARGET2 = test2
	SOURCE = main.cpp
	RESOURCE = resource.cpp
	RESOURCE2 = resource2.cpp
```
之後要使用自訂變數時，使用雙括號並於前方加上`$`符號，例如：
```make
	all: $(SOURCE)
	<Tab>$(COMPILER) -o $(TARGET) $(SOURCE) $(RESOURCE)

	test: $(SOURCE)
	<Tab>$(COMPILER) -o $(TARGET2) $(SOURCE) $(RESOURCE2)
```
然後輸入`make all`或`make test`去進行編譯。

---

## 附錄
### Compile OpenCV程式碼所用的makefile：
```make
CC = g++
INCLUDE = -I /usr/local/include -I /usr/include/opencv -I /usr/include/opencv2 -Wall -O2
LDFLAGS = -L /usr/lib/i386-linux-gnu/
LDLIBS = -lopencv_calib3d -lopencv_contrib -lopencv_core -lopencv_features2d -lopencv_flann -lopencv_highgui -lopencv_imgproc -lopencv_legacy -lopencv_ml -lopencv_objdetect -lopencv_video

opencv_test : opencv_test.cpp
	$(CC) -o opencv_test opencv_test.cpp $(INCLUDE) $(LDFLAGS) $(LDLIBS)
```

### Compile PCL程式碼所用的makefile:
```make
CC = g++
INCLUDE = -I /usr/local/include/ -I /usr/local/include/pcl-1.8/ -I /usr/include/eigen3/ -I /usr/include/boost/ -I /usr/include/vtk-5.8/ -I /usr/include/qhull/ -I /usr/include/flann/ -I /usr/include/ni/
LDLIBS = -lpthread -lboost_system -lboost_filesystem -lboost_thread -lvtkCommon -lvtkFiltering -lOpenNI -lvtkRendering -lpcl_2d -lpcl_common -lpcl_cuda_features -lpcl_cuda_io -lpcl_cuda_sample_consensus -lpcl_cuda_segmentation -lpcl_features -lpcl_filters -lpcl_filters -lpcl_gpu_containers -lpcl_gpu_features -lpcl_gpu_kinfu_large_scale -lpcl_gpu_kinfu -lpcl_gpu_octree -lpcl_gpu_segmentation -lpcl_gpu_surface -lpcl_gpu_utils -lpcl_io -lpcl_kdtree -lpcl_keypoints -lpcl_octree -lpcl_registration -lpcl_sample_consensus -lpcl_search -lpcl_segmentation -lpcl_surface -lpcl_visualization

app : kinfu_app.cpp
	$(CC) -o pcl_kinfu kinfu_app.cpp evaluation.cpp $(INCLUDE) $(LDLIBS)
```
