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
