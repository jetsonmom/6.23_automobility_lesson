








# # NumPy vs TensorFlow 비교 가이드 🚀

> NumPy 사용자를 위한 TensorFlow 텐서 학습 가이드

## 📋 목차
- [기본 생성 함수](#기본-생성-함수)
- [랜덤 함수](#랜덤-함수)
- [정보 확인](#정보-확인)
- [기본 연산](#기본-연산)
- [형태 변환](#형태-변환)
- [인덱싱](#인덱싱)
- [상호 변환](#상호-변환)
- [주요 차이점](#주요-차이점)
- [실습 예제](#실습-예제)

---

## 🏗️ 기본 생성 함수

| 기능 | NumPy | TensorFlow |
|------|-------|------------|
| **0으로 채우기** | `np.zeros((2, 3))` | `tf.zeros([2, 3])` |
| **1로 채우기** | `np.ones((2, 3))` | `tf.ones([2, 3])` |
| **배열/텐서 생성** | `np.array([1,2,3])` | `tf.constant([1,2,3])` |
| **특정값으로 채우기** | `np.full((2, 3), 7)` | `tf.fill([2, 3], 7)` |
| **연속 숫자** | `np.arange(1, 11)` | `tf.range(1, 11)` |
| **등간격 숫자** | `np.linspace(0, 10, 5)` | `tf.linspace(0.0, 10.0, 5)` |

---

## 🎲 랜덤 함수

| 기능 | NumPy | TensorFlow |
|------|-------|------------|
| **정규분포** | `np.random.normal(0, 1, (2,3))` | `tf.random.normal([2,3], 0, 1)` |
| **균등분포** | `np.random.uniform(0, 10, (2,3))` | `tf.random.uniform([2,3], 0, 10)` |
| **시드 설정** | `np.random.seed(42)` | `tf.random.set_seed(42)` |

---

## 📊 정보 확인

| 기능 | NumPy | TensorFlow |
|------|-------|------------|
| **형태** | `arr.shape` | `tensor.shape` |
| **차원 수** | `arr.ndim` | `tf.rank(tensor)` |
| **원소 개수** | `arr.size` | `tf.size(tensor)` |
| **데이터 타입** | `arr.dtype` | `tensor.dtype` |

---

## ➕ 기본 연산

| 기능 | NumPy | TensorFlow |
|------|-------|------------|
| **덧셈** | `a + b` | `tf.add(a, b)` 또는 `a + b` |
| **곱셈** | `a * b` | `tf.multiply(a, b)` 또는 `a * b` |
| **행렬곱** | `np.matmul(a, b)` 또는 `a @ b` | `tf.matmul(a, b)` 또는 `a @ b` |
| **전치** | `a.T` 또는 `np.transpose(a)` | `tf.transpose(a)` |

---

## 🔄 형태 변환

| 기능 | NumPy | TensorFlow |
|------|-------|------------|
| **형태 변경** | `arr.reshape(2, 3)` | `tf.reshape(tensor, [2, 3])` |
| **차원 추가** | `np.expand_dims(arr, 0)` | `tf.expand_dims(tensor, 0)` |
| **차원 제거** | `np.squeeze(arr)` | `tf.squeeze(tensor)` |
| **평탄화** | `arr.flatten()` | `tf.reshape(tensor, [-1])` |

---

## 🎯 인덱싱

| 기능 | NumPy | TensorFlow |
|------|-------|------------|
| **단일 원소** | `arr[0, 1]` | `tensor[0, 1]` |
| **행 선택** | `arr[0, :]` | `tensor[0, :]` |
| **열 선택** | `arr[:, 1]` | `tensor[:, 1]` |
| **슬라이싱** | `arr[1:3, 0:2]` | `tensor[1:3, 0:2]` |

---

## 🔄 상호 변환

| 변환 방향 | 코드 | 설명 |
|-----------|------|------|
| **NumPy → TensorFlow** | `tf.constant(numpy_array)` | NumPy 배열을 TensorFlow 텐서로 |
| **TensorFlow → NumPy** | `tensor.numpy()` | TensorFlow 텐서를 NumPy 배열로 |

### 예제 코드
```python
import numpy as np
import tensorflow as tf

# NumPy → TensorFlow
np_data = np.array([1, 2, 3, 4, 5])
tf_tensor = tf.constant(np_data)

# TensorFlow → NumPy  
tf_data = tf.constant([10, 20, 30])
np_array = tf_data.numpy()
```

---

## 📋 주요 차이점

| 항목 | NumPy | TensorFlow |
|------|-------|------------|
| **실행 환경** | CPU만 | CPU + GPU + TPU |
| **주 사용 목적** | 과학 계산, 데이터 분석 | 딥러닝, 머신러닝 |
| **자동 미분** | ❌ | ✅ |
| **즉시 실행** | ✅ | ✅ (2.0+) |
| **모델 저장** | ❌ | ✅ |
| **분산 처리** | ❌ | ✅ |
| **생태계** | SciPy, Pandas | Keras, TensorBoard |

---

## 💻 실습 예제

### 기본 사용법 비교
```python
import numpy as np
import tensorflow as tf

# 1. 배열/텐서 생성
np_array = np.array([[1, 2], [3, 4]])
tf_tensor = tf.constant([[1, 2], [3, 4]])

# 2. 0으로 채우기
np_zeros = np.zeros((3, 3))
tf_zeros = tf.zeros([3, 3])

# 3. 기본 연산
np_result = np_array + np_array
tf_result = tf_tensor + tf_tensor

# 4. 형태 확인
print(f"NumPy shape: {np_array.shape}")
print(f"TensorFlow shape: {tf_tensor.shape}")
```

### GPU 사용 (TensorFlow만 가능)
```python
# GPU 사용 확인
print(f"GPU 사용 가능: {tf.config.list_physical_devices('GPU')}")

# GPU에서 연산
with tf.device('/GPU:0'):
    gpu_tensor = tf.constant([[1.0, 2.0], [3.0, 4.0]])
    result = tf.matmul(gpu_tensor, gpu_tensor)
```

---

## 💡 학습 팁

### NumPy 사용자를 위한 빠른 적응법
1. **괄호 → 대괄호**: `(2, 3)` → `[2, 3]`
2. **함수명 유사**: 대부분 동일하거나 유사
3. **인덱싱 동일**: 슬라이싱 문법 완전 동일
4. **GPU 장점**: 큰 데이터는 TensorFlow가 훨씬 빠름

### 언제 어떤 것을 사용할까?
- **NumPy**: 데이터 전처리, 과학 계산, 프로토타이핑
- **TensorFlow**: 딥러닝 모델, GPU 가속, 대용량 데이터

---

## 🔗 유용한 링크

- [NumPy 공식 문서](https://numpy.org/doc/)
- [TensorFlow 공식 문서](https://www.tensorflow.org/guide)
- [TensorFlow NumPy 호환성 가이드](https://www.tensorflow.org/guide/tf_numpy)



