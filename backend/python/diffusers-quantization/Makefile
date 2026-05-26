export CONDA_ENV_PATH = "diffusers-quantization.yml"

ifeq ($(BUILD_TYPE), hipblas)
export CONDA_ENV_PATH = "diffusers-quantization-rocm.yml"
endif

# Intel GPU are supposed to have dependencies installed in the main python
# environment, so we skip conda installation for SYCL builds.
# https://github.com/intel/intel-extension-for-pytorch/issues/538
ifneq (,$(findstring sycl,$(BUILD_TYPE)))
export SKIP_CONDA=1
endif

.PHONY: diffusers-quantization
diffusers-quantization:
	bash install.sh

.PHONY: run
run: diffusers-quantization
	@echo "Running diffusers-quantization..."
	bash run.sh
	@echo "diffusers-quantization run."

test: diffusers-quantization
	bash test.sh

.PHONY: protogen-clean
protogen-clean:
	$(RM) backend_pb2_grpc.py backend_pb2.py

.PHONY: clean
clean: protogen-clean
	rm -rf venv __pycache__