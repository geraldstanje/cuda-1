CC=clang++ -std=c++11 -O2 -fsanitize=thread
NVCC=nvcc

all: multiDevice multiDevice.fatbin

multiDevice: multiDevice.o io_service_pool.o
	$(CC) -o $@ $^ -pthread -L${BOOST_ROOT}/lib -lboost_system -lboost_filesystem -L${CUDA_ROOT}/lib64 -lcuda

multiDevice.o: multiDevice.cpp
	$(CC) -o $@ $< -c -I${BOOST_ROOT} -I${CUDA_ROOT}/include

io_service_pool.o: io_service_pool.cpp
	$(CC) -o $@ $< -c -I${BOOST_ROOT}

multiDevice.fatbin: multiDevice.cu
	$(NVCC) -o $@ $< -arch=compute_11 -fatbin

clean:
	rm -f multiDevice multiDevice.o io_service_pool.o multiDevice.fatbin
