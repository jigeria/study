
> 작성자 : 박상민 - (주)한컴인스페이스 미래기술개발부 연구원
>
> 본 포스트는 K-Nearest Neighbor 알고리즘에 대해 공부한 내용을 정리한 포스트 입니다.
>
> 글 내용에 수정사항이 있거나 궁금하신 사항 등은 메일보내주시면 감사하겠습니다.

<br/>

# KNN 최근접 이웃법

## 분류와 군집화

* KNN 알고리즘에 대해서 알기 전에 분류와 군집화의 차이점을 알아볼 필요가 있습니다.

> 분류 : 라벨이 있음, 지도 학습
>
> 군집화 : 라벨리 없음, 비지도 학습

![clustering vs classification](/images/2021_03_24_knn_study_figure_1.png)

* KNN 알고리즘은 __라벨이 있는 데이터를 활용해 라벨이 없는 새로운 데이터를 분류하는 분류 알고리즘에__ 속합니다.

<br/>

## 개요

* KNN 알고리즘은 한마디로 유유상종 이라고 할 수 있습니다. 새로운 데이터를 입력 받았을 때 주위에 어떤 데이터가 있냐에 따라 새로운 데이터의 카테고리를 정해줍니다.

* 기본적인 로직은 다음과 같습니다.

>
> 새로운 샘플 가까운거리에 있는 몇 가지 라벨을 함꼐 본다.
>
> 가장 빈도가 높은 것을 통해 새로운 데이터를 분류한다.

![KNN](/images/2021_03_24_knn_study_figure_2.png)


<br/>


## 두 점 사이의 거리 계산 : 유클리드 거리 (Euclidean distance)

* 가까운 거리와 빈도가 높은 것의 기준을 계산해야 하는데, 이를 위해 __유클리드 거리 (Euclidean distance)__ 를 사용합니다.

![KNN](/images/2021_03_24_knn_study_figure_4.png)

* 두 점 사이의 거리를 계산할 때 쓰이는 방법입니다. L2 거리(L2 Distance) 라고도 합니다.

* 거리 계산은 아래와 같습니다.

![KNN](/images/2021_03_24_knn_study_figure_3.svg)


<br>

![KNN](/images/2021_03_24_knn_study_figure_5.png)

> A-N 간의 유클리드 거리 : 3.1xx
>
> B-N 간의 유클리드 거리 : 2.8xx
>
> 여기서 N은 B가 더 가까운 것으로 측정

<br/>

## 빈도가 높은 것의 기준 : K의 개수

<br>

![KNN](/images/2021_03_24_knn_study_figure_6.png)

* 위 그림에서 k=3일 때는 새로운 샘플이 세모로 분류되지만, K=7일 때는 별표로 분류됩니다.

* 여기서 주의할 점은 K의 개수가 짝수일 경우 동점이 발생할 수 있기에 홀수로 지정해줘야 합니다.

<br/>

## 특징

* 다양한 지도학습 알고리즘 중에서 가장 고전적이고, 직관적입니다.

* 단순하고, 구현이 쉬우며 성능이 좋습니다.

* 모델 훈련 시간이 필요 없습니다.

<br/>


## 구현

* Python scikit-learn의 __KNeighborsClassifier__ API를 활용하면 쉽게 구현이 가능합니다.

![KNN](/images/2021_03_24_knn_study_figure_7.png)

</br>

* 샘플 예제코드는 다음과 같습니다. [샘플 코드](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html)  


```python
X = [[0], [1], [2], [3]]
y = [0, 0, 1, 1]

from sklearn.neighbors import KNeighborsClassifier
neigh = KNeighborsClassifier(n_neighbors=3) # n_neighbors : Number of neighbors to use by default for kneighbors queries.

neigh.fit(X, y) # Fit the k-nearest neighbors classifier from the training dataset.

print(neigh.predict([[1.1]])) # Predict the class labels for the provided data.
# [0]

print(neigh.predict_proba([[0.9]])) # Return probability estimates for the test data X.
#[[0.66666667 0.33333333]]

```
<br/>


# 참고자료

* https://john-analyst.medium.com/knn-%EC%B5%9C%EA%B7%BC%EC%A0%91-%EC%9D%B4%EC%9B%83-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-b397a0b2030e
* https://gomguard.tistory.com/51
* https://ko.wikipedia.org/wiki/K-%EC%B5%9C%EA%B7%BC%EC%A0%91_%EC%9D%B4%EC%9B%83_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98
* https://needjarvis.tistory.com/454
* https://dyndy.tistory.com/159

<br/>


# Contact Me

* 이름 : 박상민  
* 소속 : (주)한컴인스페이스 미래기술개발부  
* 연락처 : jigeria@naver.com  
* Github : https://github.com/jigeria  