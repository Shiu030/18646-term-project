HOST_COMPILER  = g++
NVCC           = nvcc

SRCS = main.cu
INCS = vec3.h ray.h hitable.h hitable_list.h sphere.h camera.h material.h

cudart: cudart.o
	$(NVCC) -o cudart cudart.o

cudart.o: $(SRCS) $(INCS)
	$(NVCC) -o cudart.o -c main.cu

out.ppm: cudart
	rm -f out.ppm
	./cudart > out.ppm

out.jpg: out.ppm
	rm -f out.jpg
	ppmtojpeg out.ppm > out.jpg

profile_basic: cudart
	nvprof ./cudart > out.ppm

# use nvprof --query-metrics
profile_metrics: cudart
	nvprof --metrics achieved_occupancy,inst_executed,inst_fp_32,inst_fp_64,inst_integer ./cudart > out.ppm

clean:
	rm -f cudart cudart.o out.ppm out.jpg
