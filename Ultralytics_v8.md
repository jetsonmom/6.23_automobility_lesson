# YOLO 모델 성능 비교 및 YOLOv8 특징

## YOLO 모델들의 성능 비교

### 차트 분석 개요

| 구분 | 왼쪽 그래프 | 오른쪽 그래프 |
|------|-------------|---------------|
| **측정 기준** | 모델 크기 vs 정확도 | 추론 속도 vs 정확도 |
| **X축** | Parameters (M) - 매개변수 수 (백만) | Latency A100 TensorRT FP16 (ms/img) |
| **Y축** | COCO mAP50-95 - 객체 검출 정확도 | COCO mAP50-95 - 객체 검출 정확도 |
| **최적화 방향** | Smaller (작은 모델) | Faster (빠른 추론) |

### 성능 비교 결과

| 모델 버전 | 모델 크기 성능 | 추론 속도 성능 | 종합 평가 |
|-----------|----------------|----------------|-----------|
| **YOLOv8** | 🥇 최우수 | 🥇 최우수 | ⭐⭐⭐⭐⭐ |
| **YOLOv7** | 🥈 우수 | 🥈 우수 | ⭐⭐⭐⭐ |
| **YOLOv6-2.0** | 🥉 양호 | 🥉 양호 | ⭐⭐⭐ |
| **YOLOv5-7.0** | 📈 기준 | 📈 기준 | ⭐⭐ |

### 핵심 결론

| 평가 항목 | YOLOv8 성능 | 비고 |
|-----------|-------------|------|
| **효율성** | 작은 모델 크기로 높은 정확도 | 메모리 사용량 최적화 |
| **속도** | 빠른 추론 시간 | 실시간 처리 가능 |
| **정확도** | 최고 수준의 mAP 점수 | 객체 검출 성능 우수 |
| **종합** | 모든 면에서 이전 버전 대비 개선 | 실용성 최고 |

---

## YOLOv8 주요 기능

| 기능 | 설명 | 장점 |
|------|------|------|
| **고급 백본 및 넥 아키텍처** | 최첨단 백본 및 넥 아키텍처 채택 | 특징 추출 및 객체 감지 성능 향상 |
| **앵커 프리 스플릿 Ultralytics 헤드** | 앵커 프리 방식의 새로운 헤드 구조 | 앵커 기반 대비 더 나은 정확도와 효율성 |
| **최적화된 정확도-속도 트레이드오프** | 정확도와 속도의 최적 균형 | 실시간 물체 감지 작업에 적합 |
| **다양한 사전 학습 모델** | 여러 작업별 사전 학습 모델 제공 | 특정 사용 사례에 맞는 모델 선택 가능 |

---

## 교육 활용 권장사항

### YOLOv8의 교육적 장점

| 항목 | 특징 | 교육 효과 |
|------|------|-----------|
| **사용 편의성** | 간단한 API 제공 | 🎯 빠른 학습 곡선 |
| **우수한 성능** | 최신 기술 적용 | 📈 높은 학습 동기 부여 |
| **실시간 처리** | 빠른 추론 속도 | 🚀 즉각적인 결과 확인 |
| **풍부한 자료** | 많은 튜토리얼과 예제 | 📚 자기주도적 학습 지원 |

### 자율주행 학습 단계별 추천

| 학습 단계 | 대상 객체 | 난이도 | 비고 |
|-----------|-----------|--------|------|
| **1단계** | 신호등 인식 | ⭐ 쉬움 | 전세계 공통 표준 |
| **2단계** | 차량 인식 | ⭐⭐ 보통 | 형태가 비교적 단순 |
| **3단계** | 표지판 인식 | ⭐⭐⭐ 어려움 | 한국 특화 데이터 필요 |
| **4단계** | 통합 시스템 | ⭐⭐⭐⭐ 고급 | 실제 자율주행 구현 |

---

## YOLOv8 지원 작업 및 모드

### 개요
YOLOv8 시리즈는 컴퓨터 비전의 특정 작업에 특화된 다양한 모델을 제공합니다. 객체 감지부터 인스턴스 분할, 포즈/키포인트 감지, 방향성 객체 감지 및 분류까지 다양한 요구 사항을 충족하도록 설계되었습니다.

### 모델 변형별 지원 기능

| 모델 | 모델 파일 | 작업 | 추론 | 검증 | 교육 | 내보내기 |
|------|-----------|------|------|------|------|----------|
| **YOLOv8** | `yolov8n.pt` `yolov8s.pt` `yolov8m.pt` `yolov8l.pt` `yolov8x.pt` | 객체 탐지 | ✅ | ✅ | ✅ | ✅ |
| **YOLOv8-seg** | `yolov8n-seg.pt` `yolov8s-seg.pt` `yolov8m-seg.pt` `yolov8l-seg.pt` `yolov8x-seg.pt` | 인스턴스 세분화 | ✅ | ✅ | ✅ | ✅ |
| **YOLOv8-pose** | `yolov8n-pose.pt` `yolov8s-pose.pt` `yolov8m-pose.pt` `yolov8l-pose.pt` `yolov8x-pose.pt` `yolov8x-pose-p6.pt` | 포즈/키포인트 | ✅ | ✅ | ✅ | ✅ |
| **YOLOv8-obb** | `yolov8n-obb.pt` `yolov8s-obb.pt` `yolov8m-obb.pt` `yolov8l-obb.pt` `yolov8x-obb.pt` | 방향 탐지 | ✅ | ✅ | ✅ | ✅ |
| **YOLOv8-cls** | `yolov8n-cls.pt` `yolov8s-cls.pt` `yolov8m-cls.pt` `yolov8l-cls.pt` `yolov8x-cls.pt` | 분류 | ✅ | ✅ | ✅ | ✅ |

### 모델 크기별 특징

| 모델 크기 | 설명 | 용도 | 성능 특성 |
|-----------|------|------|-----------|
| **n (nano)** | 가장 작고 빠른 모델 | 모바일, 임베디드 | 낮은 정확도, 높은 속도 |
| **s (small)** | 작은 크기의 균형 모델 | 실시간 애플리케이션 | 적당한 정확도와 속도 |
| **m (medium)** | 중간 크기의 표준 모델 | 일반적인 용도 | 균형 잡힌 성능 |
| **l (large)** | 큰 크기의 고성능 모델 | 높은 정확도 필요 시 | 높은 정확도, 느린 속도 |
| **x (extra large)** | 가장 크고 정확한 모델 | 최고 성능 필요 시 | 최고 정확도, 가장 느림 |

### 자율주행 분야 활용 예시

| 작업 유형 | 자율주행 적용 | 추천 모델 | 활용 사례 |
|-----------|---------------|-----------|----------|
| **객체 탐지** | 차량, 신호등, 표지판 인식 | YOLOv8m | 기본 객체 검출 |
| **인스턴스 세분화** | 도로, 차선 정확한 영역 구분 | YOLOv8-seg | 정밀한 영역 분할 |
| **포즈/키포인트** | 보행자 자세 인식 | YOLOv8-pose | 보행자 행동 예측 |
| **방향 탐지** | 주차된 차량의 방향 인식 | YOLOv8-obb | 복잡한 주차 환경 |
| **분류** | 교통 표지판 종류 분류 | YOLOv8-cls | 표지판 세부 분류 |

---

## YOLOv8 성능 벤치마크

# YOLOv8 성능 벤치마크

## COCO 데이터셋 탐지 성능

| 모델 | 크기 (픽셀) | mAPval 50-95 | 속도 CPU ONNX (ms) | 속도 A100 TensorRT (ms) | 매개변수 (M) | FLOPs (B) | 다운로드 |
|------|-------------|--------------|-------------------|------------------------|-------------|-----------|----------|
| **YOLOv8n** | 640 | 37.3 | 80.4 | 0.99 | 3.2 | 8.7 | [📥 yolov8n.pt](https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8n.pt) |
| **YOLOv8s** | 640 | 44.9 | 128.4 | 1.20 | 11.2 | 28.6 | [📥 yolov8s.pt](https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8s.pt) |
| **YOLOv8m** | 640 | 50.2 | 234.7 | 1.83 | 25.9 | 78.9 | [📥 yolov8m.pt](https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8m.pt) |
| **YOLOv8l** | 640 | 52.9 | 375.2 | 2.39 | 43.7 | 165.2 | [📥 yolov8l.pt](https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8l.pt) |
| **YOLOv8x** | 640 | 53.9 | 479.1 | 3.53 | 68.2 | 257.8 | [📥 yolov8x.pt](https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8x.pt) |

> 💡 **참고**: 사전 학습된 80개의 클래스를 포함하여 COCO에서 학습된 모델입니다.

> 💡 **참고**: 사전 학습된 80개의 클래스를 포함하여 COCO에서 학습된 모델입니다. 자세한 사용 예제는 [탐지 문서](https://docs.ultralytics.com/tasks/detect/)를 참조하세요.

### 성능 지표 설명

| 지표 | 설명 | 의미 |
|------|------|------|
| **mAPval 50-95** | 평균 정밀도 (IoU 0.5-0.95) | 높을수록 정확도 우수 |
| **속도 CPU ONNX** | CPU에서의 추론 시간 | 낮을수록 빠른 처리 |
| **속도 A100 TensorRT** | GPU에서의 추론 시간 | 낮을수록 빠른 처리 |
| **매개변수** | 모델의 파라미터 수 | 적을수록 메모리 효율적 |
| **FLOPs** | 부동소수점 연산 수 | 적을수록 연산 효율적 |

---

## YOLOv8 사용 예시

### Python 코드 예제

```python
from ultralytics import YOLO

# COCO 사전 훈련된 YOLOv8n 모델 로드
model = YOLO("yolov8n.pt")

# 모델 정보 표시 (선택사항)
model.info()

# COCO8 예제 데이터셋으로 100 에포크 훈련
results = model.train(data="coco8.yaml", epochs=100, imgsz=640)

# 'xxx.jpg' 사진을 다운로드하고 경로를 넣어준다.이미지에  대해 YOLOv8n 모델로 추론 실행
results = model("path/to/xxx.jpg")
```
colab test code
```
# 라이브러리 설치
!pip install ultralytics # 사진 업로드
from google.colab import files
from ultralytics import YOLO # COCO 사전 훈련된 YOLOv8n 모델 로드
model = YOLO("yolov8n.pt") # 모델 정보 표시 (선택사항)
model.info() # COCO8 예제 데이터셋으로 100 에포크 훈련
results = model.train(data="coco8.yaml", epochs=10, imgsz=640) # 사진 업로드하고 경로 설정
uploaded = files.upload()
image_path = list(uploaded.keys())[0] # 업로드한 이미지에 대해 YOLOv8n 모델로 추론 실행
results = model(image_path)
results[0].show()
```
### CLI 명령어 예제

## YOLOv8 CLI 명령어 가이드

### 개요
YOLOv8 CLI 명령어들은 각각 **다른 목적**으로 사용하는 명령어들입니다.

### 단계별 사용 순서

#### 📚 **1단계: Train (학습)** 
```bash
yolo detect train data=coco8.yaml model=yolov8n.pt epochs=100 imgsz=640
```
- **목적**: 새로운 데이터로 모델을 훈련시킬 때
- **예시**: 한국 도로 표지판 학습
- **사용 시기**: 커스텀 데이터셋으로 모델을 개선하고 싶을 때

#### 🔍 **2단계: Predict (추론)**
```bash
yolo detect predict model=yolov8n.pt source="your_image.jpg"
```
- **목적**: 실제로 이미지 분석할 때 (가장 많이 사용)
- **예시**: 업로드한 사진에서 차량/신호등 찾기
- **사용 시기**: 완성된 모델로 실제 객체 탐지를 수행할 때

#### 📊 **3단계: Val (검증)**
```bash
yolo detect val model=yolov8n.pt data=coco8.yaml
```
- **목적**: 모델이 얼마나 정확한지 확인할 때
- **예시**: mAP, 정확도, 재현율 등 성능 지표 측정
- **사용 시기**: 모델 성능을 객관적으로 평가하고 싶을 때

#### 📦 **4단계: Export (배포)**
```bash
yolo detect export model=yolov8n.pt format=onnx
```
- **목적**: 완성된 모델을 다른 환경에서 사용할 수 있게 변환
- **예시**: ONNX, TensorRT, CoreML 등 다양한 형식으로 변환
- **사용 시기**: 모바일 앱이나 웹 서비스에 모델을 배포할 때

### Google Colab에서 실행하기

#### 설치 및 기본 설정
```bash
# 라이브러리 설치
!pip install ultralytics

# 각 명령어 앞에 '!' 추가하여 실행
!yolo detect train data=coco8.yaml model=yolov8n.pt epochs=100 imgsz=640
!yolo detect predict model=yolov8n.pt source="your_image.jpg"
!yolo detect val model=yolov8n.pt data=coco8.yaml
!yolo detect export model=yolov8n.pt format=onnx
```

### 학습 단계별 권장사항

| 학습 단계 | 주요 사용 명령어 | 설명 |
|-----------|------------------|------|
| **초급** | `predict` | 사전 훈련된 모델로 객체 탐지 체험 |
| **중급** | `train` + `predict` | 커스텀 데이터로 모델 학습 후 테스트 |
| **고급** | 전체 워크플로우 | 학습 → 검증 → 배포까지 전 과정 |

### 자율주행 프로젝트 적용 예시

### 실습 수업에서
- **주로 사용**: `predict` 명령어
- **목적**: 학생들이 직접 사진을 업로드해서 객체 탐지 체험

### 프로젝트 개발에서
- **전체 워크플로우** 사용
- **순서**: Train → Val → Predict → Export

## 주의사항
- **Train**: 시간이 오래 걸리므로 처음에는 epochs를 10-20으로 설정
- **Predict**: 가장 자주 사용하는 명령어
- **Val**: 모델 성능 비교시 유용
- **Export**: 최종 배포 단계에서 사용

> 💡 **팁**: 학생들과 실습할 때는 **Predict**만 주로 사용하고, 나머지는 고급 과정에서 배우면 됩니다!
colab cli명령
```
# 모델 훈련
!yolo detect train data=coco8.yaml model=yolov8n.pt epochs=10 imgsz=640

# 추론 실행 (업로드한 이미지 경로로 변경)
!yolo detect predict model=yolov8n.pt source="your_uploaded_image.jpg"

# 모델 검증
!yolo detect val model=yolov8n.pt data=coco8.yaml

# 모델 내보내기
!yolo detect export model=yolov8n.pt format=onnx

```

### 지원되는 작업별 사용법

| 작업 | 모델 파일 | 사용 예시 | 문서 링크 |
|------|-----------|-----------|----------|
| **객체 탐지** | `yolov8n.pt` | `YOLO("yolov8n.pt")` | [Detection](https://docs.ultralytics.com/tasks/detect/) |
| **세그멘테이션** | `yolov8n-seg.pt` | `YOLO("yolov8n-seg.pt")` | [Segmentation](https://docs.ultralytics.com/tasks/segment/) |
| **분류** | `yolov8n-cls.pt` | `YOLO("yolov8n-cls.pt")` | [Classification](https://docs.ultralytics.com/tasks/classify/) |
| **포즈 추정** | `yolov8n-pose.pt` | `YOLO("yolov8n-pose.pt")` | [Pose](https://docs.ultralytics.com/tasks/pose/) |
| **방향 탐지** | `yolov8n-obb.pt` | `YOLO("yolov8n-obb.pt")` | [OBB](https://docs.ultralytics.com/tasks/obb/) |
