![Swift Algorithm Club](/Images/SwiftAlgorithm-410-transp.png)

# Swift Algorithm Club에 오신것을 환영합니다.!

여기서 유명한 알고리즘 및 자료구조가 여러분이 좋아하는 새로운 언어 Swift에서 어떻게 작동되는지 자세한 설명과 함께 살펴보실 수 있습니다.

만약 시험 때문에 이것을 배우는 컴퓨터 과학 전공생, 프로그래밍을 독학하고 있는 프로그래머이지만, 기술에 대한 이론을 학습 해보고 싶은 사람이라면 잘 찾아오셨습니다!

이 프로젝트의 목표는 **어떻게 알고리즘이 작동하는가를 알려주는 것** 입니다. 단순히 복사 붙여넣기의 과정으로 소스코드를 자신의 프로젝트에 넣는 것이 아닌, 코드의 명확성과 가독성을 키우도록 하는 것에 초점을 두고 있습니다. 대부분의 코드는 실제로 사용할 준비가 되어있어야하지만, 자신만의 코드에 알맞게 조절할 수도 있어야 합니다. 

이 프로젝트에서 소개되는 대부분의 코드는 **Xcode8.3** 및 **Swift3** 와 호완되며, 최신 버전의 Swift에 맞게 업데이트 됩니다.

:heart_eyes: **제안 및 도움 주시면 감사하겠습니다.** :heart_eyes:

## Important links

[알고리즘과 자료구조가 무엇인가요?](What%20are%20Algorithms.markdown) Pancakes!

[왜 알고리즘을 배우나요?](Why%20Algorithms.markdown) 처음 알고리즘을 접하는 분이라면, 이 글을 읽어보세요

[Big-O 표기법](Big-O%20Notation.markdown). 알고리즘을 공부하다보면 **O(n)**과 같은 표현을 자주 보게 됩니다. 아직 무슨 의미인지 모른다면 이 글을 읽어보세요

[알고리즘 설계 기술](Algorithm%20Design.markdown). 이 글에서는 어떻게 자신만의 알고리즘을 만들 수 있는지에 대해 이야기하고있습니다.

[기여하는 법](https://github.com/raywenderlich/swift-algorithm-club/blob/master/.github/CONTRIBUTING.md). 문제 제기 또는 피드백을 보내주세요

## 어디서부터 시작하지?
만약 알고리즘과 자료구조가 처음이라면, 아래의 좋은 예제들로 시작하는게 좋습니다:

- [스텍](Stack/)
- [큐](Queue/)
- [삽입 정렬](Insertion%20Sort/)
- [이진 탐색](Binary%20Search/) / [이진 탐색 트리](Binary%20Search%20Tree/)
- [병합 정렬](Merge%20Sort/)
- [Boyer-Moore 문자열 탐색](Boyer-Moore/)

## 알고리즘

### 탐색

- [선형 탐색](Linear%20Search/). 배열로부터 요소를 찾는 작업
- [이진 탐색](Binary%20Search/). 분류된 배열에서 빠르게 요소를 찾는 작업
- [발생 빈도](Count%20Occurrences/). 배열에서 얼마나 값이 자주 나타나는지 보는 작업
- [최소/ 최대선택](Select%20Minimum%20Maximum). 배열에서 최소/최대값을 찾는 작업
- [k번째로 큰 값](Kth%20Largest%20Element/).중앙 값 과 같이 배열에서 k번째로 큰 값을 찾는 작업.
- [샘플 선택](Selection%20Sampling/). 콜렉션으로부터 값을 무작위로 추출하는 작업
- [Union-Find](Union-Find/). 분리된 집합을 찾고 쉽게 병합하도록 도와주는 작업


### 문자열 탐색

[무차별 문자열 탐색](Brute-Force%20String%20Search/). 무식한 방법
- [Boyer-Moore](Boyer-Moore/). 문자열 추출을 위한 빠른 탐색 방법. 순람표를 기초로 하여 텍스트로부터 모든 문자를 체크하는 것을 피하기 위해 사용
- [Knuth-Morris-Pratt](Knuth-Morris-Pratt/). 주어진 패턴이 발생하는 인덱스를 반환하는 선형 시간 문자열 알고리즘
- [Rabin-Karp](Rabin-Karp/)  해시를 이용한 빠른 탐색
- [Longest Common Subsequence](Longest%20Common%20Subsequence/). 최장 공통 부분 문자열 알고리즘
- [Z-Algorithm](Z-Algorithm/). 주어진 문자열로부터 특정 패턴을 찾는 알고리즘

### 정렬

알고리즘이 어떻게 작동하는지 보는 것은 재미있지만, 실제로 자신만의 정렬 루틴을 제공할 일이 거의 없습니다. 스위프트의 `sort()`를 사용하는것이 더 적합합니다. 하지만 흥미있다면 읽어보세요…


기초 정렬:

- [삽입 정렬](Insertion%20Sort/)
- [선택 정렬](Selection%20Sort/)
- [쉘 정렬](Shell%20Sort/)

빠른 정렬:

- [퀵소트](Quicksort/)
- [병합 정렬](Merge%20Sort/)
- [힙 정렬](Heap%20Sort/)

특별한 목적의 정렬:

- [계수 정렬](Counting%20Sort/)
- [기수 정렬](Radix%20Sort/)
- [위상 정렬](Topological%20Sort/)

안좋은 정렬 알고리즘 (사용하지 마세요!):

- [거품정렬](Bubble%20Sort/)
- [느린 정렬](Slow%20Sort/)

### 압축

- [Run-Length Encoding (RLE)](Run-Length%20Encoding/). 한 문자(byte)가 몇 번 반복되는지 찾는 알고리즘
- [허프만 부호화](Huffman%20Coding/). 적은 수의 비트를 사용하여 더 많은 공통 요소 저장.

### 잡다한 알고리즘

- [Shuffle](Shuffle/). 배열의 내용을 무작위로 재정렬함
- [Comb Sort](Comb%20Sort/). 거품 정렬 알고리즘이 개선된 알고리즘.

### 수학

- [최대공약수 (GCD)](GCD/). 특별 보너스: 최소공배수 포함.
- [순열 및 조합](Combinatorics/). 조합을 잡아라!
- [차량 기지 알고리즘](Shunting%20Yard/). 중위 표기법으로 표현된 수식을 분석하는 알고리즘
- [카라추바 알고리즘](Karatsuba%20Multiplication/). 큰 수를 위한 곱셈 알고리즘
- [Haversine Distance](HaversineDistance/). 구체의 두 점 사에의 거리를 구하는 알고리즘.
- [Strassen의 곱셈 행렬](Strassen%20Matrix%20Multiplication/). 효과적으로 행렬 곱셈을 다룬다.

### 머신러닝

- [k-평균 알고리즘](K-Means/). 주어진 데이터를 k개의 클러스터로 묶는 알고리즘
- [선형 회귀](Linear%20Regression/). 두 개 (또는 그 이상)의 가변 수량 사이의 관계 모델을 생성하는 알고리즘
- Logistic Regression
- 인공 신경망
- 페이지랭크

## 자료구조
특정 작업을 할떄 자료구조를 선택하는 것은 다음 몇가지에 달려있습니다.
먼저 데이터의 모양과 해야할일에 수행해야할 연산 등이 있습니다. 만약 Key를 이용해 객체를 찾고싶다면 일종의 Dictionary가 필요할 것이고; 계층적인 데이터인 경우 정렬된 트리구조가 필요할 것이고; 데이터가 순차적인 경우 스텍 또는 큐가 필요할 것입니다.

두번째로, 특정 데이터 구조가 이미 특정 작업에 맞게 최적화 되어있기때문에 무엇을 가장 많이 수행하게 될지가 중요합니다. 예를들어 컬렉션으로부터 가장 중요한 객체를 자주 찾아야하는 경우, 일반 배열보다 힙 또는 우선순위 큐가 더 적절할 것입니다.

대부분의 경우`Array`,`Dictionary`,`Set` 타입만으로도 충분 합니다만, 더 근사한 것을 원하실 수도 있겠다고 생각합니다.

### 배열 변형

- [Array2D](Array2D/). 고정 치수가 있는 2차원 배열로, 보드 게임 등에 유용합니다.
- [Bit Set](Bit%20Set/). * n * 비트의 고정 크기 시퀀스.
- [Fixed Size Array](Fixed%20Size%20Array/). 데이터가 얼마나 큰지 미리 아는 경우 고정 크기의 구형 배열을 사용하는 것이 더 효율적일 수 있습니다.
- [Ordered Array](Ordered%20Array/). 항상 정렬되어있는 배열
- [Rootish Array Stack](Rootish%20Array%20Stack/). 스위프트 배열에서 시공간적으로 효율적인 변형

### 큐

- [스텍](Stack/). 후입-선출!
- [큐](Queue/). 선입-선출
- [덱](Deque/). 양단에서 삽입, 삭제가 가능함
- [우선순위 큐](Priority%20Queue). 가장 중요한 요소가 가장 앞으로 오는 큐
- [원형 버퍼](Ring%20Buffer/). 고정된 크기의 버퍼를 양 끝이 연결된 것처럼 사용할 수 있게 해주는 자료 구조

### 리스트

- [링크드 리스트](Linked%20List/).링크를 통해 연결된 일련의 데이터 항목으로, 단일 및 이중 링크 된 리스트 모두를 다룸.
- [스킵 리스트](Skip-List/). AVL / Red-Black 트리와 동일한 로그 시간 제한 및 효율성을 지닌 확률적인 데이터 구조이며 검색 및 업데이트 작업을 효율적으로 지원할 수있는 좋은 타협을 제공합니다.

### 트리

- [트리](Tree/). 일반적인 목적의 트리 구조
- [이진 트리](Binary%20Tree/). 각 노드에 최대 두 개의 하위 노드가있는 트리.
- [이진 탐색 트리(BST)](Binary%20Search%20Tree/). 빠른 명령을 허용하는 방식으로 노드를 정렬하는 2진트리
- [레드-블랙 트리](Red-Black%20Tree/). 자가 균형 이진 탐색 트리
- Splay Tree
- [스레드 이진 트리](Threaded%20Binary%20Tree/). 저렴하고 빠른 순회 탐색을위한 몇 가지 추가 변수를 유지하는 이진 트리,
- [세그먼트 트리](Segment%20Tree/). 일부 배열에 대해 기능을 빠르게 수행 할 수 있음
- kd-Tree
- [힙](Heap/). 배열에 저장된 이진 트리이므로 포인터를 사용하지 않음. 큰 우선 순위 대기열을 만든다.
- [트라이](Trie/). 연관 자료구조를 저장하기 위해 사용되는 특별한 트리
- [B-트리](B-Tree/). 자가 균형 이진 탐색 트리로써, 각 노드가 2개 이상의 하위 노드를 가질 수 있음

### 해쉬 알고리즘

- [해쉬 테이블](Hash%20Table/). 키를 이용하여 값을 저장하거나 회수할 수 있게 해줍니다. Dictionary가 어떤식으로 작동하는지 보여줍니다.
- 해쉬 함수

### 집합

- [Bloom Filter](Bloom%20Filter/). 값이 집합에 포함되는지를 확률적으로 테스트하는 상수 메모리 자료구조.
- [해쉬 집합](Hash%20Set/). 해쉬 테이블을 사용하여 수행되는 집합.
- 멀티셋
- [정렬 집합](Ordered%20Set/). 순서가 중요한 집합

### 그래프

- [그래프](Graph/)
- [너비 우선 탐색(BFS)](Breadth-First%20Search/)
- [깊이 우선 탐색 (DFS)](Depth-First%20Search/)
- [최단 경로](Shortest%20Path%20%28Unweighted%29/) on an unweighted tree
- [싱글 소스 최단 경로](Single-Source%20Shortest%20Paths%20(Weighted)/)
- [최소 신장 트리](Minimum%20Spanning%20Tree%20%28Unweighted%29/) on an unweighted tree
- [모든쌍 최단경로](All-Pairs%20Shortest%20Paths/)

## 퍼즐

대부분의 개발자 인터뷰 질문들은 알고리즘 퍼즐로 되어 있습니다. 여기 재미있는 퍼즐들이 있습니다. (답변과 함께 보려면), 여길 보세요 [링크](http://elementsofprogramminginterviews.com/) / [링크](http://www.crackingthecodinginterview.com).

- [Two-Sum Problem](Two-Sum%20Problem/)
- [Fizz Buzz](Fizz%20Buzz/)
- [몬티 홀 문제](Monty%20Hall%20Problem/)
- [Finding Palindromes](Palindromes/) 어느쪽으로 읽어도 똑같은 숫자를 찾는 알고리즘
- [식사하는 철학자](DiningPhilosophers/) 

## 더 배우기!

더 많은 정보를 원하시면 다음의 책을 확인해보세요:

- [Introduction to Algorithms](https://mitpress.mit.edu/books/introduction-algorithms) by Cormen, Leiserson, Rivest, Stein
- [The Algorithm Design Manual](http://www.algorist.com) by Skiena
- [Elements of Programming Interviews](http://elementsofprogramminginterviews.com) by Aziz, Lee, Prakash
- [Algorithms](http://www.cs.princeton.edu/~rs/) by Sedgewick
- [Grokking Algorithms](https://www.manning.com/books/grokking-algorithms) by Aditya Bhargava 

다음 책들은 온라인에서 무료로 볼 수 있습니다.:

- [Algorithms](http://www.beust.com/algorithms.pdf) by Dasgupta, Papadimitriou, Vazirani
- [Algorithms, Etc.](http://jeffe.cs.illinois.edu/teaching/algorithms/) by Erickson
- [Algorithms + Data Structures = Programs](http://www.ethoberon.ethz.ch/WirthPubl/AD.pdf) by Wirth
- Algorithms and Data Structures: The Basic Toolbox by Mehlhorn and Sanders
- [Open Data Structures](http://opendatastructures.org) by Pat Morin
- [Wikibooks: Algorithms and Implementations](https://en.wikibooks.org/wiki/Algorithm_Implementation)

다른 알고리즘 저장소:

- [EKAlgorithms](https://github.com/EvgenyKarkan/EKAlgorithms). A great collection of algorithms in Objective-C.
- [@lorentey](https://github.com/lorentey/). Production-quality Swift implementations of common algorithms and data structures.
- [Rosetta Code](http://rosettacode.org). Implementations in pretty much any language you can think of.
- [AlgorithmVisualizer](http://jasonpark.me/AlgorithmVisualizer/). Visualize algorithms on your browser.
- [Swift Structures](https://github.com/waynewbishop/SwiftStructures) Data Structures with directions on how to use them [here](http://waynewbishop.com/swift)

## 크레딧

Swift Algorithm Club은 [Matthijs Hollemans](https://github.com/hollance)에 의해 만들어졌습니다.

현재 [Vincent Ngo](https://www.raywenderlich.com/u/jomoka), [Kelvin Lau](https://github.com/kelvinlauKL) 그리고 [Ross O'brien](https://www.raywenderlich.com/u/narrativium).에 의해 지속적으로 운영되고 있습니다.

Swift Algorithm Club 은 [raywenderlich.com](https://www.raywenderlich.com) 커뮤니티의 [most algorithmic members](https://github.com/rwenderlich/swift-algorithm-club/graphs/contributors)의 협력과 노력의 결과물입니다.  우리는 항상 도와주실 분을 찾고 있습니다. - why not [join the club](How%20to%20Contribute.markdown)? :]

## License

All content is licensed under the terms of the MIT open source license.

By posting here, or by submitting any pull request through this forum, you agree that all content you submit or create, both code and text, is subject to this license.  Razeware, LLC, and others will have all the rights described in the license regarding this content.  The precise terms of this license may be found [here](https://github.com/raywenderlich/swift-algorithm-club/blob/master/LICENSE.txt).

[![Build Status](https://travis-ci.org/raywenderlich/swift-algorithm-club.svg?branch=master)](https://travis-ci.org/raywenderlich/swift-algorithm-club)
