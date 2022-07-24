# CSS로 이미지를 중앙 정렬하는 방법

#### 구나영 번역 (Nayoung Gu)

![액자 틀에 담긴 풍경 사진](https://cdn-media-2.freecodecamp.org/w1280/5f9c9a4c740569d1a4ca24c2.jpg)

영어 원문: [How to Center an Image Vertically and Horizontally with CSS](https://www.freecodecamp.org/news/how-to-center-an-image-in-css/)<br>
글쓴이: [Cem Eygi](https://www.freecodecamp.org/news/author/cemeygi/)

### 많은 개발자들이 이미지 작업을 할 때 어려움을 느끼곤 합니다. [반응형](https://www.freecodecamp.org/news/css-responsive-image-tutorial/)과 정렬, 특히 이미지를 페이지 정중앙에 배치하는 것을 어려워합니다.

이번 글에서는 다양한 CSS 속성을 활용해 이미지를 수직 및 수평으로 가운데 정렬할 수 있는 가장 일반적인 방법을 소개해 드리려고 합니다.

CSS [Position](https://www.freecodecamp.org/news/how-to-use-the-position-property-in-css-to-align-elements-d8f49c403a26/)과 [Display](https://www.youtube.com/watch?v=hgoFi0fCv3w) 속성은 이전 글에서 다룬 적이 있습니다. 아직 이 속성들이 낯설게 느껴지신다면, 이번 글을 읽기 전에 이전 포스트를 읽어보시길 추천해 드립니다.

관심 있는 분들을 위해 영상 버전도 첨부합니다:<br>
[![Video Label](https://img.youtube.com/vi/mwVNVxpkly0/0.jpg)](https://www.youtube.com/watch?v=mwVNVxpkly0?t=0s)

## 수평적으로 이미지 가운데 정렬하기

먼저 CSS 속성을 사용해 이미지를 수평 중앙에 정렬할 수 있는 세 가지 방법에 대해 알아봅시다.

### Text-Align

이미지를 가로 중앙에 배치할 수 있는 첫 번째 방법은 `text-align` 속성을 사용하는 것입니다. 하지만 이 방법은 이미지가 `<div>`와 같은 블록 레벨 컨테이너 안에 있을 때만 작동합니다:

```
<style>
    div {
        text-align: center;
    }
</style>

<div>
    <img src="your-image.jpg">
</div>
```

### Margin: Auto

또 다른 방법은 `margin: auto` 속성을 사용하는 것입니다.

하지만 `margin: auto` 자체만으로는 이미지를 중앙 정렬할 수 없습니다. `margin: auto`를 사용하려면 다른 두 가지 속성을 함께 적용해야 합니다.

margin-auto 속성은 인라인 요소에 아무 영향을 미치지 않습니다. 따라서 인라인 요소인 `<img>` 태그의 경우 먼저 이를 블록 레벨 요소로 먼저 바꿔주어야 합니다.

```
img {
    margin: auto;
    display: block;
}
```

두 번째는 너비입니다. 왼쪽과 오른쪽 마진이 나머지 빈 공간에 자리를 잡아 자동으로 가운데 정렬이 적용되기 때문입니다. 단, 너비가 100%로 지정되지 않은 경우에 한해서요.

```
img {
    width: 60%;
    margin: auto;
    display: block;
}
```

### Display: Flex

세 번째 방법은 `display: flex`를 사용하는 것입니다. 컨테이너 요소에 `text-align` 속성을 사용했던 것처럼 컨테이너에 `display: flex`를 똑같이 사용해 줄 수 있습니다.

하지만 `display: flex`만으로는 부족합니다. 컨테이너 요소는 `justify-content`라 불리는 추가적인 속성을 가져야 합니다:

```
div {
    display: flex;
    justify-content: center;
}

img {
    width: 60%;
}
```

`justify-content`는 이미지를 수평 중앙 정렬을 할 때 `display: flex`와 함께 사용되는 속성입니다.

마지막으로 이미지의 너비는 컨테이너의 넓이보다 작아야 합니다. 그렇지 않으면 이미지가 공간 너비의 100%를 차지하게 되므로 중앙 정렬을 할 수 없습니다.

**주의할 점:** `display: flex` 속성은 오래된 버전의 브라우저에서는 지원되지 않습니다. 구체적인 내용은 [이 링크](https://caniuse.com/?search=display%20flex)를 참고하세요.

## 수직적으로 이미지 가운데 정렬하기

### Display: Flex

수직 정렬을 할 때도 `display: flex`가 큰 도움이 될 수 있습니다.

컨테이너 요소의 높이가 800px이고, 이미지의 높이가 500px밖에 되지 않는다고 가정해 봅시다.

```
div {
    display: flex;
    justify-content: center;
    height: 800px;
}

img {
    width: 60%;
    height: 500px;
}
```

이때는 `align-items: center`라는 한 줄의 코드만으로 중앙 정렬을 할 수 있습니다.

```
div {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 800px;
}
```

`align-items`는 `display: flex`와 함께 사용될 때 요소를 수직으로 정렬하는 속성입니다.

### Position: Absolute & Transform 속성

또 다른 방법은 `position`과 `transform` 속성을 함께 사용하는 것입니다. 이 방법은 조금 복잡하기 때문에 한 단계씩 해보겠습니다.

### Step 1: Position Absolute 설정하기

먼저, 이미지의 `position` 속성을 `static`에서 `absolute`로 바꿔줍니다.

```
div {
    height: 800px;
    position: relative;
    background: red;
}

img {
    width: 80%;
    position: absolute;
}
```

이미지가 상대적으로 위치한 컨테이너 요소 안에 위치해야 하므로, 컨테이너 `div`에 `position: relative` 속성을 부여해줍니다.

### Step 2: Top & Left 속성 부여하기

두 번째로, 이미지의 위와 왼쪽 속성을 50%로 설정합니다. 이렇게 하면 이미지의 시작 지점(좌상단)이 컨테이너의 중간 지점이 될 것입니다.

```
img {
    width: 80%;
    position: absolute;
    top: 50%;
    left: 50%;
}
```

### Step 3: Transform 속성 부여하기

위의 두 번째 단계까지 적용하면 이미지의 일부가 컨테이너의 밖으로 빠져나오게 됩니다. 이제 이미지를 다시 돌려놓아야 합니다.

`transform` 속성으로 X축, Y축 모두 -50%를 적용하면 비로소 이미지가 중앙에 배치됩니다.

```
img {
    width: 80%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

이 외에도 다른 방법들이 더 있지만 가장 일반적으로 사용되는 방법들을 소개해 드렸습니다. 이 글이 이미지 가운데 정렬을 이해하는 데 도움이 되었으면 좋겠습니다. 영어 원문을 읽고 싶으시다면 [How to Center an Image Vertically and Horizontally with CSS](https://www.freecodecamp.org/news/how-to-center-an-image-in-css/)를 읽어보세요.

**웹 개발을 더 공부하고 싶으시다면 제 [유튜브 채널](https://www.youtube.com/channel/UC1EgYPCvKCXFn8HlpoJwY3Q?view_as=subscriber)을 방문해 주세요.**

읽어주셔서 감사합니다!
