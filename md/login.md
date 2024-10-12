# 3차 과제 Login 코드 설명

## [Login](https://dlgudwn94.github.io/homework/login/login.html)

## HTML 구조 설명

```
<section class="login-page">
</section>
```

login-page라는 하나의 섹션으로 구성함

---

```
<figure class="naver-logo">
~
  </svg>
  <figcaption class="sr-only">네이버 로고 이미지</figcaption>
</figure>

```

로고 이미지를 figure 태그 안에 svg 요소로 마크업하고, figcaption을 숨김처리 하기 위해 sr-only 클래스를 부여함

---

```
<form action="" method="post" class="login-form">
  <label for="user-id"></label>
  <input placeholder="아이디(이메일)" type="email" name="user-id" id="user-id" required />
  <span class="err-user-id">아이디는 이메일 형식으로 입력해 주세요.</span>
  <label for="user-pwd"></label>
  <input placeholder="비밀번호" type="password" name="user-pwd" id="user-pwd" minlength="10" />
  <span class="err-user-pwd">비밀번호는 10자리 이상 입력해 주세요.</span>
  <button type="submit">로그인</button>
</form>
```

아이디와 비밀번호 등 input, button 요소를 제공하기 위해 form 태그를 사용하여 아이디, 비밀번호, 로그인 버튼을 배치함  
보안을 위해 form의 method는 post로 설정함  
타입을 각각 지정하고 아이디와 비밀번호 input 태그에 required를 넣어 필수 입력 서식으로 구현함  
유효하지 않은 값을 입력할 시 나타나게 할 안내 문구는 span 태그를 사용하여 각각 class를 부여함

---

```
<input type="checkbox" id="check-stay-login" />
<label for="check-stay-login" tabindex="0">
  <span>로그인 상태유지</span>
</label>
```

기존의 체크박스 대신 다른 체크박스 이미지를 사용하기 위해 label의 for과 체크박스의 id를 동일하게 맞춤  
마우스 외에 키보드로도 선택할 수 있도록 tabindex 값으로 0을 부여함

---

```

<div class="ip-security">
  <a href="./pages/ip_security.html" target="_blank" title="IP 보안 설명 사이트로 이동합니다.">IP 보안 <strong>OFF</strong></a>
</div>
```

IP 보안 텍스트를 클릭 시 ip_security.html 파일이 새창에 열릴 수 있도록 anchor 태그를 사용하여 target을 \_blank로 부여함. 또한 웹 접근성을 위해 title을 사용하여 마우스 오버 시 설명이 나올 수 있도록 함

---

## CSS 구조 설명

```
@import "./../../../html-css/src/common/best-reset.css";
@import "./../../../html-css/src/common/a11y.css";
```

best reset을 활용하여 리셋하였고 숨김처리를 위한 a11y.css를 import 함

---

```
:root {
  --default-font-size: 16px;
  --default-font-color: #121212;
  --default-color: #fff;
  --green-color: #03cf5d;
  --focus-color: #e9f0fd;
  --focus-custom-color: #24388d;
}
```

자주 사용할 수 있는 폰트 사이즈와 폰트 컬러를 관리가 용이하도록 변수로 지정함

---

```
.login-page {
  width: 100%;
  inline-size: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding-inline: 1.25rem;
  padding-left: 1.25rem;
  padding-right: 1.25rem;
  font-size: var(--default-font-size);
  color: var(--default-font-color);
  margin: 0 auto;

  @media (min-width: 768px) {
    width: 500px;
    inline-size: 500px;
  }
```

중앙 정렬을 시켜주었고, 모바일 스타일을 먼저 구현하기 위해 width를 100%로 설정함  
반응형 웹 디자인을 위해 여백은 rem을 사용하여 설정함  
미디어 쿼리를 사용하여 768픽셀 이상일 때 width를 500px로 설정하여 데스크탑 스타일을 정의함

---

```
.naver-logo {
  width: 230px;
  inline-size: 230px;
  margin-top: 5rem;
  margin-bottom: 5rem;
  margin-block: 5rem;
}
```

로고의 크기와 위치를 설정함

---

```
.login-form{
	width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;

  input[id="user-id"],
  input[id="user-pwd"] {
    width: 100%;
    inline-size: 100%;
    font-size: 0.875rem;
    height: 2.8125rem;
    block-size: 2.8125rem;
    padding-left: 1.25rem;
    padding-right: 1.25rem;
    padding-inline: 1.25rem;
    margin-top: 1rem;
    border: #dadada solid 1px;
    background-color: var(--default-color);
    &:focus {
      border: var(--green-color) solid 1px;
      background-color: var(--focus-color);
      outline: none;
    }
	}
}
```

입력 서식을 중앙정렬 시켜준 후 user-id와 user-pwd라는 아이디를 가진 input 요소에 대해 과제에서 요구한 크기 및 여백을 rem 단위로 설정함  
&을 사용해 부모 요소가 포커스 됐을 때 배경과 테두리 선을 설정함

---

```
.err-user-id,
.err-user-pwd {
  width: 100%;
  display: none;
  color: red;
  font-size: 0.625rem;
  padding-inline-start: 0.625rem;
  margin-top: 0.3125rem;
}
input[type="email"]:user-invalid + .err-user-id {
  display: inline;
}
input[type="password"]:user-invalid + .err-user-pwd {
  display: inline;
}
```

err-user-id, err-user-pwd 클래스를 선택하여 글자 색상 및 크기, 여백 등을 설정함  
display:none으로 평소에 보이지 않도록 설정한 후 해당 요소들이 유효하지 않을 때 인접한 err-user-OO 클래스를 display:inline으로 보이도록 설정함

---

```
button[type="submit"] {
  width: 100%;
  height: 2.8125rem;
  block-size: 2.8125rem;
  color: var(--default-color);
  background-color: var(--green-color);
  border: none;
  margin-top: 1.25rem;
  margin-block-start: 1.25rem;
  &:focus {
    outline-color: var(--focus-custom-color);
  }
}
```

로그인 버튼을 디자인하고 버튼이 포커스 됐을 때 아웃라인 색상이 변경되도록 함

---

```
.ip-security {
  display: none;
  font-size: var(--default-font-size);
  color: var(--default-font-color);
  @media (min-width: 768px) {
    display: inline-block;
  }
}
```

diplay를 none으로 설정하여 보이지 않게 처리하였고, 미디어쿼리를 사용해 768픽셀 이상(데스크탑 스타일)인 경우에만 보일 수 있도록 설정함

---

```
.stay-login {
  width: 100%;
  display: flex;
  margin-top: 0.625rem;
  justify-content: end;
  @media (min-width: 768px) {
    justify-content: space-between;
  }
}
```

로그인 상태유지와 IP 보안 앵커가 속한 stay-login 클래스를 justify-content: end으로 우측정렬 되도록 함  
이때 기본이 모바일 스타일이기 때문에 위에서 로그인 상태유지와 체크박스가 우측정렬 되며, 미디어 쿼리를 사용하여 데스크탑 스타일일 때 space-between으로 양쪽 정렬되도록 설정함

---

```
input[type="checkbox"] {
      display: none;
    }

    input[type="checkbox"] + label {
      text-align: center;
      cursor: pointer;
      margin-right: 0.3125rem;
      margin-inline-end: 0.3125rem;
    }

    input[type="checkbox"] + label::before {
      content: "";
      display: inline-block;
      background: url(../../assets/login/unchecked.svg) no-repeat;
      width: 1.5rem;
      height: 1.5rem;

      &:foucs {
        outline-color: var(--focus-custom-color);
      }
    }

    input[type="checkbox"]:checked + label::before {
      background: url(../../assets/login/checked.svg) no-repeat;
      &:focus {
        outline-color: var(--focus-custom-color);
      }
    }
```

기존의 체크박스를 안 보이도록 설정함  
마우스 오버 시 커서를 포인터 모양으로 변경함  
checkbox 타입의 input 요소와 인접한 label의 가상 요소 선택자를 이용하여 기존 체크박스 위치에 다른 체크 박스 모양이 나타나도록 함  
해당 체크박스가 체크 됐을 때 또 다른 체크박스 이미지가 나타날 수 있도록 함  
포커스 됐을 때 outline-color가 바뀔 수 있도록 설정함

---

### 회고

구글링을 하면서 어떻게 과제를 끝내긴 했지만 배치나 체크박스 관련해서 부족한 점을 많이 느꼈습니다.  
과제를 하면서 배치나 선택자, 특히 체크박스에 대해 공부가 많이 됐습니다.  
앞으로 요소의 배치에 관련하여 공부가 더 필요할 것 같습니다.
