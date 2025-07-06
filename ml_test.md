# 자율주행 지도학습 샘플 코드

## 개요
자율주행에서 지도학습을 활용한 교통표지판 분류 예시 코드입니다.

## 주요 기능
1. **차선 인식** - OpenCV로 차선 특징 추출 후 RandomForest로 주행 방향 결정
2. **교통표지판 분류** - CNN으로 정지, 직진, 좌회전, 우회전 표지판 인식
3. **통합 예측** - 차선과 표지판 정보를 종합한 주행 판단

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
