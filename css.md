---

class: center
#### CSS

![:scale 100%](nest.png)
---

[Online LESS Complier](http://lesstester.com/)

```css
.container {
    .a, .b {
      .c,
      .d {
        .e,
        .f {
          .g {
            .h .l-i,
            .h .l-j,
            .h .l-k,
            .m {
              input {
                  height: 3rem;
              }
            }
          }
        }
      }
    }
}
```

---

- Nesting or emulating your html structure leads to overly specific selectors.
    - That means you are creating styles to match every individual thing rather than generalizing.
    - It's basically the same thing as inlining styles or using ids.
    - Styles become too coupled to the DOM (location dependent) they refer to and break everything.
    - You end up having to create more and more specific selectors (even !important when it's not needed)
    - Bad for performance (takes longer to render) as well as file size.
- http://thesassway.com/beginner/the-inception-rule
- http://cssguidelin.es/#specificity

---

- Creating UI's in terms of components helps to allivetiate this problem. Styles can be scoped to the components.
- Many different ways to do this. One way:
```javascript
ComponentName--modifierName // Notification--error
ComponentName-descendentName // StoryWall-stories
ComponentName.is-stateOfComponent // Story.is-active
```
- Because classes are namespaced by component, you won't have trouble with overlapping styles or cascading issues.
- If you name the styles the same as the component, it becomes much easier to maintain.
- You can just Ctrl-f for the Component in your less file. And if you really wanted, you could even create a less file per component.
- With nesting, you can't even search for what the element inspector gives you because you can only search for 1 word at a time. So you waste a lot of time just trying to get to the correct selector (if you don't use sourcemaps). You don't easily know the folder or file the styles are in.
- Especially if your classes are all generic names. You have to search through each result to finally find the css you need to change.
- A style guide can help but also has it's own nesting, is hard to enforce, only cares about html/css.
