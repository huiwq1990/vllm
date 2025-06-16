

 

```shell

 docker buildx build \
  --build-arg http_proxy=http://172.17.0.1:7897 --build-arg https_proxy=http://172.17.0.1:7897 \
  --build-arg VLLM_CPU_DISABLE_AVX512="true" \
  --provenance=false --platform=linux/amd64 --push \
  -t hub.jdcloud.com/jdos-edge/vllm-openeuler22-amd64:v1.8.4 -f docker/Dockerfile.cpu .

```