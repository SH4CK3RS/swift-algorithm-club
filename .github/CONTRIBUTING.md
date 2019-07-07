# 기여 가이드라인

Swift Algorithm Club을 도와주고싶으신가요? 좋습니다! 기여에 대한 엄격한 규격 또는 규칙이 있는것은 아니지만 몇가지 숙지해야할 가이드를 제공합니다:

**가독성**

해당 저장소는 배움에 관한것만들 다룹니다. `README`파일은 케이크이며 샘플코드는 그위에 올려진 체리와 같습니다. 좋은 기여는 다이어그램을 활용한 간결한 설명입니다. 코드는 청크(chunk)에 잘 소개되며, 관련된 설명이 잘 되어있어야합니다.

> 간결함과 성능중에 하나를 선택해야한다면, 구현에 있어 시간 복잡성이 동일한 한 간결함의 측면을 좀 더 고려해야합니다. 이후에 성능상으로 더 좋은 방법을 제안할 수 있습니다.

**API 디자인 가이드라인**

훌륭한 기여는 [Swift API Guidelines](https://swift.org/documentation/api-design-guidelines/)를 준수하는것입니다. 우리는 이를 토대로 pull request를 리뷰합니다.

**Swift 언어 가이드라인**

우리는 Swift [style guide](https://github.com/raywenderlich/swift-style-guide)를 따릅니다.

## 기여 카테고리

### Refinement

유닛 테스트. 오타수정. 그 어떤 기여도 작지 않습니다. :-)

저장소에는 100여개 이상의 다른 데이터 구조와 알고리즘을 가지고 있습니다. 우리는 언제나 이미 존재하는 적용방법 및 설명에 대한 개선에 대해 많은 관심을 가지고 있습니다. 좀 더 Swift스러운 그리고 표준 라이브러리와 제일 잘 맞는 코드 생성에 대한 제안은 언제나 환영입니다.

### 새로운 기여

새로운 것을 작성하기전에 먼저 두가지를 수행해주세요:

1. 메인페이지에 이미 존재하는 적용방법인지 확인해주세요
2. [pull requests](https://github.com/raywenderlich/swift-algorithm-club/pulls)에서 "claimed" 토픽을 확인해주세요. 아래에 좀더 자세한 설명이 있습니다.

새로운 것을 추가할 마음이 있으시다면, 기여하실 때 아래의 과정을 따라주세요:

1. "Clain"에 알고리즘 또는 자료구조에 대한 pull request를 생성하세요. 여러 사람이 같은 주제에 대한 작업을 피하기 위함입니다.
2. 코드 작성시 이 [스타일 가이드](https://github.com/raywenderlich/swift-style-guide)를 사용하세요.
3. 어떻게 알고리즘이 작동하는지에 대한 설명을 작성해주세요. 독자들이 따라할 수 있도록 **plenty of examples**를 포함해주세요. 사진도 좋습니다. [the explanation of quicksort](../Quicksort/)를 참조하여 아이디어를 얻으세요.
4. 문서 마지막에 *Written by Your Name* 처럼 설명에 당신의 이름을 포함하세요.
5. playground나 unit test를 추가하세요.

unit test의 경우:

- `.travis.yml`에 unit project를 추가하여 [Travis-CI](https://travis-ci.org/raywenderlich/swift-algorithm-club)에서 실행할 수 있도록 하세요. `.travis.yml`에 다음과 같이 라인을 추가하세요:

```
- xctool test -project ./Algorithm/Tests/Tests.xcodeproj -scheme Tests
```

- Travis-CI를 실행하기 위해 테스트 프로젝트의 scheme를 다음과 같이 구성하세요:
    - Open **Product -> Scheme -> Manage Schemes...**
    - Uncheck **Autocreate schemes**
    - Check **Shared**

![Screenshot of scheme settings](../Images/scheme-settings-for-travis.png)
