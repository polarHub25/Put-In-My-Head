### 배열 (Array)

<img src="D:/Put-In-My-Head/Image/array.PNG" width="80%" height="60%" alt="ARRAY"></img>
- 같은 특성을 갖는 원소들이 순서대로 구성된 집합(선형 자료 구조)
- 메모리 상에 연속적으로 데이터 저장(순차 리스트)
- 고정된 크기 (메모리가 낭비 될 수 있음)
- Cache Hit Rate가 높음
(* Cache Hit Rate : CPU가 참조하고자 하는 메모리가 캐시에 존재하는 경우 , 비율이 높을수록 좋은 성능)
- 삽입/삭제 : O(N)의 시간복잡도
- 조회 : O(1)의 시간복잡도


### 리스트 (List) : 연결 리스트(Linked List)

<img src="D:/Put-In-My-Head/Image/list.PNG" width="80%" height="60%" alt="ARRAY"></img>
- 연결 리스트 , ArrayList 등 선형 자료 구조를 표현할 때 사용되는 추상 자료형
- 같은 특성을 갖는 원소들이 순서대로 구성된 집합(선형 자료 구조)
- 메모리 상에 연속적으로 저장되진 않음(연결 리스트)
- 배열 VS 리스트 차이를 묻는 의미 => 리스트는 __Linked List(연결 리스트)__ 처럼 모습이 확정된 자료구조
- 데이터들이 순차적으로 구성된 집합이지만, 데이터가 메모상에 연속적으로 있진 않음 (메모리 주소 랜덤)
- Cache Hit Rate가 낮음
- 가변적인 크기(메모리 낭비 적음)
- 삽입/삭제 : O(N)의 시간복잡도
- 조회 : O(N)의 시간복잡도
