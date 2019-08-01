# [Multiple Background image](https://www.w3schools.com/CSS/css3_backgrounds.asp)
```css
#example1 {
  background-image: url(img_flwr.gif), url(paper.gif);
  background-position: right bottom, left top;
  background-repeat: no-repeat, repeat;
}
```
background-image에 먼저 선언될 수록 위 layer에 쌓인다.

# [Background image relative position](https://css-tricks.com/positioning-offset-background-images/)
20px apart from right and 10px apart from bottom
```css
background-position: right 20px bottom 10px;
```

# [Progress Bar](https://www.w3schools.com/w3css/w3css_progressbar.asp)
```html
<progress min="0" max="100" value="60" />
```

```css
progress::-webkit-progress-value {
  background: red;
}

progress::-webkit-progress-bar {
  background: blue;
}
```

# [Box-sizing](https://developer.mozilla.org/ko/docs/Web/CSS/box-sizing)
요소의 너비와 높이를 계산하는 방법을 지정한다.

- `box-sizing: content-box` : 콘텐츠 영역이 parent container와 같아지고, 테두리와 안쪽 여백은 이에 더해진다
- `box-sizing: border-box` : 테두리와 안쪽 여백의 크기의 합도 요소의 크기로 고려한다.

# Vertical align of a div
```css
margin: auto;
```
