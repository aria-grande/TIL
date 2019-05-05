# Multiple Background image
```css
#example1 {
  background-image: url(img_flwr.gif), url(paper.gif);
  background-position: right bottom, left top;
  background-repeat: no-repeat, repeat;
}
```
background-image에 먼저 선언될 수록 위 layer에 쌓인다.

Ref: https://www.w3schools.com/CSS/css3_backgrounds.asp

# Progress Bar
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

Ref: https://www.w3schools.com/w3css/w3css_progressbar.asp
