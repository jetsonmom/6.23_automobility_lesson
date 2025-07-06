# 자율주행 지도학습 샘플 코드

## 🏗️ 전체 구조

### 클래스: `RealImageTrafficSignRecognition`
- 교통표지판 인식을 위한 모든 기능을 담은 클래스

## 🧩 주요 함수들

### 1️⃣ `__init__(self)`
```python
def __init__(self):
    self.model = None  # CNN 모델을 저장할 변수
```
- 클래스 초기화
- 모델 변수를 None으로 설정

### 2️⃣ `build_cnn_model(self)`
```python
model = models.Sequential([
    layers.Conv2D(32, (3, 3), activation='relu', input_shape=(64, 64, 3)),
    layers.BatchNormalization(),
    layers.MaxPooling2D((2, 2)),
    # ... 더 많은 레이어들
])
```
**역할**: CNN 신경망 구조 설계
- **Conv2D**: 이미지 특징 추출 (32개, 64개, 128개 필터)
- **BatchNormalization**: 학습 안정화
- **MaxPooling2D**: 이미지 크기 축소
- **Dropout**: 과적합 방지
- **Dense**: 최종 분류 (4개 클래스)

### 3️⃣ `generate_realistic_training_data(self)`
```python
for class_id in range(4):  # 4개 클래스
    for _ in range(125):   # 클래스당 125개 = 총 500개
        image = np.random.rand(64, 64, 3)  # 랜덤 이미지 생성
        
        if class_id == 0:  # 정지표지판
            image[:, :, 0] = np.random.uniform(0.7, 1.0, (64, 64))  # 빨간색
```
**역할**: 가상의 훈련 데이터 생성
- **정지**:빨간색
- **직진**:파란색 계열  
- **좌회전**: ** 파란색 계열  **
- **우회전**:   노란색 계열

### 4️⃣ `train_model(self)`
```python
# 데이터 생성
images, labels = self.generate_realistic_training_data()

# 훈련/테스트 분할
X_train, X_test, y_train, y_test = train_test_split(...)

# 모델 훈련
history = self.model.fit(X_train, y_train, epochs=15, ...)
```
**역할**: 실제 모델 훈련
- 500개 가상 이미지 생성
- 80% 훈련용, 20% 테스트용으로 분할
- 15번 에포크 훈련
- 최종 정확도 출력

### 5️⃣ `upload_and_predict(self)`
```python
uploaded = files.upload()  # 파일 업로드

# 이미지 전처리
processed_image = cv2.resize(image_array, (64, 64))
processed_image_norm = processed_image.astype(np.float32) / 255.0

# 예측
predictions = self.model.predict(input_image, verbose=0)
```
**역할**: 실제 이미지 업로드 및 예측
- 업로드 창 표시
- 이미지 크기를 64x64로 조정
- 0-1 범위로 정규화
- CNN 모델로 예측
- 3개 그래프로 시각화

## 🔄 실행 흐름

### main() 함수
```python
1. recognizer = RealImageTrafficSignRecognition()  # 객체 생성
2. recognizer.show_sample_images()                # 사용법 안내
3. history, accuracy = recognizer.train_model()   # 모델 훈련
4. while True:                                    # 반복 테스트
   recognizer.upload_and_predict()               # 이미지 업로드 & 예측
```

## 🎯 핵심 개념

### 지도학습 요소
- **데이터**: 이미지 + 라벨 (0:정지, 1:직진, 2:좌회전, 3:우회전)
- **훈련**: 정답이 있는 데이터로 학습
- **예측**: 새로운 이미지의 클래스 분류

### CNN 구조
```
입력(64x64x3) → Conv2D → MaxPool → Conv2D → MaxPool → 
Conv2D → Flatten → Dense → Dropout → Dense(4) → 출력
```

### 데이터 전처리
1. **크기 조정**: 다양한 크기 → 64x64 고정
2. **정규화**: 0-255 픽셀값 → 0-1 범위
3. **배치 차원**: (64,64,3) → (1,64,64,3)

## 💡 왜 이렇게 만들었나?

1. **색상 기반 학습**: 실제 교통표지판의 색상 특징 활용
2. **간단한 구조**: 학습용으로 이해하기 쉽게
3. **시각화 포함**: 결과를 명확하게 확인
4. **반복 테스트**: 여러 이미지로 계속 실험 가능

이 코드는 **교육용 지도학습 데모**로, 실제 교통표지판 인식보다는 **CNN과 지도학습의 개념**을 이해하는 데 목적이 있어요! 😊
  

## 코드

```
# 실제 이미지 업로드해서 교통표지판 인식하기!

!pip install opencv-python tensorflow scikit-learn matplotlib pillow

import cv2
import numpy as np
import tensorflow as tf
from tensorflow.keras import layers, models
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt
from google.colab import files
import io
from PIL import Image
import os

class RealImageTrafficSignRecognition:
    def __init__(self):
        self.model = None
        
    def build_cnn_model(self):
        """CNN 모델 구축"""
        model = models.Sequential([
            layers.Conv2D(32, (3, 3), activation='relu', input_shape=(64, 64, 3)),
            layers.BatchNormalization(),
            layers.MaxPooling2D((2, 2)),
            
            layers.Conv2D(64, (3, 3), activation='relu'),
            layers.BatchNormalization(),
            layers.MaxPooling2D((2, 2)),
            
            layers.Conv2D(128, (3, 3), activation='relu'),
            layers.BatchNormalization(),
            layers.Dropout(0.25),
            
            layers.Flatten(),
            layers.Dense(512, activation='relu'),
            layers.BatchNormalization(),
            layers.Dropout(0.5),
            layers.Dense(4, activation='softmax')  # 4개 클래스
        ])
        
        model.compile(
            optimizer='adam',
            loss='sparse_categorical_crossentropy',
            metrics=['accuracy']
        )
        return model
    
    def generate_realistic_training_data(self):
        """더 현실적인 훈련 데이터 생성"""
        np.random.seed(42)
        images = []
        labels = []
        
        for class_id in range(4):
            for _ in range(125):  # 클래스당 125개
                # 64x64 이미지 생성
                image = np.random.rand(64, 64, 3)
                
                if class_id == 0:  # 정지 표지판 (빨간색)
                    # 빨간 배경
                    image[:, :, 0] = np.random.uniform(0.7, 1.0, (64, 64))
                    image[:, :, 1] = np.random.uniform(0.0, 0.2, (64, 64))
                    image[:, :, 2] = np.random.uniform(0.0, 0.2, (64, 64))
                    
                elif class_id == 1:  # 직진 (파란색)
                    # 파란 배경
                    image[:, :, 0] = np.random.uniform(0.0, 0.2, (64, 64))
                    image[:, :, 1] = np.random.uniform(0.0, 0.2, (64, 64))
                    image[:, :, 2] = np.random.uniform(0.7, 1.0, (64, 64))
                    
                elif class_id == 2:  # 좌회전 (초록색)
                    # 초록 배경
                    image[:, :, 0] = np.random.uniform(0.0, 0.2, (64, 64))
                    image[:, :, 1] = np.random.uniform(0.7, 1.0, (64, 64))
                    image[:, :, 2] = np.random.uniform(0.0, 0.2, (64, 64))
                    
                else:  # 우회전 (노란색)
                    # 노란 배경
                    image[:, :, 0] = np.random.uniform(0.8, 1.0, (64, 64))
                    image[:, :, 1] = np.random.uniform(0.8, 1.0, (64, 64))
                    image[:, :, 2] = np.random.uniform(0.0, 0.3, (64, 64))
                
                images.append(image)
                labels.append(class_id)
        
        return np.array(images), np.array(labels)
    
    def train_model(self):
        """모델 훈련"""
        print("🚀 교통표지판 인식 모델 훈련 시작!")
        print("=" * 50)
        
        # 훈련 데이터 생성
        images, labels = self.generate_realistic_training_data()
        
        # 데이터 분할
        X_train, X_test, y_train, y_test = train_test_split(
            images, labels, test_size=0.2, random_state=42, stratify=labels
        )
        
        print(f"📊 훈련 데이터: {len(X_train)}개")
        print(f"📊 테스트 데이터: {len(X_test)}개")
        
        # 모델 생성
        self.model = self.build_cnn_model()
        
        # 훈련
        print("\n🏋️ 모델 훈련 중...")
        history = self.model.fit(
            X_train, y_train,
            epochs=15,
            batch_size=32,
            validation_data=(X_test, y_test),
            verbose=1
        )
        
        # 최종 평가
        test_loss, test_accuracy = self.model.evaluate(X_test, y_test, verbose=0)
        print(f"\n✅ 훈련 완료!")
        print(f"🎯 최종 정확도: {test_accuracy:.1%}")
        print("=" * 50)
        
        return history, test_accuracy
    
    def upload_and_predict(self):
        """이미지 업로드하고 예측하기"""
        print("\n📷 교통표지판 사진을 업로드해주세요!")
        print("(정지, 직진, 좌회전, 우회전 표지판이면 더 좋아요!)")
        print("-" * 50)
        
        # 파일 업로드
        uploaded = files.upload()
        
        if not uploaded:
            print("❌ 업로드된 파일이 없습니다.")
            return
        
        for filename, file_data in uploaded.items():
            print(f"\n🔍 '{filename}' 분석 중...")
            
            try:
                # 이미지 로드
                image = Image.open(io.BytesIO(file_data))
                
                # RGB로 변환
                if image.mode != 'RGB':
                    image = image.convert('RGB')
                
                # 원본 이미지 표시
                plt.figure(figsize=(15, 5))
                
                # 1. 원본 이미지
                plt.subplot(1, 3, 1)
                plt.imshow(image)
                plt.title(f'📷 업로드된 이미지\n({filename})', fontsize=12)
                plt.axis('off')
                
                # 2. 전처리된 이미지
                image_array = np.array(image)
                processed_image = cv2.resize(image_array, (64, 64))
                processed_image_norm = processed_image.astype(np.float32) / 255.0
                
                plt.subplot(1, 3, 2)
                plt.imshow(processed_image)
                plt.title('🔧 전처리된 이미지\n(64x64 크기)', fontsize=12)
                plt.axis('off')
                
                # 3. 예측 수행
                input_image = np.expand_dims(processed_image_norm, axis=0)
                predictions = self.model.predict(input_image, verbose=0)
                
                # 결과 분석
                class_names = ['🛑 정지', '⬆️ 직진', '↩️ 좌회전', '↪️ 우회전']
                predicted_class = np.argmax(predictions[0])
                confidence = np.max(predictions[0])
                
                # 예측 결과 시각화
                plt.subplot(1, 3, 3)
                colors = ['red', 'blue', 'green', 'orange']
                bars = plt.bar(range(4), predictions[0], color=colors, alpha=0.7)
                
                # 가장 높은 확률 강조
                bars[predicted_class].set_alpha(1.0)
                bars[predicted_class].set_edgecolor('black')
                bars[predicted_class].set_linewidth(3)
                
                plt.title(f'🎯 예측 결과\n{class_names[predicted_class]} ({confidence:.1%})', fontsize=12)
                plt.ylabel('확률')
                plt.xticks(range(4), ['Stop', 'Go Straight', 'Turn Left', 'Turn Right'], rotation=45)
                plt.ylim(0, 1)
                
                # 확률 값 표시
                for i, (bar, prob) in enumerate(zip(bars, predictions[0])):
                    plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.01, 
                            f'{prob:.1%}', ha='center', va='bottom', fontsize=9)
                
                plt.tight_layout()
                plt.show()
                
                # 결과 출력
                print(f"\n🎯 예측 결과: {class_names[predicted_class]}")
                print(f"🔥 신뢰도: {confidence:.1%}")
                print("\n📊 모든 클래스 확률:")
                for i, (name, prob) in enumerate(zip(class_names, predictions[0])):
                    indicator = "👈" if i == predicted_class else "  "
                    print(f"  {name}: {prob:.1%} {indicator}")
                
                print("-" * 50)
                
            except Exception as e:
                print(f"❌ 오류 발생: {e}")
                print("💡 jpg, png 형식의 이미지를 업로드해주세요!")
    
    def show_sample_images(self):
        """어떤 이미지를 업로드하면 좋을지 예시 보여주기"""
        print("\n💡 이런 이미지들을 업로드해보세요!")
        print("=" * 50)
        print("🛑 정지 표지판 - 빨간색 팔각형")
        print("⬆️ 직진 표지판 - 파란색 화살표")  
        print("↩️ 좌회전 표지판 - 초록색 화살표")
        print("↪️ 우회전 표지판 - 노란색 화살표")
        print("\n📝 팁:")
        print("• 구글에서 '교통표지판' 검색해서 이미지 저장")
        print("• 스마트폰으로 실제 표지판 촬영")
        print("• 명확하고 잘 보이는 표지판일수록 정확도 높음")
        print("=" * 50)

def main():
    """메인 실행 함수"""
    print("🚗 실제 이미지 교통표지판 인식 시스템")
    print("=" * 50)
    
    # 시스템 초기화
    recognizer = RealImageTrafficSignRecognition()
    
    # 예시 이미지 설명
    recognizer.show_sample_images()
    
    # 모델 훈련
    history, accuracy = recognizer.train_model()
    
    # 이미지 업로드 및 예측
    while True:
        recognizer.upload_and_predict()
        
        # 계속할지 묻기
        continue_choice = input("\n🔄 다른 이미지도 테스트해보시겠어요? (y/n): ")
        if continue_choice.lower() != 'y':
            break
    
    print("\n🎉 테스트 완료! 수고하셨습니다!")

if __name__ == "__main__":
    main()
```

## 지도학습 적용 부분

- **라벨링된 차선 데이터**로 주행 방향 학습
- **표지판 이미지와 클래스**로 분류 모델 훈련  
- **실시간 도로 상황**에서 학습된 모델로 예측

실제 자율주행 시스템에서는 더 많은 센서 데이터와 복잡한 딥러닝 모델을 사용하지만, 이 코드는 지도학습의 핵심 개념을 잘 보여줍니다! 🚗
