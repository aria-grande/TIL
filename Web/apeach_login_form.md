# 어피치 로그인 폼

![apeach_login](images/apeach_login.gif)

데뷰 2018에서 우연히 [LoginCritter](https://github.com/cgoldsby/LoginCritter)를 알게 되어, 어피치 버전으로 간단하게 만들어 보았습니다.
>  An animated avatar that responds to text field interactions.

## 목적
- [SVG(Scalable Vector Graphic)](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/svg)를 사용해보자!
- [CSS transform](https://www.w3schools.com/cssref/css3_pr_transform.asp)을 사용해보자!
- 어피치는 내가 제일 좋아하는 캐릭터!

## 코드
### HTML
```html
<div id="apeach-login-form">
  <form>
    <svg version="1.1" baseProfile="full" width="300" height="300" xmlns="http://www.w3.org/2000/svg">
      <g>
        <g>
          <g><!-- 얼굴 -->
            <path xmlns="http://www.w3.org/2000/svg" d="M101.47 29.58C116.76 20.18 125.58 12.14 127.95 11.35C131.87 10.05 136.12 10.05 140.69 11.35C159.78 23.21 175.38 33.96 187.49 43.63C189.38 45.14 191.19 46.62 192.91 48.07C205.64 58.85 213.71 68.17 217.12 76.02C234.76 102.15 241.29 124.36 236.71 142.65C233.37 156.03 226.83 168.89 217.1 181.22C210.67 189.36 202.43 195.9 193.04 200.31C186.69 203.3 178.78 205.72 169.32 207.57C157.13 209.97 133.22 208.25 119.14 210.26C110.33 211.52 101.8 211.08 93.54 210.26C71.77 208.1 51.89 198.96 33.89 182.82C18.21 164.53 12.33 144.28 16.25 122.07C20.17 99.87 36.83 77 66.22 53.49C79.75 43.68 91.5 35.71 101.47 29.58Z" id="face"/>
          </g>
          <g><!-- 왼쪽눈 -->
            <path xmlns="http://www.w3.org/2000/svg" d="M96.49 117.57C96.49 121.35 93.41 124.43 89.63 124.43C85.84 124.43 82.77 121.35 82.77 117.57C82.77 113.78 85.84 110.71 89.63 110.71C93.41 110.71 96.49 113.78 96.49 117.57Z" id="left-eye" class="eyes"/>
            <path xmlns="http://www.w3.org/2000/svg" fill="none" fill-opacity="1" stroke="#222222" stroke-opacity="1" stroke-width="5" stroke-dasharray="none" stroke-linejoin="round" stroke-linecap="butt" stroke-dashoffset="" fill-rule="nonzero" opacity="1" marker-start="" marker-mid="" marker-end="" d="M66.29729314369392,115.6216168323515L104.135130493897,116.9729681662873" id="left-closed-eye" class="closed_eyes hide"/>
          </g>
          <g><!-- 오른쪽눈 -->
            <path xmlns="http://www.w3.org/2000/svg" d="M165.37 117.57C165.37 121.35 162.3 124.43 158.51 124.43C154.72 124.43 151.65 121.35 151.65 117.57C151.65 113.78 154.72 110.71 158.51 110.71C162.3 110.71 165.37 113.78 165.37 117.57Z" id="right-eye" class="eyes right-eye"/>
            <path xmlns="http://www.w3.org/2000/svg" fill="none" fill-opacity="1" stroke="#222222" stroke-opacity="1" stroke-width="5" stroke-dasharray="none" stroke-linejoin="round" stroke-linecap="butt" stroke-dashoffset="" fill-rule="nonzero" opacity="1" marker-start="" marker-mid="" marker-end="" d="M147.78377767128183,116.70269822273235 L185.6216150214849,118.05404955666816 " class="closed_eyes hide" id="right-closed-eye"/>
          </g>
          <g><!-- 볼터치 -->
            <path xmlns="http://www.w3.org/2000/svg" d="M84.82 149.51C84.82 158.7 74.07 166.17 60.83 166.17C47.58 166.17 36.83 158.7 36.83 149.51C36.83 140.32 47.58 132.85 60.83 132.85C74.07 132.85 84.82 140.32 84.82 149.51Z" id="left-chin"/>
            <path xmlns="http://www.w3.org/2000/svg" d="M213.36 149.51C213.36 158.7 202.61 166.17 189.36 166.17C176.12 166.17 165.37 158.7 165.37 149.51C165.37 140.32 176.12 132.85 189.36 132.85C202.61 132.85 213.36 140.32 213.36 149.51Z" id="right-chin"/>
          </g>
          <g><!-- 입 -->
              <path xmlns="http://www.w3.org/2000/svg" d="M97.3 156.99C95.13 148.66 97.31 143.84 103.85 142.52L124.25 145.15C130.89 143.76 135.03 142.9 136.69 142.55C136.78 142.53 136.87 142.52 136.96 142.52C138.42 142.52 142.08 142.52 147.93 142.52C154.85 147.35 155.84 152.83 150.9 158.97C145.96 165.11 137.07 167.96 124.25 167.52C108.46 168.84 99.48 165.33 97.3 156.99Z" id="mouth"/>
          </g>
        </g>
      </g>
      <g>
        <g>
          <g>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#face" opacity="1" fill="#fecbcf" fill-opacity="1"/>
            <g>
              <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#face" opacity="1" fill-opacity="0" stroke="#fc9fa1" stroke-width="4" stroke-opacity="1"/>
            </g>
          </g>
          <g>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#left-eye" opacity="1" fill="#030301" fill-opacity="1"/>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#left-closed-eye" opacity="1" fill="#030301" fill-opacity="1"/>
          </g>
          <g>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#right-eye" opacity="1" fill="#030301" fill-opacity="1"/>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#right-closed-eye" opacity="1" fill="#030301" fill-opacity="1"/>
          </g>
          <g>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#left-chin" opacity="1" fill="#fa6270" fill-opacity="1"/>
          </g>
          <g>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#mouth" opacity="1" fill="#9b1f36" fill-opacity="1"/>
            <g>
              <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#mouth" opacity="1" fill-opacity="0" stroke="#69282f" stroke-width="4" stroke-opacity="1"/>
            </g>
          </g>
          <g>
            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#right-chin" opacity="1" fill="#fa6270" fill-opacity="1"/>
          </g>
        </g>
      </g>
    </svg>
    <div id="inputs">
      <input id="email" type="text" placeholder="email@domain.com"/>
      <input id="pw" type="password" placeholder="password" />
      <input type="submit" value="Sign In"/>
    </div>
  </form>
</div>
```

### CSS
```css
#inputs {
    width:250px;
    border-radius: 10px;
    position: fixed;
    top: 200px;
    background-color: #fecbcf;
    padding: 10px;
}
#inputs input {
    display: block;
    width: 80%;
    margin: 10px auto;
    font-size: 15px;
    border: 0;
    border-radius: 5px;
    outline: 0;
    padding: 10px 15px;
}
input[type="submit"]:hover {
    background-color: lightgray;
}
.hide {
    visibility: hidden;
    opacity: 0;

    transition: visibility 0s linear 0.1s, opacity 0.1s linear;
}
```

### JS
```js
function Eye(openId, closeId) {
  this.openElement = document.getElementById(openId);
  this.closeElement = document.getElementById(closeId);
  this.open = function() {
    this.openElement.classList.remove("hide");
    this.closeElement.classList.add("hide");
  };
  this.close = function() {
    this.openElement.classList.add("hide");
    this.closeElement.classList.remove("hide");
  };
  this.move = function(x, y, z) {
    this.openElement.style.transform = `translate3D(${x}px, ${y}px, ${z}px)`;
    this.openElement.style.transitionDuration = ".5s";
  }
}
var leftEye = new Eye("left-eye", "left-closed-eye");
var rightEye = new Eye("right-eye", "right-closed-eye");

const maxTextCount = 24;
var emailElement = document.getElementById("email");
emailElement.addEventListener("focus", function() {
  leftEye.move(-5, 2, 0);
  rightEye.move(-7, 2, 0);
})
emailElement.addEventListener("input", function() {
  var textCount = this.selectionEnd;
  if(textCount > maxTextCount) {
    textCount = maxTextCount;
  }
  var y = Math.pow((textCount - maxTextCount / 2), 2) / 30;
  leftEye.move(textCount / 2 - 2, -y, 0);
  rightEye.move(textCount / 3 - 2, -y, 0);
});


var passwordElement = document.getElementById("pw");
passwordElement.addEventListener("focus", function() {
  leftEye.close();
  rightEye.close();
});
passwordElement.addEventListener("focusout", function() {
  leftEye.open();
  rightEye.open();
});
```

## 느낀점
- 얼굴도 움직이고, 입도 옴싹달싹 하면 좋겠다!
- 그렇게 고퀄로 만들기엔 각도 계산도 필요하고, svg에 대한 마스터링이 필요하다.
- 나중에 하고 싶을 때 해보자!

- [Method Draw](https://editor.method.ac/)라는 web svg editor로 쉽게 svg 태그를 만들 수 있다!
- Curved animation에 대해 [이 아티클](http://tobiasahlin.com/blog/curved-path-animations-in-css/)을 읽어봐도 좋을 것 같다.
