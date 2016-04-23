###### �ӤH�ۻs²���оǡA�ȴ��Ψ䤤�X�ذ򥻥\��ϥ�

---

# Simple Makefile Tutorial

---
## Compile Program
�bLinux���ҤU�A��ڭ̷Q�ϥ�GNU Compiler�sĶC++�{���X�ɡA�|�b�R�O�C��J�G
```bash
    g++ -o out main.cpp
```
g++�OCompiler�W�١A-o out�N���X�ɮר�out�̡Amain.cpp �O��l�X�ɮסCCompile������A��J�G
```bash
    ./out
```
�Y�i�ϥθ��ɮסC

���Ѧ��h���ɮסAmain.cpp�Aresource.cpp�Aresource.h�A�h�ݧi�DCompiler�ڭ��٦���L�ɮסA���ɷ|��J�G
```bash
	g++ -o test main.cpp resource.cpp
```

�p�G�٦��ϥΨ�LLibrary���ɮסA�hCompile�L�{�A�ٻݭn�[�Jinclude���|�Blib���|�K���A�C���ݭn��J�����O�N�|�D�`�����A
���ɴN�i�H�ϥ�Makefile�Өϧڭ̨C����Compile��²��C

---
## Makefile
Makefile�èS������S�O���\��A�A�u�ݧ�A�|�Ψ쪺���O���g�i�h�A�M��C���ק粒��l�X�ݭn���sCompile���ɭԡA�u�n��J�A�]�w���N���N�i�H�i�樺�����O�C

�����b�A�{���X�Ҧb����Ƨ��A�إߤ@�ӷs�ɮסA�W��makefile�A�M��A�̭���J�G
```make
	all: main.cpp
	<Tab>g++ -o test main.cpp resource.cpp
```
all�O�@�Ӧۭq���N���A�b�_������J���ɮצW�١A�N�����ɮצ��ܧ�A�~�|�h�i��U�@�檺���O�C�ӤU�@�檺���O�A�����b�̫e����J�@��Tab�C

�s�ɫ�A�b�R�O�C��J`make`�άO`make all`�A�Y�i�����sĶ�ʧ@�C

�p�G�A���ѵ{�����ܦh�����A�i�H�bmakefile���Y����J�h���ۭq���O�A�Ҧp�G
```make
	all: main.cpp
	<Tab>g++ -o test main.cpp resource.cpp
	
	test: main.cpp
	<Tab>g++ -o test1 main.cpp resource2.cpp

	test2: main.cpp
	<Tab>g++ -o test2 main.cpp resource3.cpp
```
����b�sĶ�ɡA�N�i�H��ܡA`make all`��`make test`��`make test2`�A�ۤv�Q�n���ʧ@�C

�bMakefile���A�Y�����ƨϥΪ����O�A�i�Φۭq�ܼƥh�x�s�L�C
�ۭq�ܼƮɡA����J�ܼƦW�١A���ۦb�������[�W�L�����e�A�Ҧp�G
```make
	COMPILER = g++
	TARGET = test
	TARGET2 = test2
	SOURCE = main.cpp
	RESOURCE = resource.cpp
	RESOURCE2 = resource2.cpp
```
����n�ϥΦۭq�ܼƮɡA�ϥ����A���é�e��[�W`$`�Ÿ��A�Ҧp�G
```make
	all: $(SOURCE)
	<Tab>$(COMPILER) -o $(TARGET) $(SOURCE) $(RESOURCE)

	test: $(SOURCE)
	<Tab>$(COMPILER) -o $(TARGET2) $(SOURCE) $(RESOURCE2)
```
�M���J`make all`��`make test`�h�i��sĶ�C

---

## ����
### Compile OpenCV�{���X�ҥΪ�makefile�G
```make
CC = g++
INCLUDE = -I /usr/local/include -I /usr/include/opencv -I /usr/include/opencv2 -Wall -O2
LDFLAGS = -L /usr/lib/i386-linux-gnu/
LDLIBS = -lopencv_calib3d -lopencv_contrib -lopencv_core -lopencv_features2d -lopencv_flann -lopencv_highgui -lopencv_imgproc -lopencv_legacy -lopencv_ml -lopencv_objdetect -lopencv_video

opencv_test : opencv_test.cpp
	$(CC) -o opencv_test opencv_test.cpp $(INCLUDE) $(LDFLAGS) $(LDLIBS)
```

### Compile PCL�{���X�ҥΪ�makefile:
```make
CC = g++
INCLUDE = -I /usr/local/include/ -I /usr/local/include/pcl-1.8/ -I /usr/include/eigen3/ -I /usr/include/boost/ -I /usr/include/vtk-5.8/ -I /usr/include/qhull/ -I /usr/include/flann/ -I /usr/include/ni/
LDLIBS = -lpthread -lboost_system -lboost_filesystem -lboost_thread -lvtkCommon -lvtkFiltering -lOpenNI -lvtkRendering -lpcl_2d -lpcl_common -lpcl_cuda_features -lpcl_cuda_io -lpcl_cuda_sample_consensus -lpcl_cuda_segmentation -lpcl_features -lpcl_filters -lpcl_filters -lpcl_gpu_containers -lpcl_gpu_features -lpcl_gpu_kinfu_large_scale -lpcl_gpu_kinfu -lpcl_gpu_octree -lpcl_gpu_segmentation -lpcl_gpu_surface -lpcl_gpu_utils -lpcl_io -lpcl_kdtree -lpcl_keypoints -lpcl_octree -lpcl_registration -lpcl_sample_consensus -lpcl_search -lpcl_segmentation -lpcl_surface -lpcl_visualization

app : kinfu_app.cpp
	$(CC) -o pcl_kinfu kinfu_app.cpp evaluation.cpp $(INCLUDE) $(LDLIBS)
```
