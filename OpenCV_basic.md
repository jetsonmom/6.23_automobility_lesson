

OpenCV란
OpenCV란?
**OpenCV(Open Source Computer Vision Library)**는 컴퓨터 비전, 머신러닝, 이미지 처리를 위한 오픈소스 라이브러리입니다.
주요 특징
무료 오픈소스: 상업적 용도로도 자유롭게 사용 가능한 BSD 라이선스
크로스 플랫폼: Windows, Linux, macOS, Android, iOS 등 다양한 운영체제 지원
다양한 언어 지원: C++, Python, Java, C# 등 여러 프로그래밍 언어에서 사용 가능
고성능: C/C++로 작성되어 빠른 처리 속도를 제공
주요 기능
이미지 처리: 필터링, 색상 변환, 크기 조정, 회전 등 기본적인 이미지 조작
컴퓨터 비전: 객체 검출, 얼굴 인식, 특징점 추출, 패턴 매칭
비디오 처리: 비디오 파일 읽기/쓰기, 실시간 카메라 입력 처리
머신러닝: 분류, 회귀, 클러스터링 등 기본적인 머신러닝 알고리즘
활용 분야
의료 영상: 의료 이미지 분석, 진단 보조
자율주행: 차선 인식, 객체 검출, 거리 측정
보안 시스템: 얼굴 인식, 동작 감지, 침입 탐지
제조업: 제품 검사, 결함 탐지, 품질 관리
엔터테인먼트: AR/VR, 게임, 영상 편집
스마트폰: 카메라 앱, 사진 편집, 필터 효과
Python에서 사용법



import cv2
import numpy as np
import matplotlib.pyplot as plt

# 이미지 읽기 (실제 파일 경로 사용)
image = cv2.imread('/content/sample_data/3.jpg')

# 파일이 제대로 읽혔는지 확인
if image is None:
    print("이미지를 찾을 수 없습니다!")
else:
    # 그레이스케일 변환
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # 이미지 표시 (matplotlib 사용)
    plt.figure(figsize=(12, 5))
    
    plt.subplot(1, 2, 1)
    plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # BGR을 RGB로 변환
    plt.title('Original')
    plt.axis('off')
    
    plt.subplot(1, 2, 2)
    plt.imshow(gray, cmap='gray')
    plt.title('Gray')
    plt.axis('off')
    
    plt.show()




자주 사용되는 컬러맵, 소문자가 정
plt.imshow(image, cmap='viridis')    # 기본값
plt.imshow(image, cmap='plasma')     # 보라-핑크
plt.imshow(image, cmap='hot')        # 빨강-노랑
plt.imshow(image, cmap='cool')       # 파랑-보라
plt.imshow(image, cmap='jet')        # 무지개색






방대한 기능: 이미지 처리부터 고급 컴퓨터 비전까지 포괄적인 기능 제공
활발한 커뮤니티: 전 세계 개발자들이 기여하고 지원하는 거대한 생태계
풍부한 자료: 문서, 튜토리얼, 예제 코드가 풍부함
산업 표준: 컴퓨터 비전 분야에서 사실상의 표준 라이브러리
학습 용이성: 특히 Python 바인딩으로 초보자도 쉽게 시작 가능
OpenCV는 2000년 인텔에서 시작되어 현재까지 20년 이상 발전해온 검증된 라이브러리로, 컴퓨터 비전과 이미지 처리를 배우고 싶다면 반드시 알아야 할 필수 도구입니다!


OpenCV 기본 용어 정리
이미지 기본 개념
Image: 이미지
Pixel: 픽셀
Resolution: 해상도
Grayscale: 그레이스케일 (흑백)
RGB: Red-Green-Blue (빨강-초록-파랑)
BGR: Blue-Green-Red (OpenCV 기본 색상 순서)
HSV: Hue-Saturation-Value (색조-채도-명도)
Channel: 채널 (색상 성분)
Depth: 깊이 (색상 비트수)
이미지 처리 기본
Filtering: 필터링
Smoothing: 스무딩 (부드럽게)
Blurring: 블러링 (흐림)
Sharpening: 샤프닝 (선명하게)
Noise Reduction: 노이즈 제거
Histogram: 히스토그램
Equalization: 평활화
기하학적 변환
Resize: 크기 조정
Rotate: 회전
Translation: 이동
Scaling: 스케일링
Flip: 뒤집기
Crop: 자르기
Warp: 변형
Affine Transform: 아핀 변환
Perspective Transform: 원근 변환
필터와 커널
Kernel: 커널 (필터 행렬)
Convolution: 합성곱
Gaussian Filter: 가우시안 필터
Median Filter: 중간값 필터
Bilateral Filter: 양방향 필터
Morphological Operations: 형태학적 연산
Erosion: 침식
Dilation: 팽창
Opening: 열기
Closing: 닫기
엣지 및 윤곽선
Edge Detection: 엣지 검출
Canny Edge: 캐니 엣지
Sobel: 소벨
Laplacian: 라플라시안
Gradient: 그래디언트
Contour: 윤곽선
Contour Detection: 윤곽선 검출
Boundary: 경계
임계값 처리
Threshold: 임계값
Binary Threshold: 이진 임계값
Adaptive Threshold: 적응형 임계값
Otsu's Method: 오츠 방법
Binarization: 이진화
특징 검출
Feature Detection: 특징 검출
Corner Detection: 모서리 검출
Harris Corner: 해리스 모서리
SIFT: Scale-Invariant Feature Transform
SURF: Speeded Up Robust Features
ORB: Oriented FAST and Rotated BRIEF
Keypoint: 키포인트
Descriptor: 디스크립터
객체 검출 및 추적
Object Detection: 객체 검출
Template Matching: 템플릿 매칭
Feature Matching: 특징 매칭
Tracking: 추적
Cascade Classifier: 캐스케이드 분류기
Haar Cascade: 하르 캐스케이드
HOG: Histogram of Oriented Gradients
기본 데이터 타입
Mat: 행렬 (OpenCV 기본 이미지 타입)
Array: 배열
Vector: 벡터
Point: 점
Rect: 사각형
Size: 크기
Scalar: 스칼라 (색상값)
색상 공간
Color Space: 색상 공간
Color Conversion: 색상 변환
cvtColor: 색상 변환 함수
COLOR_BGR2GRAY: BGR에서 그레이스케일로
COLOR_BGR2HSV: BGR에서 HSV로
COLOR_BGR2RGB: BGR에서 RGB로
이미지 입출력
imread: 이미지 읽기
imwrite: 이미지 쓰기
imshow: 이미지 보기
waitKey: 키 입력 대기
destroyAllWindows: 모든 창 닫기
비디오 처리
VideoCapture: 비디오 캡처
VideoWriter: 비디오 쓰기
Frame: 프레임
FPS: Frames Per Second (초당 프레임수)
Codec: 코덱
이 용어들은 OpenCV 문서나 튜토리얼에서 자주 등장하는 핵심 개념들입니다!


