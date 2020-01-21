# waifu2x ncnn Vulkan

waifu2x에 불칸 api를 사용해서 "인텔 내장그래픽 / AMD 그래픽 / 엔비디아 그래픽 " 모두 사용하가능하게 만듬

waifu2x-ncnn-vulkan 은 [ncnn project](https://github.com/Tencent/ncnn)을 프레임 워크로 사용함, 흥미있다면 한번 봐보세요

## [Download](https://github.com/nihui/waifu2x-ncnn-vulkan/releases)

윈도우용 waifu2x-ncnn-vulkan 다운로드:

**https://github.com/nihui/waifu2x-ncnn-vulkan/releases**

패키지는 모델등 필요한 모듈들을 내장하고 있으니, CUDA 와 CUDNN 등이 필요 없음.


## 사용방법

### 사용 예시:

```shell

단일 파일 사용:
waifu2x-ncnn-vulkan.exe -i input.jpg -o output.png -n 2 -s 2


디렉토리안에 있는 모든 파일을 png 파일로 변경할 시:
waifu2x-ncnn-vulkan.exe -i C:\Users\amane\Desktop\ffmpeg\input\%05d.jpg -o C:\Users\amane\Desktop\ffmpeg\output\ - n 2 -s 2 -t 500


C:\Users\amane\Desktop\ffmpeg\input\ 에 들어있는 00001.jpg , 000002.jpg ... 들을 전부 업스케일링 하여서
C:\Users\amane\Desktop\ffmpeg\output\ 에 저장한다
```

### Full Usages

```console
Usage: waifu2x-ncnn-vulkan -i <input dir> -o <output dir> [options]...

  -h                  도움말
  -v                   verbose output
  -i input-path        input 경로
  -o output-path       output 으로 저장될 경로
  -n noise-level       디노이즈 단계 1/2/3 (디노이즈를 안하고 싶으면 -1 을 넣으면됨) 
  -s scale             X배로 부풀릴 단계, (현재 정수중 1,2 만 지원)
  -t tile-size         타일 크기 (>=32, default=400), GPU의 성능에 따라 크기를 조절하자
  -m model-path        업스케일의 모델의 경로
  -g gpu-id            GPU 장치 번호 선택 (default=0) , SLI나 크로스파이어 시 두개중 하나만 사용하고 싶을때 선택
  -j load:proc:save    thread count for load/proc/save (default=1:2:2)
```

- `input-path` 과 `output-path` 둘 다 단일 파일 혹은 선택한 디렉토리 안에 들어있는 파일 전부로 선택 가능
- `noise-level` = 디노이즈 레벨, (정수) 숫자가 커질수록 디노이즈 단계가 더 강하게 된다
- `scale` = scale level, 1=no scale, 2=upscale 2x
- `tile-size` = 타일크기, GPU의 성능에 따라서 크기를 조절 가능함
- `load:proc:save` = (load: 이미지 디코딩 , proc : 업스케일 , save: 이미지 인코딩) 사용 시 사용할 쓰레드 숫자를 정하는 패러미터. GPU의 성능에 따라서 조절 할 수 있다. 예를들어 4:4:4 는 해상도가 작은 여러 파일들을 프로세싱 할때, 2:2:2는 해상도가 큰 파일들을 프로세싱시 쓰면된다. 기본적으로 설정이 된 1:2:2 의 값은 거의 모든 상황에서 쓸 수 있지만 GPU의 리소스가 남을떄 더 빠른 프로세싱을 위해서, 반대로 리소스가 부족할시 값을 바꾸면 된다.

드라이버 오류가 날 시, 최신 드라이버로 업데이트 하는걸 권장함

- Intel: https://downloadcenter.intel.com/product/80939/Graphics-Drivers
- AMD: https://www.amd.com/en/support
- NVIDIA: https://www.nvidia.com/Download/index.aspx

WAIFU2x-CAFFE 보다 약 1.5배 정도 빠르다
