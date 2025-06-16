

 

```shell

 docker buildx build \
  --build-arg http_proxy=http://172.17.0.1:7897 --build-arg https_proxy=http://172.17.0.1:7897 \
  --build-arg VLLM_CPU_DISABLE_AVX512="true" \
  --provenance=false --platform=linux/amd64 --push \
  -t hub.jdcloud.com/jdos-edge/vllm-openeuler22-amd64:v1.8.4 -f docker/Dockerfile.cpu .

```


```shell

srcTag=vllm-cpu-env-qwen1
destTag=qwen1
docker pull registry.cn-beijing.aliyuncs.com/huiwq1990/public:${srcTag}
docker tag registry.cn-beijing.aliyuncs.com/huiwq1990/public:${srcTag} hub.jdcloud.com/jdos-edge/vllm-cpu-env:${destTag}
docker push hub.jdcloud.com/jdos-edge/vllm-cpu-env:${destTag}

docker run --rm \
  --privileged=true \
  --shm-size=15g \
  -p 8000:8000 \
  -e VLLM_LOGGING_LEVEL=DEBUG \
  hub.jdcloud.local/jdos-edge/vllm-cpu-env:qwen1 \
  --served-model-name=Qwen/Qwen2.5-VL-3B-Instruct \
  --model=/root/.cache/modelscope/hub/models/Qwen/Qwen2.5-VL-3B-Instruct \
  --swap-space=2 \
  --max_model_len=12800

```