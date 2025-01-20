# `🖐️` Introduction
While experimenting with CSS, I stumbled upon a fascinating trick: using CSS variable fallbacks to mimic an if-else structure. It pushes the boundaries of CSS and opens up new possibilities.

I discovered this trick will playing with CSS and i think this concept has immense potential, presenting a creative and groundbreaking way to utilize CSS variables to their fullest. <br/>
So, join me as I present you some CSS magic 🧙!

Disclaimer: <br/>
To my knowledge (Internet research) there is no record of this principle being used, but it may have been discovered already (let me know). But if it hasn't, it certainly has now.

# `📖` Theorie
There are two key aspects you have to understand about CSS to fully understand the concept.
- One is that you can initialize a CSS varibale with no value `--test: ;` and this will still count as initialized.
- The other one is the Fallback behaviour of CSS variables `var(--test, red)`, where a default value is being applied, if the variable has not been initialized, so if there is no `--test` in this example `red` would be the outcome.

# `✍️` Concept / Examples
The basic principle is that if you have multiple variables that function as booleans, then if you now define the currently active variable for example by `Classes` or `Pseudo-classes` the only initialised variable will be that one and we can work with that. What this means, is that we now need to reverse this to be in line with the CSS Fallback principle. As you can see below, if `html` had a class `bool1`, `--bool1` would be active and the background-color would change to `blue`, you might think "blue?" but yes, that's because it's the fallback of `--bool2` because `--bool2` is not defined in this case. And now you can see why it is important to initialise the variable with no value, because if you initialised it with "", 0 etc. it would look like this `background-color: "" blue;` but because we initialise it with no value we get this `background-color: "<no value>" blue;` which is still valid CSS. You are also not limited to only two variables see [multiple](examples/multiple.scss).

```CSS
html.bool1 {
  --bool1: ;
}

html.bool2 {
  --bool2: ;
}

background-color: var(--bool1, red) var(--bool2, blue);
```

It may be an overkill, if you use it for small things but can get to a huge advantage if you use it in complexer cases, like sown with the darkmode below.

## Problem
- A problem is that currently if two variables are active at the same time or none are active it will breake, because you can't give two/no colors to the background but im trying my best to find a solution to this problem.
- If there are to many variables used it will get messy but i'm currently trying to figure out a solution to this problem see TODO's.

## Examples

I found it very usefull when I was working on my [darkmode](examples/darkmode.scss), because as I discovered this methode, I was finally able to make one time changes to the design, that means I don't have to create a extra color for every special case and keep the color file in a managable size with the important colors.

- Example 1: <br/>
If I have an error color and I want to lighten it in lightmode using SASS I can use `lighten($errorColor, 20%)` and leave it on `errorColor` in the darkmode, so I don't ave to create a variable like `--error-color-lighen-in-lightmode`.

<br/>

I think there are a lot of other use cases you could use this for, try it out and see out what you can do with it.

# `📌` TODO's
- [ ] Search for a way to invert the Condition so !false => true.
- [ ] Search for a way to allow multipel to be true (prioritization or condition if both are true).

# `🛡️` License
This project was licensed under the Apache-2.0 License.
<br />
See [`License`](LICENSE) for details.


# `📧` Contact
You can contact me by [mail](mailto:contact@fabian.li).
