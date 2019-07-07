# 스텍

스텍은 배열같지만 제한적인 기능을 가지고 있습니다. 오직 스텍의 탑에 새로운 요소를 추가하기 위하여 *push*를 이용허고, 다시 탑으로부터 데이터를 지우기 위해 *pop을 사용합니다. 그리고 탑으로부터 데이터를 *pop*하지 않고 가져오기 위해 *peek*을 사용합니다.

왜 이걸 하려고 하냐구요? 글쎄요.. 많은 알고리즘에서 임시 목록에 데이터를 추가하고 싶을수도 있으며 마지막에 빼고싶을 수도 있겠죠. 이렇게 값을 추가하고 제거하는 순서가 중요할 때가 많습니다.

스텍은 LIFO(last-in first-out)구조입니다.. 가장 마지막에 push한 값이 pop할때 가장 먼저 나오는거죠. (비슷한 자료구조로 [큐](../Queue/)가 있는데 이것은 FIFO(first-in first-out.)구조입니다.)

예를들어 스텍이 숫자를 Push해봅시다:

```swift
stack.push(10)
```

스텍은 지금 `[ 10 ]`입니다. 다음 숫자를 Push해봅시다:

```swift
stack.push(3)
```

스텍은 지금 `[ 10, 3 ]`입니다. 번호를 하나 더 Push해봅시다:

```swift
stack.push(57)
```

스텍은 지금 `[ 10, 3, 57 ]`입니다. 스텍의 탑에 있는 숫자를 Pop해봅시다:

```swift
stack.pop()
```

그러면 `57`을 반환합니다, 왜냐하면 `57`은 우리가 가장 최근에 Push한 숫자이기 때문입니다. 다시 스텍은  `[ 10, 3 ]`입니다.

```swift
stack.pop()
```

이번에는 `3`을 반환하며, 계속 똑같이 실행됩니다. 만약 스텍이 비어있다면 Pop하는 작업은 `nil`을 반환하거나, 어떤 실행에서는 ("stack underflow”)라는 오류 메시지를 보여줄 것입니다.

스위프트에서 스텍을 만드는 것은 쉽습니다. 이것은 단순히 배열 주위를 둘러싸고, Push,Pop 그리고 스텍의 탑 부분을 볼 수 있게 해줍니다.

```swift
public struct Stack<T> {
  fileprivate var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }

  public var count: Int {
    return array.count
  }

  public mutating func push(_ element: T) {
    array.append(element)
  }

  public mutating func pop() -> T? {
    return array.popLast()
  }

  public var top: T? {
    return array.last
  }
}
```

Push가 배열의 시작지점이 아닌 마지막에 새로운 값을 추가한다는 것을 알아두새요. 배열의 처음 부분에 값을 삽입하는 것은 **O(n)**만큼의 수행을 요구합니다. 왜냐하면 존재하는 배열의 요소들을 한칸씩 옮겨야하기 때문입니다.  반면에 마지막에 값을 추가하는 것은 **O(1)**정도의 성능이라 배열의 크기에 상관없이 항상 같은양의 시간을 요구합니다.

스텍의 재밌는 사실: 함수 또는 메소드를 호출할 떄마다, CPU는 반환 주소를 스텍에 위치시킵니다. 함수가 끝나면 CPU는 반환 주소를 이용해 호출 지점으로 돌아갑니다.
만약 많은 함수를 호출하게 되면 — 예를들어 끝나지 않는 재귀함수를 호출하게 되면 CPU의 스텍 공간이 넘치게 되어 흔히 말하는 스텍 오버플로우가 발생하게됩니다.

*Written for Swift Algorithm Club by Matthijs Hollemans*

*Translated By Byeonggeun Son*
