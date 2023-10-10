# Working with Responsive Type

## Learning Goals

- Create maintainable responsive type with `em`.
- Create maintainable responsive type with column count.

## Introduction

CSS media queries are great for reshaping websites for any device, making them
"responsive". There is still some work to do though, particularly in regard to
content.

In addition to media such as images, the _text_ content also becomes a concern
for readability. Depending on the screen size of a user's device, text can take
up different amounts of space. On a site with static sized text, a user with a
huge desktop monitor may see a website with large blank spaces and text
sprawling in long lines across the screen, while a mobile user might be
scrolling down through seemingly endless text. On a small screen, text can
appear large, however, on screens with higher resolution, text with fixed size
could become too difficult to read, and on a smaller device it would take up way
too much screen real estate. What are some workarounds for these styling
challenges?

## Create Maintainable Responsive Type with `em`

One of the best ways to create maintainable type is with relative measurements
such as _em_. Em values are relative to the current font-size. Because it is a
relative measurement, it is very useful for keeping type proportional. Let's
take a look at an example where we want our header text to always be two and a
half times larger than our paragraph text. On certain devices, when the screen
gets below `400px` we want all of our text to become 30% larger while still
maintaining the relationship of the heading being 2.5 times larger than our
paragraph.

```css
body {
  font-size: 100%;
}
h1 {
  font-size: 2.5em;
}
p {
  font-size: 1em;
}

@media only screen and (max-width: 400px) {
  body {
    font-size: 130%;
  }
}
```

In the code above, on line 1, 2, and 3 we are setting default styles. The body
element's default text size is already 100%, but we have included it here to
clarify the change that's made in the media query. On line 2 we set all `h1`
elements to be `2.5em`, and on line 3 we set the `p` element to `1em`. So, the
`h1` is two and a half times larger than our paragraphs. In our media query on
line 5 we set the query to trigger for device screens less than 400 pixels. When
this occurs on line 6 we adjust the body font-size to 130%. This causes all
elements within the body (`h1`, `p`) to inherit this change and grow 30% larger.

Since we sized using `em`, the `h1` and `p` adjust in proportion to each other
even as they grow or shrink in size. This makes it very convenient to make size
adjustments to one element, the body and thus affect all other type in our
layout uniformly.

Em values can be used in width and height properties, so this measurement can be
used for the `div`s and elements making up your webpage structure, and would
also adjust in proportion based on font-size, like in the example above.

## Create Maintainable Responsive Type with Column Count

Another tip for adjusting type is when you might want to wrap text into separate
columns. This is especially true on larger screen sizes where you have big
bodies of text content. You can imagine that as a paragraph stretches across
bigger screens, the lines of text get really long, and become awkward for the
reader to find the next line. Designers suggest that for optimum readability you
want the measure of your text lines to be between 40 to 80 characters. Anything
smaller or larger becomes a bit awkward to read. To tackle this we can make use
of a lesser known, yet fairly well supported CSS `column-count` property.

The default column-count is one, meaning text is contained within one column.
When our screen gets bigger, it might be good to adjust the text into multiple
columns; let's see an example:

```html
<article>
  <p>
    Nor again is there anyone who loves or pursues or desires to obtain pain of
    itself, because it is pain, but occasionally circumstances occur in which
    toil and pain can procure him some great pleasure. To take a trivial
    example, which of us ever undertakes laborious physical exercise, except to
    obtain some advantage from it? But who has any right to find fault with a
    man who chooses to enjoy a pleasure that has no annoying consequences, or
    one who avoids a pain that produces no resultant pleasure?
  </p>
</article>
```

```css
article p {
  column-count: 1; /* This is the default so we don't really need to specify */
}

@media only screen and (min-width: 480px) {
  article p {
    column-count: 2;
  }
}
```

As we mentioned, paragraphs by default normally only occupy one column. However,
we can create the visual effect of this single paragraph element splitting into
multiple columns by setting our media query on line 5 to trigger on screens
greater than `480px`; then on line 7 we set our paragraph to adjust its column
count to 2 columns instead. Have a look at this in the code example in the
resource section below at the bottom of this lesson.

## Create Fluid Typography Headers with CSS Clamp

The `vw` unit scales with the viewport of the screen. Each `vw` unit is 1% of
the viewport width. If the user has a 1000px-wide window, a `5vw` value would
translate to `50px`. We can use it like this to scale the text:

```html
<style>
  h1 {
    font-size: 6vw;
    margin-bottom: 0.5em;
  }
</style>

<main>
  <h1>I am a fluid headline!</h1>
  <p>The heading will grow and shrink with the viewport.</p>
</main>
```

But you'll notice that the text can become too big or small at certain
viewports. This is why we need to use the `clamp` function ([Clamp MDN
Doc][clamp-mdn]) to limit how big or small the text can get.

```html
<style>
  h1 {
    font-size: clamp(1.5rem, 6vw, 3rem);
    margin-bottom: 0.5em;
  }
</style>

<main>
  <h1>I am a fluid headline!</h1>
  <p>The heading will grow and shrink with the viewport.</p>
</main>
```

There's another problem we need to address with the code. If the user increases
their default font size, the text doesn't scale properly. This is an
accessibility violation. We need to mix in a `rem` unit to fix the issue:

```html
<style>
  h1 {
    font-size: clamp(1.5rem, 5vw + 1rem, 3rem);
    margin-bottom: 0.5em;
  }
</style>

<main>
  <h1>I am a fluid headline!</h1>
  <p>The heading will grow and shrink with the viewport.</p>
</main>
```

This technique should be used for headers or other large texts since viewport
units produce very small text on mobile devices.

You can read more about fluid typography [in this
article][modern-fluid-typography] and find the right scale for your app by using
[this fluid typography editor][fluid-type-editor].

## Conclusion

Creating responsive layouts can be tricky, but with a number of techniques in
mind, this process becomes more manageable. It is to our advantage to set all
typography within our site to ems and then in media queries adjust the body
font-size as a percent to adjust all type in proportion to each other. This
simplifies our media queries on typography. In addition to `em`, with the
`column-count` property, you can adjust it to split text into virtual columns.

## Resources

- [Responsive Type Column Count - Code Example](http://jsfiddle.net/flatiron_school/vy43K/2/)
- [Fluid Typography - Code Example](https://jsfiddle.net/alveem/zvnbo71t/)
- [Modern Fluid Typography Using CSS Clamp][modern-fluid-typography]
- [Modern Fluid Typography Editor][fluid-type-editor]
- [Clamp MDN Doc][clamp-mdn]

[clamp-mdn]: https://developer.mozilla.org/en-US/docs/Web/CSS/clamp
[modern-fluid-typography]:
  https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/
[fluid-type-editor]: https://modern-fluid-typography.vercel.app/
