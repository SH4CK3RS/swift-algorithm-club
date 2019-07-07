# 이진 

목표: 배열로부터 요소를 빠르게 찾기.

숫자로 이루어진 배열이 있고, 그 배열에 특정 숫자가 있다면 어떤 인덱스에 있는지 확인하려고한다고 가정해 보겠습니다.

대부분의 경우에 Swift에서는 `indexOf()` 함수를 사융하는 것으로도 충분합니다:

```swift
let numbers = [11, 59, 3, 2, 53, 17, 31, 7, 19, 67, 47, 13, 37, 61, 29, 43, 5, 41, 23]

numbers.indexOf(43)  // returns 15
```
내장 함수 `indexOf()` 는 [선형 탐색](../Linear%20Search/)을 수행합니다. 코드는 다음과 같습니다:

```swift
func linearSearch<T: Equatable>(_ a: [T], _ key: T) -> Int? {
    for i in 0 ..< a.count {
        if a[i] == key {
            return i
        }
    }
    return nil
}
```

그리고 이런 방식으로 사용 가능합니다:

```swift
linearSearch(numbers, 43)  // returns 15
```

그래서 문제가 뭘까요? `linearSearch()` 는 처음부터 찾고자 하는 값을 발견할 떄까지 전체 배열을 순회합니다. 최악의 경우는 배열에 값이 없을 수도 있고 그렇다면 작업이 완료되도 아무것도 얻지 못할 것입니다.

평균적으로 선형 탐색 알고리즘은 배열의 절반을 탐색하는것을 필요로하며, 배열이 커질 경우 작업은 매우 느려지게됩니다!


## 분할 정복

고전적인 방법으로 선형 탐색의 속도를 올리는 방법은 *이진 탐색*이다. 이 방법은 원하는 값을 찾을 때까지 배열을 반으로 나누는 것이다. 

선형 탐색에서 크기가 `n`인 배열의 경우 성능은 **O(n)**이 아니라 **O(log n)**이다. 이러한 관점에서 봤을 때 1,000,000개의 요소로 이루어진 배열에서 이진 탐색은 `log_2(1,000,000) = 19.9`이므로 원하는 데이터를 찾는데 약 20단계를 거친다. 그리고 10억개의 데이터가 있는 배열의 경우 오직 30단계만 거친다. (더해서.. 10억개 이상의 데이터 배열을 사용한게 언제가 마지막인가요?..)

좋습니다. 하지만 이진탐색이 부적합한 경우도 있습니다: 배열이 정렬되어야할때. 실제로, 이런게 일반적으로 문제가 되진 않습니다.

다음은 이진 탐색이 작동하는 방법입니다:

- 배열을 반으로 나눈 후 *search key*라고 하는 찾고자하는 값이 어디에 반으로 나눈 좌측에 있는지 아니면 우측에 있는지 특정합니다.
- 그렇다면 어떻게 key가 어디에 있는지 특정할 수 있을까요? 이것이 먼저 배열을 정렬해야하는 이유아며, 단순히 `<` 또는 `>`와 같은 비교 연산을 사용할 수 있습니다.
- 만약 search key가 반으로 나눈 배열 중 왼쪽이라면 해당 배열에 같은 과정을 반복합니다: 왼쪽 배열을 계속하여더 작은배열로 만드는 과정을 반복하여 key가 어디에 있는지 탐색합니다.(만약 오른쪽 배여링라면 해당 배열에서도 마찬가지로 반복합니다.)
- search key가 발견될 떄 까지 해당 작업을 반복합니다. 만약 배열이 더이상 둘로 나뉘어질 수 없을때까지 해당 작업을 반복했다면 애석하게도 해당 배열에서 찾고자 하는 search key는 존재 하지 않는것입니다.

이제 이게 왜 "이진" 탐색이라고 불리는지 아실것입니다: 모든 과정에서 배열을 두개로 나눕니다. 이 과정에서 *분할과 정복*은 빠르게 범위를 좁혀서 search key를 찾는 것입니다.

## 코드

다음 코드는 이진 탐색을 Swift에서 적용한 것입니다:

```swift
func binarySearch<T: Comparable>(_ a: [T], key: T, range: Range<Int>) -> Int? {
    if range.lowerBound >= range.upperBound {
        // If we get here, then the search key is not present in the array.
        return nil

    } else {
        // Calculate where to split the array.
        let midIndex = range.lowerBound + (range.upperBound - range.lowerBound) / 2

        // Is the search key in the left half?
        if a[midIndex] > key {
            return binarySearch(a, key: key, range: range.lowerBound ..< midIndex)

        // Is the search key in the right half?
        } else if a[midIndex] < key {
            return binarySearch(a, key: key, range: midIndex + 1 ..< range.upperBound)

        // If we get here, then we've found the search key!
        } else {
            return midIndex
        }
    }
}
```

해당 코드를 실행해보기 위해서 아래 코드를 복사하여 Playground에서 실행해보세요:

```swift
let numbers = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67]

binarySearch(numbers, key: 43, range: 0 ..< numbers.count)  // gives 13
```

`숫자`배열이 정렬되어있는 것에 주목하세요. 이진 탐색 알고리즘은 정렬되지 않은 배열에서는 효과가 없습니다.

이진 탐색은 배열을 반으로 분할하여 작동한다고 말씀드렸습니다. 하지만 두개의 새로운 배열을 만드는 것이 아닙니다. 대신에, Swift의 `Range`객체를 이용하여 분할을 추적합니다. 처음 `0 ..< numbers.count`로 전체 배열의 범위를 다룹니다. 배열을 반으로 나누면서 해당 범위가 점점 작아지는 것입니다. 

> **주목:** 한가지 알고 넘어가야할 부분은 `range.upperBound`가 항상 마지막 요소의 다음을 가리키고 있다는 것입니다. 예시로, 범위가 `0..<19` 일때 총 19개의 숫자가 배열에 있기 때문에 `range.lowerBound = 0`이며 `range.upperBound = 19`입니다. 하지만 배열의 index는 0부터 세기 때문에 우리의 배열에서 마지막 요소의 index는 19가 아닌 18입니다. 따라서 ranges를 사용할 때에는 이 점을 숙지해두세요: `upperBound`는 마지막 index보다 값이 하나 더 높습니다.

## 예제로 봅시다.

어떻게 알고리즙이 작동하는지 자세히 보는게 유용할 것입니다..

위의 예제에서의 배열은 19개의 숫자로 이루어져있고, 정렬되어있다면 다음과 같을 것입니다:

	[ 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67 ]

우리는 `43`이라는 숫자가 해당 배열에 있는지 확인해볼 것입니다.

배열을 반으로 나누기 위해 우리는 이 배열의 중간 값의 index를 알 필요가 있습니다. 다음 줄에서 해당 index를 구할 수 있습니다.:

```swift
let midIndex = range.lowerBound + (range.upperBound - range.lowerBound) / 2
```

range는 `lowerBound = 0`이며 `upperBound = 19`입니다. 우리는  `midIndex` 가 `0 + (19 - 0)/2 = 19/2 = 9` 인것을 확인할 수 있습니다. 실제로는 `9.5`이지만 우리는 정수를 사용하기 때문에 내림을 사용하여 `9`입니다.

다음으로 `*`는 중간 값을 가리킵니다. 보시다시피, 양쪽 숫자의 개수는 같으므로 중간을 기점으로 배열을 두개로 나눌 수 있습니다.

	[ 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67 ]
                                      *

이제 이진 탐색은 반으로 나눈 배열중 어떤 배열을 더 사용할지 특정합니다. 해당 부분에 대한 코드는 다음과 같습니다:

```swift
if a[midIndex] > key {
    // use left half
} else if a[midIndex] < key {
    // use right half
} else {
    return midIndex
}
```

이 경우, `a[midIndex] = 29` 입니다. `29`는 찾고자하는 search key보다 작기 때문에 우리는 왼쪽 배열에 우리가 찾고자 하는 값이 없다고 결론지을 수 있습니다.  그렇다면, 왼쪽 배열은 `29`보다 작은 값만 포함하고 있습니다. 따라서, search key는 무조건 오른쪽 배열에 있을 것입니다(그렇지 않다면 배열에 존재하지 않는 것입니다).

그럼 다시 이진 탐색을 반복합니다. 하지만 수행하는 배열의 간격은 `midIndex + 1`부터 `range.upperBound`로 합니다:

	[ x, x, x, x, x, x, x, x, x, x | 31, 37, 41, 43, 47, 53, 59, 61, 67 ]

왼쪽 배열의 값을 모두 `x`로 표시했기 떄문에 우리는 왼쪽 배열에 대해서 더이상 걱정하지 않아도 됩니다. 이제부터 우리는 index 10으로 시작하는 오른쪽 배열만 신경쓰면 됩니다.

다시 `midIndex = 10 + (19 - 10)/2 = 14`으로 중간 index를 다시 계산하였으며, 다시 중간을 기점으로 배열을 반으로 나눕니다.

	[ x, x, x, x, x, x, x, x, x, x | 31, 37, 41, 43, 47, 53, 59, 61, 67 ]
	                                                 *

보시다시피 오른쪽 배열의 중간 값은 `a[14]`입니다.

search key가 `a[14]`보다 작은가요 아니면 큰가요? `43 < 47`이기 때문에 더 작습니다. 이제 왼쪽 배열을 보고 오른쪽 배열은 무시하도록 합시다:

	[ x, x, x, x, x, x, x, x, x, x | 31, 37, 41, 43 | x, x, x, x, x ]

새로운 `midIndex`입니다:

	[ x, x, x, x, x, x, x, x, x, x | 31, 37, 41, 43 | x, x, x, x, x ]
	                                     *

search key가 `37` 보다 크기 떄문에 오른쪽 부분에서 계속합니다:

	[ x, x, x, x, x, x, x, x, x, x | x, x | 41, 43 | x, x, x, x, x ]
	                                        *

다시 search key가 더 크므로, 한번 더 분할하여 오른쪽 값을 얻습니다.:

	[ x, x, x, x, x, x, x, x, x, x | x, x | x | 43 | x, x, x, x, x ]
	                                            *

다 되었습니다. 찾고자 하는 search key가 배열의 요소와 일치합니다. 따라서 마침내 원하는 값을 찾았습니다: 숫자 `43` 은 index `13`입니다. 예~!

이러한 과정이 많은 작업으로 보일 수 있지만, 실제로 search key를 찾기 위해 고작 4단계만 거친 것입니다. 이진 탐색에서는 `log_2(19) = 4.23` 이지만, 만약 선형 탐색이었다면 14단계였을 것입니다. 

만약 `43`대신에 `42`를 찾았다면 어땠을까요? 이 경우에 더이상 배열을 분할하지 못했을 것입니다. `range.upperBound`가 `range.lowerBound`보다 작아지기 때문에 해당 알고리즘으로 값을 찾지 못하고 배열은 `nil`을 반환할 것입니다. 

> **Note:** Many implementations of binary search calculate `midIndex = (lowerBound + upperBound) / 2`. This contains a subtle bug that only appears with very large arrays, because `lowerBound + upperBound` may overflow the maximum number an integer can hold. This situation is unlikely to happen on a 64-bit CPU, but it definitely can on 32-bit machines.

## Iterative vs recursive

Binary search is recursive in nature because you apply the same logic over and over again to smaller and smaller subarrays. However, that does not mean you must implement `binarySearch()` as a recursive function. It's often more efficient to convert a recursive algorithm into an iterative version, using a simple loop instead of lots of recursive function calls.

Here is an iterative implementation of binary search in Swift:

```swift
func binarySearch<T: Comparable>(_ a: [T], key: T) -> Int? {
    var lowerBound = 0
    var upperBound = a.count
    while lowerBound < upperBound {
        let midIndex = lowerBound + (upperBound - lowerBound) / 2
        if a[midIndex] == key {
            return midIndex
        } else if a[midIndex] < key {
            lowerBound = midIndex + 1
        } else {
            upperBound = midIndex
        }
    }
    return nil
}
```

As you can see, the code is very similar to the recursive version. The main difference is in the use of the `while` loop.

Use it like this:

```swift
let numbers = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67]

binarySearch(numbers, key: 43)  // gives 13
```

## The end

Is it a problem that the array must be sorted first? It depends. Keep in mind that sorting takes time -- the combination of binary search plus sorting may be slower than doing a simple linear search. Binary search shines in situations where you sort just once and then do many searches.

See also [Wikipedia](https://en.wikipedia.org/wiki/Binary_search_algorithm).

*Written for Swift Algorithm Club by Matthijs Hollemans*
