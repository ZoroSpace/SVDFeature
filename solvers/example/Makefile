# Makefile for SVDFeature customization

# !!specify HOME PATH
PRJ=../..
export CC  = gcc
export CXX = g++
export CFLAGS = -Wall -O3 -msse2 

# !! change the name of customized code
BIN = svdf_lite svdf_lite_infer 
OBJ = apex_svd.o apex_svd_data.o
.PHONY: clean all

all: $(BIN)
export LDFLAGS= -pthread -lm 

# !! use apex_svd_lite.cpp for customized solver
apex_svd.o:apex_svd_lite.cpp $(PRJ)/apex_svd.h $(PRJ)/apex_svd_model.h $(PRJ)/apex_svd_data.h 
# !! reuse input component of SVDFeature
apex_svd_data.o:$(PRJ)/apex_svd_data.cpp $(PRJ)/apex_svd_data.h

svdf_lite:$(PRJ)/svd_feature.cpp apex_svd.o apex_svd_data.o $(PRJ)/apex_svd_data.h $(PRJ)/apex_svd.h 
svdf_lite_infer:$(PRJ)/svd_feature_infer.cpp apex_svd.o apex_svd_data.o $(PRJ)/apex_svd_data.h $(PRJ)/apex_svd.h 

$(BIN) : 
	$(CXX) $(CFLAGS) $(LDFLAGS) -o $@ $(filter %.cpp %.o %.c, $^)

$(OBJ) : 
	$(CXX) -c $(CFLAGS) -o $@ $(filter %.cpp %.c, $^)

clean:
	$(RM) $(OBJ) $(BIN) *~

