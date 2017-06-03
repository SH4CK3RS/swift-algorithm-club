# 삽입 정렬

목표: 배열을 낮은쪽에서 높은쪽으로(또는 높은쪽에서 낮은쪽으로) 정렬할 수 있다.

당신은 숫자로 이루어진 배열이 주어져 있고, 알맞은 순서로 정렬을 해야합니다. 삽입 정렬 알고리즘은 다음과 같이 작동합니다:

숫자를 더미에 쌓습니다. 숫자더미들은 정렬되어있지않습니다.
숫자더미로부터 숫자를 고릅니다. 어떤 숫자를 고를지는 중요하지 않지만 가장 쉬운 방법은 숫자더미의 가장 위에 있는 숫자를 고르는 것입니다.
고른 숫자를 새로운 배열에 집어넣습니다.
다음 숫자를 정렬되지 않은 숫자더미에서 고르고 또 다시 새로운 배열에 집어 넣습니다. 그리고 처음 고른 숫자 뒤 또는 앞으로 방금 고른 숫자를 집어넣어 두 숫자가 정렬되도록합니다.
다시 숫자를 고르고 배열에 적절히 정렬된 위치에 넣어줍니다.
숫자더미에 더이상 숫자가 존재하지 않을 때까지 이 과정을 반복합니다. 그러면 빈 숫자더미와 정렬된 배열을 얻었을 것입니다.

숫자더미에서 숫자를 뽑아 배열의 적절히 정렬된 위치로 넣는다는것 때문에 “삽입" 정렬로 불립니다.

## 예제

`[ 8, 3, 5, 4, 6 ]` <— 이 숫자들이 정렬이 필요한 숫자라고 합시다. 이것은 정렬되지 않은 숫자더미입니다.

첫번째 숫자인 `8`을 고르고 새로운 배열에 넣어줍니다. 아직 배열이 없기때문에 이 작업은 쉽습니다. 그럼 정렬된 배열은 지금 `[ 8 ]`이며 숫자더미는 `[ 3, 5, 4, 6 ]` 입니다.

숫자더미에서 다음 숫자인 `3`을 고르고 방금 정렬돈 배열에 넣어줍니다. 이번 숫자는 `8` 앞으로 가야하기 때문에 이번에 정렬된 배열은 `[ 3, 8 ]`입니다. 그리고 숫자더미는 `[ 5, 4, 6 ]`입니다.

다음 숫자인 `5`를 뽑아 다시 정렬된 배열에 넣어줍니다. 이번 숫자는 `3`과 `8`사이에 넣어줍니다. 그러면 정렬된 배열은 현재 `[ 3, 5, 8 ]`이며, 숫자더미는 `[ 4, 6 ]`입니다.

숫자더미에서 숫자를 다 뽑을 때까지 이 작업을 반복합니다.

## 현재 위치 정렬

위의 설명대로라면 두개의 배열이 필요한 것처럼 보입니다. 하나는 정렬되지 않은 숫자더미이며 나머지 하나는 정렬된 숫서의 숫자들을 가지고있습니다.

하지만 분리된 배열을 만드는 대신 *현재 위치*를 참고하여 삽입 정렬을 사용 할 수 있습니다.
But you can perform the insertion sort *in-place*, without having to create a separate array. 단순히 배열을 하나하나 따라가며 어느부분이 정렬되어있고 어느부분이 정렬돼야할  숫자더미인지를 구분할 수 있습니다.

`[ 8, 3, 5, 4, 6 ]`라는 배열로 시작합시다. `|`는 정렬된부분의 끝과 정렬돼야할 숫자더미의 경계를 보여줍니다:

	[| 8, 3, 5, 4, 6 ]

위의 배열은 정렬된 부분이 비어있으며, 정렬돼야할 숫자더미가  `8`로 시작된다는것을 보여줍니다.
처음 숫자를 지나게 되면 다음과 같은 배열을 가지게됩니다:

	[ 8 | 3, 5, 4, 6 ]

정렬된 부분은 `[ 8 ]`이며 정렬돼야할 부분은 `[ 3, 5, 4, 6 ]`입니다. `|`가 한칸 오른족으로 이동되었습니다.

아래 배열들이 어떤식으로 정렬이 되는지를 보여줍니다:

	[| 8, 3, 5, 4, 6 ]
	[ 8 | 3, 5, 4, 6 ]
	[ 3, 8 | 5, 4, 6 ]
	[ 3, 5, 8 | 4, 6 ]
	[ 3, 4, 5, 8 | 6 ]
	[ 3, 4, 5, 6, 8 |]

각 단계에서  `|` 는 한칸씩 이동합니다. 위에서 볼수 있듯이 `|`가 이동하면서 배열이 정렬이 됩니다. 숫자더미는 숫자가 없고 더이상 정렬될 숫자가 없을 때까지 숫자 더미가 하나씩 줄어들고 정렬된 배열이 하나씩 증가합니다. 

## 어떻게 삽입할까요?

각 단계에서 정렬되지 않으 숫자더미의 가장 위에서부터 숫자를 집어 배열의 정렬된 부분에 집어넣습니다. 꼭 숫자를 적절한 부분에 위치시켜 배열의 시작부터 정렬되도록 하여야합니다. 그럼 어떻게 작동되는 걸까요?

그럼 처음 몇개의 요소가 아래와 같이 정렬되어 있다고 합시다:

	[ 3, 5, 8 | 4, 6 ]

다음 숫자는 `4`이며, 나머지 `[ 3, 5, 8 ]` 를 어딘가 정렬될 위치에 넣어야 합니다.

정렬하는 방법: `|`이전에 있는 숫자  `8`을 먼저 보세요. 

	[ 3, 5, 8, 4 | 6 ]
	        ^
	        
이 값이 `4`보다 큰가요? 맞습니다, 그래서 `4`는 `8` 앞으로 와야 합니다. 우리는 아래와 같은 배열을 얻기 위해 두 숫자의 위치를 바꿔줍니다:

	[ 3, 5, 4, 8 | 6 ]
	        <-->
	       자리 바뀜

아직 정렬해야할 부분이 남았습니다. 새로이 앞에 있는 값인 `5` 또한 `4` 보다 큽니다. 그래서 우리는 이 두 숫자 또한 자리를 바꿔주어야합니다.:

	[ 3, 4, 5, 8 | 6 ]
	     <-->
	    자리 바뀜

[추후 번역 예정]
Again, look at the previous element. Is `3` greater than `4`? No, it is not. That means we're done with number `4`. The beginning of the array is sorted again.

This was a description of the inner loop of the insertion sort algorithm, which you'll see in the next section. It inserts the number from the top of the pile into the sorted portion by swapping numbers.

## The code

Here is an implementation of insertion sort in Swift:

```swift
func insertionSort(_ array: [Int]) -> [Int] {
  var a = array                             // 1
  for x in 1..<a.count {                    // 2
    var y = x
    while y > 0 && a[y] < a[y - 1] {        // 3
      swap(&a[y - 1], &a[y])
      y -= 1
    }
  }
  return a
}
```

Put this code in a playground and test it like so:

```swift
let list = [ 10, -1, 3, 9, 2, 27, 8, 5, 1, 3, 0, 26 ]
insertionSort(list)
```

Here is how the code works.

1. Make a copy of the array. This is necessary because we cannot modify the contents of the `array` parameter directly. Like Swift's own `sort()`, the `insertionSort()` function will return a sorted *copy* of the original array.

2. There are two loops inside this function. The outer loop looks at each of the elements in the array in turn; this is what picks the top-most number from the pile. The variable `x` is the index of where the sorted portion ends and the pile begins (the position of the `|` bar). Remember, at any given moment the beginning of the array -- from index 0 up to `x` -- is always sorted. The rest, from index `x` until the last element, is the unsorted pile.

3. The inner loop looks at the element at position `x`. This is the number at the top of the pile, and it may be smaller than any of the previous elements. The inner loop steps backwards through the sorted array; every time it finds a previous number that is larger, it swaps them. When the inner loop completes, the beginning of the array is sorted again, and the sorted portion has grown by one element.

> **Note:** The outer loop starts at index 1, not 0. Moving the very first element from the pile to the sorted portion doesn't actually change anything, so we might as well skip it. 

## No more swaps

The above version of insertion sort works fine, but it can be made a tiny bit faster by removing the call to `swap()`. 

You've seen that we swap numbers to move the next element into its sorted position:

	[ 3, 5, 8, 4 | 6 ]
	        <-->
            swap
	        
	[ 3, 5, 4, 8 | 6 ]
         <-->
	     swap

Instead of swapping with each of the previous elements, we can just shift all those elements one position to the right, and then copy the new number into the right position.

	[ 3, 5, 8, 4 | 6 ]   remember 4
	           *
	
	[ 3, 5, 8, 8 | 6 ]   shift 8 to the right
	        --->
	        
	[ 3, 5, 5, 8 | 6 ]   shift 5 to the right
	     --->
	     
	[ 3, 4, 5, 8 | 6 ]   copy 4 into place
	     *

In code that looks like this:

```swift
func insertionSort(_ array: [Int]) -> [Int] {
  var a = array
  for x in 1..<a.count {
    var y = x
    let temp = a[y]
    while y > 0 && temp < a[y - 1] {
      a[y] = a[y - 1]                // 1
      y -= 1
    }
    a[y] = temp                      // 2
  }
  return a
}
```

The line at `//1` is what shifts up the previous elements by one position. At the end of the inner loop, `y` is the destination index for the new number in the sorted portion, and the line at `//2` copies this number into place.

## Making it generic

It would be nice to sort other things than just numbers. We can make the datatype of the array generic and use a user-supplied function (or closure) to perform the less-than comparison. This only requires two changes to the code.

The function signature becomes:

```swift
func insertionSort<T>(_ array: [T], _ isOrderedBefore: (T, T) -> Bool) -> [T] {
```

The array has type `[T]` where `T` is the placeholder type for the generics. Now `insertionSort()` will accept any kind of array, whether it contains numbers, strings, or something else.

The new parameter `isOrderedBefore: (T, T) -> Bool` is a function that takes two `T` objects and returns true if the first object comes before the second, and false if the second object should come before the first. This is exactly what Swift's built-in `sort()` function does.

The only other change is in the inner loop, which now becomes:

```swift
      while y > 0 && isOrderedBefore(temp, a[y - 1]) {
```

Instead of writing `temp < a[y - 1]`, we call the `isOrderedBefore()` function. It does the exact same thing, except we can now compare any kind of object, not just numbers.

To test this in a playground, do:

```swift
let numbers = [ 10, -1, 3, 9, 2, 27, 8, 5, 1, 3, 0, 26 ]
insertionSort(numbers, <)
insertionSort(numbers, >)
```

The `<` and `>` determine the sort order, low-to-high and high-to-low, respectively.

Of course, you can also sort other things such as strings,

```swift
let strings = [ "b", "a", "d", "c", "e" ]
insertionSort(strings, <)
```

or even more complex objects:

```swift
let objects = [ obj1, obj2, obj3, ... ]
insertionSort(objects) { $0.priority < $1.priority }
```

The closure tells `insertionSort()` to sort on the `priority` property of the objects.

Insertion sort is a *stable* sort. A sort is stable when elements that have identical sort keys remain in the same relative order after sorting. This is not important for simple values such as numbers or strings, but it is important when sorting more complex objects. In the example above, if two objects have the same `priority`, regardless of the values of their other properties, those two objects don't get swapped around.

## Performance

Insertion sort is really fast if the array is already sorted. That sounds obvious, but this is not true for all search algorithms. In practice, a lot of data will already be largely -- if not entirely -- sorted and insertion sort works quite well in that case.

The worst-case and average case performance of insertion sort is **O(n^2)**. That's because there are two nested loops in this function. Other sort algorithms, such as quicksort and merge sort, have **O(n log n)** performance, which is faster on large inputs.

Insertion sort is actually very fast for sorting small arrays. Some standard libraries have sort functions that switch from a quicksort to insertion sort when the partition size is 10 or less.

I did a quick test comparing our `insertionSort()` with Swift's built-in `sort()`. On arrays of about 100 items or so, the difference in speed is tiny. However, as your input becomes larger, **O(n^2)** quickly starts to perform a lot worse than **O(n log n)** and insertion sort just can't keep up.

## See also

[Insertion sort on Wikipedia](https://en.wikipedia.org/wiki/Insertion_sort)

*Written for Swift Algorithm Club by Matthijs Hollemans*
