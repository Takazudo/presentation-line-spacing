# Killing line spacing

[@Takazudo](https://twitter.com/Takazudo)

----

## What I mean...

```html
<div class="debugBar">デバッグ用バー</div>
<p>彼は背後にひそかな...</p>
<div class="debugBar">デバッグ用バー</div>
```

---

![](imgs/0.png)

---

### Top

<img src="imgs/1.png" alt="" width="700">

---

### Bottom

<img src="imgs/2.png" alt="" width="700">

----

## Why

```html
<div class="box">
  <p>彼は背後にひそかな...</p>
</div>
```

```css
.box {
  padding: 20px;
  border: 4px solid #000;
}
```

---

`padding: 20px`

![](imgs/3.png)

---

Here's the padding

![](imgs/4.png)

---

Then we have more

![](imgs/5.png)

---

We'll have 20px+ spacing on top and bottom.

![](imgs/3.png)

----

## Understanding<br>font-size / line-height

---

`font-size: 14px; line-height: 1.9;`

<img src="imgs/6.png" alt="" width="600">

---

`font-size: 14px`

<img src="imgs/7.png" alt="" width="600">

---

Leading

<img src="imgs/8.png" alt="" width="600">

---

Here's one line's height on browser.  
14px * 1.9 = 26.6px

<img src="imgs/9.png" alt="" width="600">

----

## How to kill it

---

one line's height: 14px * 1.9 = 26.6px  
leading's height: 26.6px - 14px = 12.6px  
half-leading: 12.6 / 2 = 6.3px

<img src="imgs/10.png" alt="" width="500">

---

Finally, we'll get `6.3px` height here.

<img src="imgs/11.png" alt="" width="600">

---

Slide it to upper

<img src="imgs/12.png" alt="" width="600">

---

```css
p:before,
p:after {
  content: '';
  display: block;
  height: 0;
  margin: -6.3px 0 0;
}
```
---

<img src="imgs/13.png" alt="">

---

### Top

<img src="imgs/14.png" alt="" width="700">

---

### Bottom

<img src="imgs/15.png" alt="" width="700">

----

## Think more simply

---

one line's height: 1em * 1.9 = 1.9em  
leading's height: 1.9em - 1em = 0.9em  
half-leading: 0.9em / 2 = 0.45em

<img src="imgs/10.png" alt="" width="500">

---

```css
p:before,
p:after {
  content: '';
  display: block;
  height: 0;
  margin: -0.45em 0 0;
}
```

---

### Top

<img src="imgs/14.png" alt="">

---

### Bottom

<img src="imgs/15.png" alt="">

----

## + a little tweak

---

```css
p:before,
p:after {
  content: '';
  display: block;
  height: 0;
}
p:before { margin: -0.35em 0 0; }
p:after { margin: -0.55em 0 0; }
```

---

<img src="imgs/16.png" alt="">

---

<img src="imgs/17.png" alt="">
---

```scss
@mixin lineSpacingKiller {
  &:before, &:after {
    content: '';
    display: block;
    height: 0;
  }
  &:before { margin: -0.35em 0 0; }
  &:after { margin: -0.55em 0 0; }
}
```

```scss
p {
  @include lineSpacingKiller;
}
```

----

## Conslusion

* More detailed spacing tweak is possible
* Beautiful margin is awesome
* CSS will be more complicated
* Make sure that this technique<br>has some difference between browsers<br>(it may be ±1px)

