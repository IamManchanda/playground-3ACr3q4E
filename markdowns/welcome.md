# Part 3 - Here comes ECSS, Long Live ECSS!

In the previous article, I covered about **CSSinJS** and **separation of concerns** is not taken care of. This last but not the least part will cover the new Rockstar in the mix. Being both Sass/CSS and JavaScript Developer, I can only tell you this is best approach according to me so what are you waiting for Christmas? Still 50 days to go. Let’s not wait and cover ECSS right now! 

ECSS is a methodology for writing stylesheets especially for large scale long-lived web projects that are rapidly changing day by day. You can quickly Isolate and contain styles, so modules become self-quarantining. But hey did I said above Isolating CSS is bad and you should look for Visual consistency, right? Yes but hey if you are just using CSS, that Visually consistency remains intact, and you can control what to Isolate and what to not. Thanks to isolation, it helps the designers/developers to gain maintainability with each visual pattern. With ECSS, the class names can communicate context, and initiate the logic and variation.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_043E65AF3EF3BB37503CCB5A25DF5E327B4531B8593ACA920CB59E98A1EC0C1A_1505854081053_ecss-good.png)

ECSS is Scalable; it doesn’t matter if you are a just sole developer or a dev team of a Corporate like Google, it provides a very dependable and maintainable approach when you are writing style sheets. It helps you **avoid abstraction and specificity.**  There is **one key selector which will rule them all** and will provide you a *single source of truth* for every key selector in your project. With this approach, the file size somehow remains minimal over long periods of time as you have the luxury of cutting out sections/features/components. 

ECSS has been inspired, or simply put has stolen a lot from OOCSS, SMACSS, and BEM. 

> **Good coders copy, great coders steal.**

That being said, **BEM** is the thing which has been taken most into accounts within ECSS for these simple reasons: 

  - All elements get the same specificity; a class is added to all the elements.
  - There is no use of type selectors so HTML structure isn't tightly coupled to the styles.
  - It's easy to reason about what the parent of an element is, whether viewing the DOM tree in the browser developer tools or the CSS in a code editor.

The use of modifiers within BEM didn’t excite the author of ECSS as mostly you would need to override styles on a Block waiting upon some possible event or outcome above it.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_043E65AF3EF3BB37503CCB5A25DF5E327B4531B8593ACA920CB59E98A1EC0C1A_1505854346399_bem-much-take.png)

From SMACSS the thing that was taken and found useful was dealing with the state. Yes the STATE, same that I referred with BEMIT. The declarative manner in which classes like `is-pressed` or attributes like `.btn[data-state=pressed]` is used, it surely helps you understand what the current state of the component is. Though it has changed a bit, will clear in upcoming sections.

## **ECSS Terminology and what it solves.**

![](https://d2mxuefqeaa7sj.cloudfront.net/s_043E65AF3EF3BB37503CCB5A25DF5E327B4531B8593ACA920CB59E98A1EC0C1A_1505323906120_ecss.png)

It makes a sense if we create CSS classes which are abstractions of the common functionality. The benefit to a simple algorithm is that they can then be re-used and re-applied on many varied elements. On larger and more complicated UI, it will become impossible to make even those minor tweaks and changes to those abstractions without accidentally effecting the areas where you didn't intend to. 

The best workaround is to isolate styles to the intended target. Believe it or not, but even at the cost of repetition, Isolation can buy you greater advantages. It allows you to have predictable styling and simple decoupling of styles. In fact, separation helps the designer to bring whatever they need to make, without being restricted to existing visual patterns.

One more thing, I wanted to tell you is that JavaScript (or any other programming languages) developer just have hatred towards `__` and `--` . They find it hard to read (which includes me) and what they like instead is this camelCase and PascalCase. So this maybe the best approach!

## **Dealing with Specificity?**

Ben Frain, the author of this methodology always wanted to negate the issues that are related to specificity. Thus, he adopted the widely used approach of insisting all selectors to use a single class-based selector. The structural HTML elements are never referenced in the style sheets as type selectors. Furthermore, as discussed above how ID selectors have a too bigger specificity comparing other selectors, thus they are completely avoided in this methodology. It is not because ID selectors are for anchor tags or that ID selectors are normally used for JavaScript or the concern that only one ID can be used in the whole document nor their is such thing that they are wrong to your CSS, it's just that you need a level playing field of selector strength and as seen above, this is just not possible with ID selectors. 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_043E65AF3EF3BB37503CCB5A25DF5E327B4531B8593ACA920CB59E98A1EC0C1A_1505386936268_css-problems-noarrow.png)

**Changes** to components are handled through simple overrides. So, the way they are handled from an authoring perspective makes them easy to manage and reasoned out to the public. Suppose you have an element that needs to be a different width if it is within a certain container. The best way to do this in Sass would be:

```postcss
.enr-Card_Section { 
    width: 100%;    
    .cat-Sidebar & {
      width: 50%;
    }
}
```   

And it would output this CSS below:

```postcss
.my-Module_Component {
  width: 100%;
}

.sw-Sidebar .my-Module_Component {
  width: 50%;
}
```   

This may seem like a subtle benefit. After all, we may be authoring things a little differently, by nesting the overrides, but the net result is standard CSS; an element that gets different styles based upon a different and more specific selector. The thing with this approach is that we are creating a **single source of truth** for each key selector. Everything that will ever make a change to that key selector is nested inside that set of curly braces. Moreover, that key selector will never be defined as a root rule again.

**This is !important:** If on the odd occasion the presence of one one override isn't enough, we can rely on `!important`. Yes that dreadly `!important`. Here’s what [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) says about `!important`

> When an `important` rule is used on a style declaration, this declaration overrides any other declarations. Although technically `!important` has nothing to do with specificity, it interacts directly with it. Using `!important,` however, is **bad practice** and should be avoided because it makes debugging more difficult by breaking the natural [cascading](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade) in your stylesheets. When two conflicting declarations with the `!important` rule are applied to the same element, the declaration with a greater specificity will be applied.

But, when there are events that are beyond our control mess with our styles from a 3rd party CSS file loaded on the page and we need some clout, we can and should be embracing `!important`. Here's an example of a state change:

```postcss
[aria-expanded="true"] & {
    transform: translate3d(0, -$super-height, 0)!important;
}
```
    
## **Yes Yes! Embracing Repetition**

The ECSS approach embraces repetition in the properties and values of the CSS. With ECSS, every single visual module or component is written with a micro-namespace to provide isolation from other modules and components. Things like `color` and `font-size` are declared in most components. The `@include headline` mixin generates a sizeable chunk of CSS to designate a particular font stack too. Yes! there's repetition across styles. Here is an example with Sass:

```postcss
.my-SubHeader_Wrapper {
  @include headline;
  align-items: center;
  
  /* We want the subheader hidden by default on mobile */
  display: none;
  font-size: $text12;
  background-color: darken($color-grey, 54%);
  border-bottom: 1px solid darken($color-grey, 54%);
  min-height: $size-fine-quadruple;
  
  /* But not in Desktop! */
  @include breakpoint(medium) {
    display: flex;
    background-color: darken($color-grey, 27%);
    color: darken($color-grey, 54%);
    font-size: $text13;
    min-height: 1.5rem;
    border-bottom: 1px solid darken($color-grey, 54%);
    border-top: 1px solid darken($color-grey, 33%);
  }
  /* However, even on mobile, if the SubHeader Wrapper is in section 1, we want to see it */
  .my-Classification_Header-1 & {
      display: flex;
  }
}
```   

This approach has these positives below:

  - It's verbose yet it relies on nothing.
  - It's generally context agnostic (save for the size context of where it is placed), any media queries that affect this component are defined within this single set of curly braces.
  - A namespaced module is written once and once only. When this module needs to change, you only need to look in this one place.
  - Writing rules with all overrides nested within creates a sort of micro-cascade. Where ordinarily overrides could be anywhere in the CSS, adhering to this method confines them to a very specific area. It then becomes far easier to reason about specificity as it relates to the rule.

**Zero component abstractions:** With ECSS, if there is a component that needs to be made which is quite similar, yet subtly different to an existing component, we would not look to abstract or extend from this current component. Instead, a new one would be written. This is how it goes in ECSS, even if 95% of the component is the same. The benefit of this is simply that each component is then independent and isolated to each other and the one that can exist without the another component and change as per their needs. 

Why? Here’s what the [book author](https://twitter.com/benfrain) says:

> A further analogy: a BMW 3 series has a lot in common with a BMW 5 series. But they are not the same. They may share some/many parts (the equivalent of CSS property and value combinations) but that doesn't make them the same. Their differences define them. They cannot be made of exactly the same parts because there is something inherently different about them. I'd argue it is the same case with modules and components defined with ECSS. The CSS language **IS** the abstraction. The property/value pairs of CSS already mean we can build what we want from individual parts.

## **Project organisation**

But the biggest part for me is that all the files that create a module are contained within the same folder. How? Let me show you - Instead of writing our code like this:

```
html/
- shopping-cart-template.html
- callouts-template.html
- products-template.html

js/
- shopping-cart-template.js
- callouts-template.js
- products-template.js

css/
- shopping-cart-template.css
- callouts-template.css
- products-template.css
```   

ECSS aims for something like this:

```
shopping-cart-template/
- shopping-cart.html
- shopping-cart.css
- shopping-cart.js

callouts-template/
- callouts.html
- callouts.js
- callouts.css

products-template/
- products.html
- products.js
- products.css
```  

When you look first at it, you may think this is not good but to let you know it brings a lot significant benefits. The code for each component becomes physically self-enclosed. Then, on our project, when features need changes or are deprecated, all associated code for that module (styles, view logic (HTML) and JS) can be easily updated/removed with ease. When a module is deprecated, all language files associated with it can be quickly withdrawn from the codebase in one go. It’s effortless, just delete that damn folder containing the module.

Just to be crystal clear, consider this folder structure:

```
ShoppingCart/
   - ShoppingCart.html
   - ShoppingCart.js
   - ShoppingCart.css
```     

Now suppose we are creating a new shopping cart to replace that old one:

```
v2ShoppingCart/
    - v2ShoppingCart.html
    - v2ShoppingCart.js
    - v2ShoppingCart.css
```

As soon as our v2 shopping cart is finished, it's easy to remove the code for the old version from our project; we just have delete that folder containing the original ShoppingCart.

## **Naming classes and selectors with ECSS**

Name-spacing the CSS of a module helps you to create a form of isolation. If you are preventing name collisions with other elements, the chunks of CSS can be moved easily from one environment to another (From Prototype to Production for example). It's also far less likely that a change of styles on one selector would inadvertently affect another.

> There are a number of other approaches to solve the name collision problem. For example, if you are building an application with the popular [React](https://facebook.github.io/react/) framework, consider [Radium](https://github.com/FormidableLabs/radium) which will inline the styles for each node so you can effectively serve no CSS at all. Naturally, there are trade-offs such as a lack of caching and no way to add reset styles but it it certainly solves the issue at hand. In addition, when not building with React, consider [CSS Modules](https://github.com/css-modules/css-modules). While requiring more involved tooling than ECSS it means you could forgo having to think about naming things altogether as it creates CSS scoped for you. Read [more about that here](https://medium.com/seek-ui-engineering/the-end-of-global-css-90d2a4a06284).

ECSS takes the notion of selector namespacing. Selectors are namespaced in two ways:

- a micro namespace: usually used to designate context but can also indicate a parent module
- the module's own namespace: usually the name of the logic file that created the element in question

## **The State of STATE**

A state is something that extends and overrides all other styles. For example, a Dropdown Menu may have a closed or active state. Notification Component may be in success, warning or error state. The State changes required to be communicated within the DOM, so that any styles changes necessary can be applied in the front-end of the application too.

**How ECSS used to handle state change:** Historically, ECSS followed the SMACSS approach of communicating state like examples below:

```postcss
.has-MiniCartActive {}
.is-ShowingValue {}

.is-Suspended {}
.is-Live {}
.is-Selected {}
.is-Busy {}
``` 

**Switching to WAI-ARIA:** As, this information has to go in the DOM purely for styling hooks, it may as well lift a little more weight while it's there. These same styling hooks can actually be placed in the DOM as [WAI-ARIA](http://www.w3.org/TR/wai-aria/) states. According to WAI-ARIA:

> These semantics are designed to allow an author to properly convey user interface behaviors (sic) and structural information to assistive technologies in document-level markup

While the specification only aimed at helping users with disability (via assistive technology) to communicate state and properties. But it can also serve the need of a web application project architecture beautifully. Adopting this approach results in a 'Win Win' situation. This way, we are helping to improve the accessibility of our web application, while also gaining a defined, well-considered vocabulary for communicating the states we will need in our application logic. Here's the prior example re-written with aria to communicate state:

```html
<button class="my-Button" aria-selected="true">Old Skool Button</button>
```

As this will eventually communicate the state (if any) of that node or its descendants. Within JavaScript world, the only change needed is shifting from `classList` amendments for state changes to `setAttribute` amendments. For example, to set our button attribute:

```javascript
button.setAttribute("aria-selected", "true");
```

In our CSS syntax, writing that change within a single set of braces (Sass) would be like this:

```postcss
.my-Button {
  background-color: $color-button-passive;
  &[aria-selected="true"] {
      background-color: $color-button-selected;
  }
}
```

That being said, the [CSS Selectors Level 4 specification](http://dev.w3.org/csswg/selectors-4/#attribute-case) makes provision for case insensitivity by using a `i` flag before the closing square bracket. This look something like this: 

```postcss
.co-Button {
   background-color: $color-button-passive;
   &[aria-selected="true" i] {
       background-color: $color-button-selected;
   }
}
```

## **The Ten Commandments of Sane Style Sheets**

According to the [book](https://leanpub.com/enduringcss), these ten rules should be always followed to make your CSS sensible.

- Thou shalt have a single source of truth for all key selectors
- Thou shalt not nest (unless thou art nesting media queries, overrides or thou really hast to)
- Thou shalt not use ID selectors (even if thou thinkest thou hast to)
- Thou shalt not write vendor prefixes in the authoring style sheets
- Thou shalt use variables for sizing, colours and z-index
- Thou shalt always write rules mobile first (avoid max-width)
- Use mixins sparingly (and avoid @extend)
- Thou shalt comment all magic numbers and browser hacks
- Thou shalt not inline images
- Thou shalt not write complicated CSS when simple CSS will work just as well

## **Further Reading**
  - http://ecss.io/
  - https://leanpub.com/enduringcss

## **Wrapping Up**

I hope this article series was helpful to you in some way or the other. End of the day, what I will say by my knowledge (and that’s very opinionated and personal viewpoint) is that though BEM and Styled Components solves many concerns related to CSS Specificity, I would dare say that the best practices revolve around Vue Single File Components or Enduring CSS. ECSS is an answer to BEM’s ugly class names and JS dev’s love of camelCase and PascalCase, That said I don’t see anything bad with the Vue.js handling of CSS-in-JS and this maybe right approach for you.

**Thanks a lot**, If you liked my article and also my passion for teaching and want to say hello… my twitter handle is [@harmanmanchanda](https://bit.ly/tw-harry). My DM’s are open to the public so just hit me up.
