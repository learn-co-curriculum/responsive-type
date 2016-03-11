# Responsive Type

## Overview

In this lesson we will look at strategies for making adjustments to type in repsonsive layouts.

## Objectives

1. Adjust text sizing to be responsive while maintaining its size relationship to other bodies of text.

## Creating Responsive Type That's Easy To Maintain

<iframe width="640" height="480" src="//www.youtube.com/embed/I3SB9RNg74w?rel=0" frameborder="0" allowfullscreen></iframe>

*Note: Slides for this lecture video are provided in the resources at the bottom of this lesson.*

### Em, What Else Would I Use?

Using ems to size your typography site wide has one large advantage over pixels or percents. That is that this size measurement (em) is a relative measurement. Let's take a look at an example where we want our header text to always be two and half times larger than our paragraph text. On certain devices when the screen gets below 400px we want all of our text to become 30% larger whilst still maintaining the relationship of the heading being 2.5 times larger than our paragraph.

```css
body { font-size: 100%; }
h1 { font-size: 2.5em; }
p { font-size: 1em; }

@media only screen and (max-width: 400px) {
  body { font-size: 130%; }  
} 
``` 

...

## Summary

- ...

## Resources

- [Presentation Slides](https://docs.google.com/presentation/d/1j_i5pGPB5lHbgr4fpdUDheRBv2kAeOk_yhfd1Uc2f3s/edit?usp=sharing)
- [Responsive Type - Code Example](http://jsfiddle.net/flatiron_school/H6cN5/)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/responsive-type' title='Responsive Type'>Responsive Type</a> on Learn.co and start learning to code for free.</p>