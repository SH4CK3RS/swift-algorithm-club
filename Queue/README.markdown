# 큐(Queue)

큐는 새로운 아이템을 뒤에만 추가할 수 있고 앞에서만 데이터를 지울 수 있는 리스트입니다. 확실히 처음 넣은 데이터가 가장 먼저 나오는 아이템입니다. 즉 FIFO(first in, first out)입니다.

왜 이걸 하려고 하냐구요? 글쎄요.. 많은 알고리즘에서 임시 목록에 데이터를 추가하고 싶을수도 있으며 마지막에 빼고싶을 수도 있겠죠. 이렇게 값을 추가하고 제거하는 순서가 중요할 때가 많습니다.

큐는 FIFO(first-in, first-out)의 순서로 작동합니다. 가장 먼저 넣은 값이 가장 먼저 나오는 값이 될 것입니다. 그래서 이것은 공평합니다.(비슷한 자료구조로 [스텍](../Stack/)이 있으며 스텍은 LIFO(last-in first-out)의 순서로 작동합니다.)

여기 숫자를 큐에 enqueue 예제가 있습니다.
Here is an example to enqueue a number:

```swift
queue.enqueue(10)
```

큐는 현재 `[ 10 ]`입니다. 큐에 다음 숫자를 더해줍시다:

```swift
queue.enqueue(3)
```

큐는 현재 `[ 10, 3 ]`입니다. 숫자 하나를 더 더해봅시다:

```swift
queue.enqueue(57)
```

큐는 현재`[ 10, 3, 57 ]`입니다. 큐에 처음에 넣은 값이 나오도록 dequeue해봅시다

```swift
queue.dequeue()
```

`10`을 리턴합니다. 왜냐하면 `10`이 우리가 처음에 넣은 값이기 때문입니다. 현재 큐는`[ 3, 57 ]`입니다. 

한번 더 dequeue해봅시다
```swift
queue.dequeue()
```

`3`을 리턴합니다. 계속해서 다음 dequeue는 `57`을 리턴합니다. 만약 큐가 비어있다면 dequeue는`nil`을 리턴하거나, 에러메시지를 출력할 것입니다.

> **Note:** 큐가 항상 최선의 선택은 아닙니다. 만약 값이 더해지고 지워지는 순서가 중요하지 않은 리스트라면 큐 대신에 스텍을 사용하세요. 스텍이 더 단순하고 빠릅니다.
## The code

아래 코드는 가장 단순하게 큐가 Swift로 실행되는 코드입니다. 배열에서 enqueue, dequeue 그리고 peek할 수 있도록 하고 있습니다.

```swift
public struct Queue<T> {
  fileprivate var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }
  
  public var count: Int {
    return array.count
  }

  public mutating func enqueue(_ element: T) {
    array.append(element)
  }
  
  public mutating func dequeue() -> T? {
    if isEmpty {
      return nil
    } else {
      return array.removeFirst()
    }
  }
  
  public var front: T? {
    return array.first
  }
}
```

이 큐는 잘 작동하지만 바람직한 방법은 아닙니다.

Enqueue 하는것은 **O(1)**의 성능을 냅니다. 왜냐하면 배열 마지막에 값을 더하는 것은 배열의 크기에 상관없이 항상 같은 시간을 요구하기 때문입니다.

아이템을 배열에 더하는 것이 왜 **O(1)**만큼의 성능을 내는지 궁금해 할 것입니다.. 왜냐하면 스위프트는 항상 끝에 빈 공간이 있기때문입니다. 

만약 우리가 다음과 같이 코드를 작성한다면:

```swift
var queue = Queue<String>()
queue.enqueue("Ada")
queue.enqueue("Steve")
queue.enqueue("Tim")
```
배열은 아마 다음과 같이 보일 것입니다:

	[ "Ada", "Steve", "Tim", xxx, xxx, xxx ]
`xxx`가 있는곳은 예약되어 있지만 아직 채워지지 않은 메모리입니다. 새로은 값을 배열에 추가하는 것은 사용되지 않은 공간을 덮어쓰는 것과 같습니다:

	[ "Ada", "Steve", "Tim", "Grace", xxx, xxx ]
메모리의 한 공간으로부터 다른 공간으로 복사한 결과는 항상 동일한 시간 성능을 가집니다.

여기에는 제한적인 양의 미사용 공간이 배열 끝에 있습니다. 만약 마지막 `xxx`가 사용된다면 다음 아이템을 추가하고 싶을 것입니다. 그럼 배열은 더많은 공간을 만들기 위해 크기를 재조정할 필요가 있습니다.

크기를 재조정하는것은 새로운 메모리를 할당하고 존재하는 모든 데이터를 새로운 배열에 복사하는 작업을 포함합니다. 이것은 **O(n)**정도의 성능으로 조금 느립니다. 이러한 작업은 가끔 발생하지만 새로운 값을 추가하는데 걸리는 시간은 평균적으로**O(1)** 정도입니다.

하지만 dequeue하는 것은 다른 이야기입니다. dequeue하기 위해서는 우리는 배열의 시작점(처음)에 있는 값을 지워야 합니다. 이 작업은 항상 **O(n)** 의 성능을 요구합니다. 왜냐하면 배열에 존재하는 모든 값들을 메모리로부터 이동되어야하기 때문입니다.

우리의 예제에서, `”Ada"`를 dequeue하는것은 `"Steve"`를 `”Ada"`위치에 복사하고, `"Tim"`을`"Steve"`위치에, 그리고 `”Grace"`를 `”Tim”`위치에 복사하는 것입니다.:

	before   [ "Ada", "Steve", "Tim", "Grace", xxx, xxx ]
	                   /       /      /
	                  /       /      /
	                 /       /      /
	                /       /      /
	 after   [ "Steve", "Tim", "Grace", xxx, xxx, xxx ]
 
메모리에 있는 이러한 모든 값을을 이동하는 것은 항상 **O(n)**성능을 요구합니다. 따라서 위의 간단한 실행에서 enqueue하는 것은 효과적이지만, dequeue하는 작업은 바람직하지 않습니다

## 더 효과적인 큐

dequeue하는것을 더 효과적으로 만들려면 enqueue와 마찬가지로 여분의 여유 공간을 예약하는 것입니다. 하지만 이번에는 뒤가 아닌 앞에 그 공간을 만들어야합니다. 스위프트에서 기본적으로 제공하는 배열에는 이러한 기능을 제공하지 않으므로 이 코드를 우리가 직접 작성해야합니다.

결국 목표는 언제든지 값을 dequeue하든지 배열의 값들을 앞으로 옮기지 않는 것입니다(느리기때문에) 그 대신에 그 자리가 비어있다고 표시하는 겁니다.
`”Ada"`를 dequeue하면 배열은 다음과 같을 것입니다:

	[ xxx, "Steve", "Tim", "Grace", xxx, xxx ]

`”Steve"`를 dequeue하면, 배열은 다음과 같을 것입니다:

	[ xxx, xxx, "Tim", "Grace", xxx, xxx ]

앞에 있는 빈 공간은 절대 다시 사용하지 않을 것이기때문에 주기적으로 나머지 값들을 앞으로 옮김으로써 배열을 정돈시킬 수 있습니다.:

	[ "Tim", "Grace", xxx, xxx, xxx, xxx ]

이렇게 정돈하는 순서는 메모리 이동을 요구하므로 **O(n)**의 성능을 냅니다. 왜냐하면 이러한 작업은 한번 작업되지만 dequeue하는 작업은 평균저긍로 **O(1)**정도의 성능입니다.

아래 코드는 위의 코드를 적용한 버전의 큐입니다::

```swift
public struct Queue<T> {
  fileprivate var array = [T?]()
  fileprivate var head = 0
  
  public var isEmpty: Bool {
    return count == 0
  }

  public var count: Int {
    return array.count - head
  }
  
  public mutating func enqueue(_ element: T) {
    array.append(element)
  }
  
  public mutating func dequeue() -> T? {
    guard head < array.count, let element = array[head] else { return nil }

    array[head] = nil
    head += 1

    let percentage = Double(head)/Double(array.count)
    if array.count > 50 && percentage > 0.25 {
      array.removeFirst(head)
      head = 0
    }
    
    return element
  }
  
  public var front: T? {
    if isEmpty {
      return nil
    } else {
      return array[head]
    }
  }
}
```

이 배열은 자리에 값이 비어있다는 것을 표현해줘야 하기때문에 `T` 가 아닌 `T?`타입의 객체를 저장합니다.  `head`  변수는 배열에서 가장 앞에 있는 값을 가리킵니다.(실제로 값이 존재하는 구간의 제일 앞부분)

대부분의 새로운 기능은 `dequeue()`에 있습니다. 아이템을 dequeue할 때 배열로부터 객체를 지우기 위해 `array[head]`를 `nil`로 설정합니다.  Then, we increment `head` because the next item has become the front one.

We go from this:

	[ "Ada", "Steve", "Tim", "Grace", xxx, xxx ]
	  head

to this:

	[ xxx, "Steve", "Tim", "Grace", xxx, xxx ]
	        head

이것은 마치 슈퍼마켓에 있는 사람들에 계산을 하기위해 새치기를 하지 않고 줄을 서 있는것과 같습니다. 하지만 계산은 큐처럼 이루어집니다.

배열의 앞부분에 있는 빈 공간을 지우지 않고 계속해서 enqueue 및 dequeue를 한다면 배열의 크기는 한없이 커질 것입니다. 아래에 코드에 구현된 것처럼 주기적으로 배열을 정돈해주세요:

```swift
    let percentage = Double(head)/Double(array.count)
    if array.count > 50 && percentage > 0.25 {
      array.removeFirst(head)
      head = 0
    }
```
위의 코드는 시작 부분에 있는 빈공간과 배열의 크기에 대한 비율을 계산합니다. 그래서 만약 사용하지 않는 공간의 비율이 25%가 넘는다면 낭비되는 공간을 걸러냅니다. 하지만 만약 배열의 크기가 작다면 항상 사이즈를 재조정하는 것은 아닙니다. 그래서 배열을 정돈해주려면 최소한 50개의 요소가 배열에 존재해야합니다.

[계속 번역중]
> **Note:** I just pulled these numbers out of thin air -- you may need to tweak them based on the behavior of your app in a production environment.

To test this in a playground, do the following:

```swift
var q = Queue<String>()
q.array                   // [] empty array

q.enqueue("Ada")
q.enqueue("Steve")
q.enqueue("Tim")
q.array             // [{Some "Ada"}, {Some "Steve"}, {Some "Tim"}]
q.count             // 3

q.dequeue()         // "Ada"
q.array             // [nil, {Some "Steve"}, {Some "Tim"}]
q.count             // 2

q.dequeue()         // "Steve"
q.array             // [nil, nil, {Some "Tim"}]
q.count             // 1

q.enqueue("Grace")
q.array             // [nil, nil, {Some "Tim"}, {Some "Grace"}]
q.count             // 2
```

To test the trimming behavior, replace the line,

```swift
    if array.count > 50 && percentage > 0.25 {
```

with:

```swift
    if head > 2 {
```

Now if you dequeue another object, the array will look as follows:

```swift
q.dequeue()         // "Tim"
q.array             // [{Some "Grace"}]
q.count             // 1
```

The `nil` objects at the front have been removed, and the array is no longer wasting space. This new version of `Queue` is not more complicated than the first one but dequeuing is now also an **O(1)** operation, just because we were aware about how we used the array.

## See also

There are many ways to create a queue. Alternative implementations use a [linked list](../Linked%20List/), a [circular buffer](../Ring%20Buffer/), or a [heap](../Heap/). 

Variations on this theme are [deque](../Deque/), a double-ended queue where you can enqueue and dequeue at both ends, and [priority queue](../Priority%20Queue/), a sorted queue where the "most important" item is always at the front.

*Written for Swift Algorithm Club by Matthijs Hollemans*
