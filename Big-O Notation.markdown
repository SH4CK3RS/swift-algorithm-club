# Big-O 표기법
알고리즘이 얼마나 빠르고 얼마나 많은 공간을 차지하는지 아는것은 어떤 작업을 할 때 적절한 알고리즘을 고를 수 있게 해줄 수 있어 매우 유용합니다.

Big-O표기법은 알고리즘의 실행시간 그리고 사용되는 메모리의 양을대략적으로 알 수 있게 해줍니다. 누군가가 “이 알고리즘은 **O(n^2)**라는 최악의 실행시간을 가지며 **O(n)**만크의 공간을 사용한다” 라고 한다면 이 알고리즘은 느리지만 많은양의 부가 메모리가 필요하지 않다는 것을 의미합니다

알고리즘의 Big-O를 파악하는 것은 대게 수학적 분석을 통해 이루어집니다. 여기서 수학적인 부분은 건너뛰지만, 값들이 어떻게 다른 의미를 가지고 있는지를 아는게 좋습니다. 아래의 표에서 볼 수 있는 **n**은 접근하는 데이터의 개수를 의미합니다. 예를들어 100개의 아이템이 있는 배열을 정렬한다면 **n = 100**입니다.


Big-O | 이름 | 설명
------| ---- | ----
**O(1)** | constant | **This is the best.** The algorithm always takes the same amount of time, regardless of how much data there is. Example: looking up an element of an array by its index.
**O(log n)** | logarithmic | **Pretty great.** These kinds of algorithms halve the amount of data with each iteration. If you have 100 items, it takes about 7 steps to find the answer. With 1,000 items, it takes 10 steps. And 1,000,000 items only take 20 steps. This is super fast even for large amounts of data. Example: binary search.
**O(n)** | linear | **Good performance.** If you have 100 items, this does 100 units of work. Doubling the number of items makes the algorithm take exactly twice as long (200 units of work). Example: sequential search.
**O(n log n)** | "linearithmic" | **Decent performance.** This is slightly worse than linear but not too bad. Example: the fastest general-purpose sorting algorithms.
**O(n^2)** | quadratic | **Kinda slow.** If you have 100 items, this does 100^2 = 10,000 units of work. Doubling the number of items makes it four times slower (because 2 squared equals 4). Example: algorithms using nested loops, such as insertion sort.
**O(n^3)** | cubic | **Poor performance.** If you have 100 items, this does 100^3 = 1,000,000 units of work. Doubling the input size makes it eight times slower. Example: matrix multiplication.
**O(2^n)** | exponential | **Very poor performance.** You want to avoid these kinds of algorithms, but sometimes you have no choice. Adding just one bit to the input doubles the running time. Example: traveling salesperson problem.
**O(n!)** | factorial | **Intolerably slow.** It literally takes a million years to do anything.

Often you don't need math to figure out what the Big-O of an algorithm is but you can simply use your intuition. If your code uses a single loop that looks at all **n** elements of your input, the algorithm is **O(n)**. If the code has two nested loops, it is **O(n^2)**. Three nested loops gives **O(n^3)**, and so on.

Note that Big-O notation is an estimate and is only really useful for large values of **n**. For example, the worst-case running time for the [insertion sort](Insertion%20Sort/) algorithm is **O(n^2)**. In theory that is worse than the running time for [merge sort](Merge%20Sort/), which is **O(n log n)**. But for small amounts of data, insertion sort is actually faster, especially if the array is partially sorted already!

If you find this confusing, don't let this Big-O stuff bother you too much. It's mostly useful when comparing two algorithms to figure out which one is better. But in the end you still want to test in practice which one really is the best. And if the amount of data is relatively small, then even a slow algorithm will be fast enough for practical use.
