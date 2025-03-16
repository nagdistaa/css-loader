# Loading Spinner Animation

This project creates an elegant loading animation with rotating dots that appear and disappear in sequence, creating a circular loading effect.

## Overview

The animation consists of a circular arrangement of dots that fade in and out around a central "loading" text. The dots are illuminated in a cyan color with a glow effect, creating a visually appealing loading indicator against a dark background.

## HTML Structure

The HTML structure is simple and consists of:

```html
<section>
    <div class="loader">
        <p>loading</p>
        <span style="--i:1"></span>
        <span style="--i:2"></span>
        <!-- ... spans continue through --i:20 -->
    </div>
</section>
```

- A `section` element serves as the container for the entire animation
- Inside it, a `div` with class `loader` contains:
  - A paragraph element showing the text "loading"
  - 20 `span` elements that will become the animated dots
  - Each span has a custom property `--i` with values from 1 to 20 to control their positioning and animation timing

## CSS Styling

### Reset and Basic Setup

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

section {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: #001f25;
}
```

This creates a full-viewport dark teal background and centers the animation.

### Loader Container

```css
.loader {
    position: relative;
    width: 200px;
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.loader p {
    color: #00efff;
    font-size: 1.8em;
    text-shadow: 0 0 20px #00efff, 0 0 40px #00efff;
}
```

- The loader container is a 200px × 200px square
- The "loading" text is positioned in the center using flex
- The text is styled with a cyan color (#00efff) and has a text shadow for a glowing effect

### Animated Dots

```css
.loader span {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transform: rotate(calc(18deg * var(--i)));
}

.loader span::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: #00efff;
    box-shadow: 0 0 20px #00efff, 0 0 40px #00efff, 0 0 80px #00efff, 0 0 160px #00efff;
    animation: animate 1s linear infinite;
    animation-delay: calc(-0.1s * var(--i));
}
```

- Each span is positioned absolutely and rotated based on its `--i` value
- The rotation angle is calculated as `18deg * var(--i)` (360° divided by 20 spans = 18° per span)
- Each span has a pseudo-element `::before` that creates a circular dot
- The dots are styled as 30px × 30px cyan circles with multiple layers of box shadow for the glow effect
- Each dot is animated using the `animate` keyframes with a staggered delay based on its position

### Animation

```css
@keyframes animate {
    0% {
        transform: scale(1);
    }
    80%, 100% {
        transform: scale(0);
    }
}
```

- The animation scales each dot from its full size to zero
- The dot stays at full size from 0% to 80% of the animation duration
- It quickly shrinks to nothing between 80% and 100% of the animation
- Combined with the staggered delays, this creates a circular wave effect

## How It Works

1. The 20 span elements are positioned in a circle around the central "loading" text
2. Each span has a dot created using a pseudo-element
3. Each dot is rotated to its position using the CSS custom property `--i`
4. The dots are animated to scale down to zero size
5. The animation delays are staggered based on position, creating a wave-like effect

## Customization

You can easily modify this loading animation by:

- Changing the color by replacing all instances of `#00efff`
- Adjusting the size by modifying the `width` and `height` of the `.loader`
- Changing the number of dots by adding or removing `span` elements and adjusting the rotation calculation
- Modifying the animation speed by changing the duration in the `animation` property