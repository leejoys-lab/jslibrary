# JS 라이브러리 1 : Text Rolling

### 한 방향으로 흘러가는 텍스트 배너를 구현합니다.
아래와 같은 두 가지 방법을 찾았고, 2번(CSS)방법을 적용함

👀 나의 Demo 결과 미리보기

<img src ="textRoll.gif" height="50">


1. javascript 활용방법 [바로가기](https://elvanov.com/1592)
2. CSS만 사용하는 방법 [바로가기](https://velog.io/@favorcho/%ED%9D%90%EB%A5%B4%EB%8A%94-%ED%85%8D%EC%8A%A4%ED%8A%B8-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)

#### 🧐 2번을 선택한 이유?

- CJFOODVIILE 이라는 글자를 화면을 꽉 채우는 크기로 설정했기 때문에 같은 text를 여러번 반복하지 않아도 되는 상황이라서 CSS 애니메이션만으로도 충분히 구현할 수 있다고 생각함

#### 🤷‍♀️ 원본코드와 달라진점
1. 원본코드의 keyframes 안에 translate3d 를 translateX로 변경하여 작성
> 변경한 이유 : translate3d 가 뭔지 모름

```
  @keyframes textLoop {
    0% {
      -webkit-transform: translate3d(0, 0, 0);
      transform: translate3d(0, 0, 0);
    }
    100% {
      -webkit-transform: translate3d(-100%, 0, 0);
      transform: translate3d(-100%, 0, 0);
    }
  }
```

2. text:hover 효과 삭제
> 변경한 이유 : 기존 프로젝트에서 hover시 text를 정지시키는 것이 시각적으로 더 방해가 됨
```
  .flow-text:hover .flow-wrap {
    animation-play-state: paused;
    cursor: pointer;
  }
```

#### ✏ 개선할 점

( 1 )  translate3d 를 사용하면 하드웨어 과속(GPU)을 이용하므로 좀 더 나은 퍼포먼스를 보여준다.

translateX 만 필요할지라도 성능 향상을 위해 translate3d를 사용하기도 한다.

> 위의 내용을 참고하여 translte3d에 대한 학습 필요

( 2 ) 텍스트 길이, 화면의 너비에 따라서 div.flow-wrap의 갯수를 조절해 줘야하는것이

유지보수 측면상 좋지 않아 보인다.
> 위의 내용을 참고하여 다른 코드로 수정 시도해보기

---
# JS 라이브러리 2 : toggle Button(언어)
### 언어(Language)에 hover시 KOR, ENG가 말풍선 모양으로 떠오릅니다.
### tailwind CSS를 사용하여 디자인했습니다.

적용계획 : CJ푸드빌 리디자인 프로젝트 - 언어설정

👀 나의 Demo 결과물 미리보기

<img src ="toggleBtn2.gif" height="100">


* 원본코드 [바로가기](https://codepen.io/stefan-galescu/pen/vYNXWMP)

#### 🤷‍♀️ 원본코드와 달라진점

원본코드는 vue.js를 활용하여 작성되었으나, 아직 학습 전이기 때문에
같은 효과를 javascript로 구현하고자 함


#### 🧐 느낀점

- classList를 활용해서 자바스크립트 코드를 작성했는데, tailwind CSS때문에 나열된 클래스명들 때문에 보기에 너무 헷갈렸다..
- vue.js는 무엇일까. 약 30줄 정도로 작성한 javascript코드를 아래와 같이 정리해버린다니...
```
var app = new Vue({
el: "#app",
data: {
    isVisible: false,
},
});
```

#### ✏ 내가 작성한 javascript
더 나은 방법이 있을지 좀 더 고민해봐야겠다.
```
<script>
    let isVisible = false;
    let toggleBtn = document.getElementById("toggleBtn");
    let myTransition = document.getElementById("dropdown");

    function showDropdown(isShow) {
    if (isShow) {
        myTransition.classList.remove("scale-95", "opacity-0", "translate-y-2", "pointer-events-none");
    } else {
        myTransition.classList.add("scale-95", "opacity-0", "translate-y-2", "pointer-events-none");
    }
    }

    function toggleVisibility(show) {
    isVisible = show;
    if (isVisible) {
        showDropdown(true);
        document.addEventListener("click", onDocClick);
    } else {
        showDropdown(false);
        document.removeEventListener("click", onDocClick);
    }
    }

    function onDocClick(event) {
    if (!myTransition.contains(event.target)) {
        toggleVisibility(false);
    }
    }

    toggleBtn.addEventListener("click", function () {
    toggleVisibility(!isVisible);
    });

    toggleBtn.addEventListener("mouseover", function () {
    toggleVisibility(true);
    });

    myTransition.addEventListener("mouseleave", function () {
    toggleVisibility(false);
    });

    document.addEventListener("keydown", function (event) {
    if (event.key === "Enter") {
        toggleVisibility(!isVisible);
    }
    });
</script>
```

---
# JS 라이브러리 3
### 특정 단어만 색상을 적용시켜주는 자바스크립트 라이브러리 입니다.

- 예제 웹페이지 : https://wooyeongcho.github.io/Soursage.js/docs/index.html
- 적용할 웹페이지 : http://leejoys.dothome.co.kr/port/pf/gs/
- github Fork : https://github.com/leejoys-lab/Soursage.js.git

#### 적용계획 : GS건설 홈페이지에서 반복되는 "GS" 글자에 적용해볼 예정입니다.

<details>
<summary>🧐 미리보기 </summary>
<div markdown="1">

![image](https://user-images.githubusercontent.com/127175220/227722953-6bd9f646-d03d-46e0-9178-07c79bc7f965.png)
</div>
</details>

---

# JS 라이브러리 4
### 이미지가 흘러가는 배너를 만드는 자바스크립트 라이브러리 입니다.
#### 기능 1 : 한쪽 방향으로 이미지 흘러가도록 하기(연속재생)
#### 기능 2 : 배너에 마우스를 올렸을 때 정지하도록 하기

- 예제 웹페이지 : http://www.happycgi.com/Attach/screen_shot/2007/12/07/1197006821/index.html
- 적용할 웹페이지 : http://leejoys.dothome.co.kr/port/pf/cj_m/


#### 적용계획 : CJ푸드빌 모바일버전에서 왼쪽으로 흘러가는 이미지 배너에 적용해볼 예정입니다.

<details>
<summary>🧐 미리보기 </summary>
<div markdown="1">

![image](https://user-images.githubusercontent.com/127175220/227725394-654d3111-3f1f-4f32-be0c-61b352d26b21.png)

</div>
</details>
