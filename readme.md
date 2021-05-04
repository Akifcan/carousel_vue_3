# carousel_vue_3

## Add carousel for your vue.js 3 applications

### Example

![example](https://i.imgur.com/Lbi4t1o.gif)

```
import Carousel from './components/Vue3-Carousel'
createApp(App).use(Carousel)......
```

```
 <Carousel>
      <div id="carousel-1" class="carousel-item custom-slide">😎</div>
      <div id="carousel-2" class="carousel-item custom-slide">😪</div>
      <div id="carousel-3" class="carousel-item custom-slide">😣</div>
</Carousel>

.custom-slide {
  font-family: sans-serif;
  color: white;
  display: grid;
  place-items: center;
  font-size: 3rem;
}
.custom-slide:nth-child(1) {
  background: blue;
}
.custom-slide:nth-child(2) {
  background: orange;
}
.custom-slide:nth-child(3) {
  background: pink;
}

```

- carousel-item class is required. For custom styling you can add another classes. Class names are up to you doesn't have
  to be `custom-slide`.

### Features

- draggable
- box-shadow
- border-radius
- button-color

```
<Carousel
    :shadow="'0 0 50px rgba(0, 0, 0, 0.5);'"
    :containerRadius="'1rem'"
    :buttonColor="'#002553'"
>
```
