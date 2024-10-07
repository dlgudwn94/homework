# 2차 과제 Avatars 코드 설명

## html 구성

```
<body>
    <main class="main">
	</main>
</body>
```

콘텐츠 위치 정렬을 편하게 하기 위해 body 안에 main 클래스로 큰 틀을 구성함

---

```
<section class="top">
</section>
<section class="bottom">
</section>
```

flex를 지원하는 환경에서 위아래 역으로 출력이 되야하기 때문에 이를 편하게 하기 위해 section 태그로 top과 bottom을 구성함

---

```
<div class="profile">
  <img src="../assets/avatars/face1.jpg" alt="프로필 사진1" />
  <div class="status_offline" aria-label="오프라인"></div>
</div>
<div class="profile">
  <img src="../assets/avatars/face2.jpg" alt="프로필 사진2" />
  <div class="status_online" aria-label="온라인"></div>
</div>
```

div 태그로 이미지와 상태 정보를 묶고 특정 이미지만 변경하기 용이하도록 profile이라는 클래스와 status_online, status_offline 이라는 클래스를 부여함.  
사용자 접근성을 위해서 aria-label로 온라인, 오프라인이라는 대체 텍스트를 제공함

## CSS 구성

```
.main {
  position: absolute;
  display: block;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

콘텐츠를 화면 중앙에 배치하기 위해 main 섹션이 화면 중앙에 올 수 있도록 함

---

```
.profile {
  position: relative;
  float: left;
}
```

이미지 우측에 다음 이미지가 배치될 수 있도록 float: left 속성을 부여함

---

```
.profile img {
  width: 64px;
  height: 64px;
  margin-right: 20px;
  border-radius: 70%;
  object-fit: cover;
}
```

profile 클래스에 속한 img 파일은 가로, 세로를 64px로 고정하고, 여백을 20px로 고정함  
object-fit: cover와 border-radius 속성을 70%로 줌으로써 비율을 유지한 상태로 프로필 사진을 원형으로 변경함

---

```
.profile .status_online {
  position: absolute;
  background-color: #4cfe88;
  bottom: 8%;
  right: 20%;
  width: 16px;
  height: 16px;
  border-radius: 10px;
}

.profile .status_offline {
  position: absolute;
  background-color: #dbdbdb;
  bottom: 8%;
  right: 20%;
  width: 16px;
  height: 16px;
  border-radius: 10px;
}
```

상태 정보를 표시하는 우측 하단의 원을 표시하기 위해 absolute로 고정된 위치를 부여하고  
bottom, right 속성으로 위치를 조정하며 width, height 속성으로 크기를 조절 및 border-radius 속성으로 원형으로 변경함

---

```

@supports (display: flex) {
  .main {
    display: flex;
    flex-direction: column-reverse;
  }
}
```

과제 내용 중 flex를 지원하는 환경에서는 위아래 열이 바뀌어 표시되어야 한다는 조건이 있어서  
@supports로 flex를 지원하는 브라우저에서는 column을 역순으로 변경되도록 함

<!-- - 피드백
    - `avatars.md` 파일에 과제를 구현해 나가는 과정에 대한 설명이 인상적임.
    다만 코드 가독성을 높이기 위해 컬러링을 신경썼다면 더 좋을 것 같고 또한 해당 과제를 통해 어떤 점을 배웠는지에 대한 회고가 있다면 더 좋을 것 같음.
    - <section> 요소 내 <div>, <img>, <span> 요소를 사용하여 마크업 하였는데 만약 아바타 이미지를 하나의 `component(컴포넌트 - 부품)`로 접근한다면 해당 요소가 적절할지 고민해 보기 바람.
    [Component Driven Development](https://www.componentdriven.org/)
    - `<section> 요소`를 사용했다면 이를 고려하여 `적절한 제목`을 제공하는 것이 필요함.
    - `“프로필 사진 1”`이라는 대체 텍스트가 적절한가에 대해 고민해보기 바람.
    만약 해당 대체 텍스트가 실제 사용자의 아바타로 사용될 경우 사용자의 이름이나 닉네임 등으로 수정될 가정을 하였다면 좋겠지만 디자인만을 생각하고 순서를 매기는 형태로 접근한 것이라면 이 역시 해당 서비스를 사용하는 사용자에 대한 고민이 부족한 것으로 보여짐.
    - `jpg` 형식의 이미지를 제공하는 것이 `성능` 관점에서 최선이었을지 고민해보기 바람.
    - <div> 요소에 aria-label 속성으로 상태 정보를 제공하고 있으나 해당 정보는 `숨김 콘텐츠 기법`을 사용하는 방향을 추천하고 싶음.
    aria-label 속성은 문법상 모든 요소에 사용할 수 있지만  DOM에 레이블로 사용할 눈에 보이는 텍스트가 없는 경우, 특히 `대화형 요소` 또는 다른 ARIA 선언을 통해 대화형으로 만들어진 요소를 위해 의도된 속성임.
    [MDN aria-label](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-label)
    - `<img> 요소`에 `width`와 `height` 속성을 추가한다면 렌더링 성능 관점에서 이점이 있음.
    - `float`을 적용하기 위한 마크업과 `flex`를 적용하기 위한 마크업을 `따로 구현`한 부분은 아쉬움.
    - `float` 과제임에도 float을 사용하지 않은 점이 아쉬움.
    - `@support` 규칙을 사용하여 flex가 지원되는 환경에서는 flex로 배치되도록 미션을 잘 수행 하였음.
    - 과제 저장소를 배포하지 않아 실제 파일의 `렌더링 결과를 확인할 수 없었던 점`이 아쉬움. -->
