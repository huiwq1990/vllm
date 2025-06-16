

 

```shell

 docker buildx build \
  --build-arg http_proxy=http://172.17.0.1:7897 --build-arg https_proxy=http://172.17.0.1:7897 \
  --build-arg VLLM_CPU_DISABLE_AVX512="true" \
  --provenance=false --platform=linux/amd64 --push \
  -t hub.jdcloud.com/jdos-edge/vllm-openeuler22-amd64:v1.8.4 -f docker/Dockerfile.cpu .

```


```shell

docker pull registry.cn-beijing.aliyuncs.com/huiwq1990/public-vllm-cpu-env-v0.0.2 


docker run --rm \
  --privileged=true \
  --shm-size=4g \
  -p 8000:8000 \
  -e VLLM_USE_MODELSCOPE=true \
  -e VLLM_LOGGING_LEVEL=DEBUG \
  registry.cn-beijing.aliyuncs.com/huiwq1990/public-vllm-cpu-env-v0.0.2 \
  --model=facebook/opt-125m \
  --swap-space=0

```