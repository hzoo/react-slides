class: center, middle, dark-bg

[![:scale 100%](https://i.imgur.com/KwiNy2T.png)](https://facebook.github.io/react/)

---

Some React Users!

- [Facebook](facebook.com): comments, chat, search, notifications... + new JS development. React Native: f8 app, Facebook Groups, Facebook Ads Manager. 
- [Instagram](https://instagram.com/)
- [AirBnB](https://twitter.com/spikebrehm/status/491645223643013121): airbnb.com/resolutions
- [Asana](https://eng.asana.com/2014/11/asana-switching-typescript/): React + typescript
- [Atlassian](https://developer.atlassian.com/blog/2015/02/rebuilding-hipchat-with-react/): Hipchat
- [BBC](http://www.bbc.co.uk/blogs/internet/entries/47a96d23-ae04-444e-808f-678e6809765d): Homepage
- [Brackets](http://www.kevindangoor.com/2014/09/intro-to-the-new-brackets-project-tree/): Project Tree (code editor)
- [Codeacademy](https://twitter.com/codecademy/status/566365837905625088): Learning environment ([slides](https://docs.google.com/presentation/d/1b7sZOqBuTnTTKP7Rk1xgbMspCsFZBR2mzsHUF7Zd62g/edit?pli=1#slide=id.g61b77bb41_0114))
- [Flipboard](http://engineering.flipboard.com/2015/02/mobile-web/): created [react-canvas](https://github.com/Flipboard/react-canvas)
- [Khan Academy](http://joelburget.com/backbone-to-react/): [equation editor](http://benalpert.com/2013/06/09/using-react-to-speed-up-khan-academy.html), student exercises, admin panels.
- [Netflix](http://techblog.netflix.com/2015/01/netflix-likes-react.html)
- [Pivotal](https://twitter.com/stubbornella/status/562678360275701763): Pivotal UI
- [Reddit](https://twitter.com/holtbt/status/493852312604254208): reddit gifts
- [The New York Times](http://www.nytimes.com/interactive/2014/02/02/fashion/red-carpet-project.html?_r=1): 2014 Red Carpet Project, Festival de Cannes, world cup
- [WhatsApp](https://twitter.com/reacteurope/status/558097823330492416): web app
- [Wired](http://www.wired.com/2015/03/wired-dot-com-from-the-devs/): using in articles for live updates
- [XKCD: xkcloud](https://xkcd.com/1506/)
- [Yahoo](http://www.meetup.com/ReactJS-San-Francisco/events/206685812/): Yahoo! mail
- [Zendesk](https://twitter.com/ryanseddon/status/540256931600805888)

---

class: center, middle
background-image: url(https://i.imgur.com/2ue2vQp.png)

.white[Lets you write declarative, composable, simple UIs.]

---
class: center
background-image: url(https://imgs.xkcd.com/comics/sandwich.png)

Declarative

---

# Declarative vs. Imperative

- Focus on *what* needs to be done (not implementation details).

```javascript
var numbers = [1,2,3,4,5];
```

```javascript
// triple each number in the list and only get the even ones.
```

```javascript
// imperative
var tripledEvens = [];
for (var i = 0; i < numbers.length; i++) {
    var newNumber = numbers[i] * 3;
    if (newNumber % 2 === 0) {
        tripledEvens.push(newNumber);
    }
}
```

```javascript
// declarative/functional
function triple(n) { return n * 3; }
function evens(n) { return n % 2 === 0; }
var tripledEvens = numbers.map(triple).filter(evens);
```

- Allows us to talk about problems at a higher level (abstraction).

???
- HTML/CSS/SQL, functional languages/features
- Usually more concise (don't have to deal with internals)

---


```sql
-- Declarative: describe what should happen

SELECT * from dogs
INNER JOIN owners
WHERE dogs.owner_id = owners.id
```

```javascript
// Imperative: explain how it happens

// dogs = [{name: 'Fido', owner_id: 1}, {...}, ... ]
// owners = [{id: 1, name: 'Bob'}, {...}, ...]
var dogsWithOwners = [];
var dog, owner;

for (var di = 0; di < dogs.length; di++) {
    dog = dogs[di];

    for (var oi = 0; oi < owners.length; oi++) {
        owner = owners[oi];
        if (owner && dog.owner_id === owner.id) {
            dogsWithOwners.push({
                dog: dog,
                owner: owner
            });
        }
    }}
}
```

- Easier to reason, maintain, test

http://latentflip.com/imperative-vs-declarative/

---
class: center, middle

So what? We use imperatives to change the DOM.

```javascript
var p = document.createElement("p");
document.body.appendChild(elements);
document.body.removeChild(elements);
document.body.addChild(elements123);
// move elements, modify elements...
```

---

![:scale 25%](https://i.imgur.com/x36z4gi.png)

```javascript
// Example of a notification UI

if (count > 99) {
    if (!hasFire()) {
        addFire();
    }
} else {
    if (hasFire()) {
        removeFire();
    }
}
if (count === 0) {
    if (hasBadge()) {
        removeBadge();
    }
    return;
}
if (!hasBadge()) {
    addBadge();
}
var countText = count > 99 ? '99+' : count.toString();
getBadge().setText(countText);

// Retained mode (DOM, svg)
```

???
- Complexity in UIs scales with the number of states; O(n) states.
- Need to write code to account for the state transitions.

---

```javascript
// Can start at 10:10 in the video.
```

<iframe width="640" height="360" src="https://www.youtube.com/embed/rI0GQc__0SM?rel=0" frameborder="0" allowfullscreen></iframe>

???
- Immediate mode (video games, webgl, canvas)
- So when data changes - instead of data-binding or observables, React will re-render the view.
- Allows components (more specifically `render()`) to describe your UI at any point in time (Don't need to keep track of state in your head).
- A component is basically a state machine. You update a component's state and it renders a new UI based on the state.
- React doesn't remove and readd the whole DOM on each change (you would lose performance, form state, scroll position, focus, etc).

---

React wraps the imperative DOM with a declarative layer
```javascript
if (count === 0) {
```

```javascript
    return <div className="bell"></div>;
```

```javascript
} else if (count < 99) {
```

```javascript
    return (
        <div className="bell">
            <span className="badget">{count}</span>
        </div>
    );
```

```javascript
} else {
```

```javascript
    return (
        <div className="bell onFire">
            <span className="badge">99+</span>
        </div>
    );
}
```

---
class: middle, center

Virtual DOM

---

Diff Alg

```javascript
var MyComponent = React.createClass({
    // What is returned is just a javascript object.
    render: function() {
        if (this.props.first) {
            return <div className="first"><span>A Span</span></div>;
        } else {
            return <div className="second"><p>A Paragraph</p></div>;
        }
    }
});
```

```javascript
// None to first
Create node: <div className="first"><span>A Span</span></div>
```
```javascript
// First to second
Replace attribute: className="first" by className="second"
Replace node: <span>A Span</span> by <p>A Paragraph</p>
```
```javascript
// Second to none
Remove node: <div className="second"><p>A Paragraph</p></div>
```

React finds the minimal set of operations between the two render trees (previous and current state).

http://calendar.perfplanet.com/2013/diff/

---

Optimizations to go from `O(n^3)` to `O(n)`

Level by Level

![:scale 40%](http://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/1.png)

List Diffing

![:scale 40%](http://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/2.png)

Component Diffing

![:scale 40%](http://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/3.png)

---

Batching

![:scale 35%](http://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/4.png)

Sub-tree Rendering

![:scale 35%](http://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/5.png)

Selective Sub-tree Rendering (`shouldComponentUpdate`)

![:scale 35%](http://calendar.perfplanet.com/wp-content/uploads/2013/12/vjeux/6.png)

---

Demo (4:47)

<iframe width="640" height="360" src="https://www.youtube.com/embed/z5e7kWSHWTg" frameborder="0" allowfullscreen></iframe>

https://youtu.be/z5e7kWSHWTg?t=4m47s

---

React Inspired
- [Angular2 rendering engine](https://docs.google.com/document/d/1M9FmT05Q6qpsjgvH1XvCm840yn2eWEg0PMskSQz7k4E/preview?sle=true&pli=1#) will use vDOM
- [Ember Glimmer engine](http://f.cl.ly/items/0t031v2Z3y001V1N0F3N/Virtual%20DOM.pdf) will use vDOM ([PR](https://github.com/emberjs/ember.js/pull/10501))
- [React Native](https://facebook.github.io/react-native/): framework to write iOS (and later Android) apps using React.
- [ComponentKit](http://componentkit.org/): a iOS library by Facebook to make apps similar to React
- [React Canvas](https://github.com/Flipboard/react-canvas): adds the ability for React components to render to <canvas>.

Similar to React
- [Riot.js](https://muut.com/riotjs/)
- [Mithril](https://lhorie.github.io/mithril/)
- [Om](https://github.com/omcljs/om): ClojureScript interface to React
- [Mercury](https://github.com/Raynos/mercury): (uses `virtual-dom`)
- [Elm-html](https://github.com/evancz/elm-html): HTML in Elm (uses `virtual-dom`)

---
class: center
background-image: url(http://i.imgur.com/V98O2zK.png)

Composition

---

#### Components: similar to creating your own element (`h1`, `select`, `img`)
* An element has it's own structure, default styles, and functionality (no interference between components).
* A component uses JSX/HTML, CSS, and JS.
    
```javascript
// Allows you to use a component with a simple require
define(['components/toolbar'], function (Toolbar) {})

// commonjs/node
var Toolbar = require('components/toolbar');

// es6 modules
import Toolbar from 'components/toolbar';
```

![:scale 25%](https://s3.amazonaws.com/media-p.slid.es/uploads/danabramov/images/661109/Screen_Shot_2014-09-25_at_0.46.11_.png)
![:scale 25%](https://s3.amazonaws.com/media-p.slid.es/uploads/danabramov/images/661211/Screen_Shot_2014-09-25_at_1.09.19_.png)
![:scale 25%](https://s3.amazonaws.com/media-p.slid.es/uploads/danabramov/images/661209/Screen_Shot_2014-09-25_at_1.08.37_.png)

http://slides.com/danabramov/components-react-flux-wip#/16

???

Components vs. a mix of a partials, scripts, templates, etc.

---

An app can be broken down into simple components.

![:scale 100%](https://d262ilb51hltx0.cloudfront.net/max/1320/1*8fuXs-f2LJHYnEfxGKYdLA.png)

React components, Ember.Components, Angular directives, Web Components...

https://medium.com/@addyosmani/javascript-application-architecture-on-the-road-to-2015-d8125811101b

---

### Templates (logic in HTML)

```javascript
// Handlebars
<ul id="comments">
    {{#each comments}}
        <li>{{text}}</li>
    {{/each}}
</ul>
```

```javascript
// Kendo
<script id="javascriptTemplate" type="text/x-kendo-template">
    <ul>
    # for (var i = 0; i < data.length; i++) { #
        <li>#= data[i] #</li>
    # } #
    <ul>
<script>
```

```javascript
// Manual DOM creation
var out = "<ul>";
    for(var i=0, l=items.length; i<l; i++) {
        out = out + "<li>" + options.fn(items[i]) + "</li>";
    }
return out + "</ul>";
```

---

### Write HTML-like syntax for structure (rather than learning another DSL)

```javascript
// React (ES5)
return (
    var items = this.props.items;
    var listItems = items.map(function(i) {
        return <li>{i}</li>;
    });
    <ul>
        {listItems}
    </ul>
);
```

```javascript
// React (ES6)
return (
    <ul>
        {this.props.items.map((i) => <li>{i}</li>)}
    </ul>
);
```

---

```javascript
var Avatar = React.createClass({
  render: function() {
    return (
      <div>
        <ProfilePic username={this.props.username} />
        <ProfileLink username={this.props.username} />
      </div>
    );
  }
});
var ProfilePic = React.createClass({
  render: function() {
    return (
      <img src={'http://graph.facebook.com/' + this.props.username + '/picture'} />
    );
  }
});
var ProfileLink = React.createClass({
  render: function() {
    return (
      <a href={'http://www.facebook.com/' + this.props.username}>
        {this.props.username}
      </a>
    );
  }
});
React.render(
  <Avatar username="pwh" />,
  document.getElementById('example')
);
```

https://facebook.github.io/react/docs/multiple-components.html#composition-example

---

#[React Dev Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) ([Github](https://github.com/facebook/react-devtools))

![:scale 100%](http://i.imgur.com/bDYkFqU.png)

---

# [JSX Specification](https://facebook.github.io/jsx/)

+ [HTML to JSX Converter](https://facebook.github.io/react/html-jsx.html)

```html
<div class="awesome" style="border: 1px solid red">
  <label for="name">Enter your name: </label>
  <input type="text" id="name" />
</div>

<div className="awesome" style={{border: '1px solid red'}}>
  <label htmlFor="name">Enter your name: </label>
  <input type="text" id="name" />
</div>
```

+ [Supported tags/attributes](https://facebook.github.io/react/docs/tags-and-attributes.html)
+ Differences from HTML (reserved words in JS; React matches the JS DOM API)
  + `for` -> `htmlFor`,
  + `class` -> `className`

---

# JSX Complier
- It's just syntax. You can use anything in javascript!
- [JSX Complier](https://facebook.github.io/react/jsx-compiler.html)

Turns
```html
<div>Hello {this.props.name}</div>;
```
into
```javascript
React.DOM.div(null, "Hello ", this.props.name),
React.createElement("div", null, "Hello ", this.props.name);
```
- Just another build step like uglify
    - Can use [jsx-transform](https://github.com/alexmingoia/jsx-transform), [react-tools](https://www.npmjs.com/package/react-tools), [babel](https://babeljs.io/)

---
class: center, middle

[Example](http://jsbin.com/wotafifiqa/1/edit)

![:scale 100%](https://i.imgur.com/dZ1XG9I.png)

---
class: center, middle

Simple

---

class: center, middle
React API

(Demo: http://jsbin.com/yefabumixi/1/edit), increment the number.

So the next would be http://jsbin.com/yefabumixi/2/edit

---

Create a custom component (your own `select`):
```javascript
var NewButton = React.createClass({});
```

Render a component to a container:
```javascript
React.render(<NewButton />, document.body);
```

Props
```javascript
// Props are like html attributes and are seen as immutable
<NewButton color={ 'red' } />
```
```javascript
getDefaultProps: function() { return { color: 'green' } }
```
```javascript
// Validate component usage (only in development)
propTypes: { color: React.PropTypes.string }
```

https://facebook.github.io/react/docs/top-level-api.html

---
State
```javascript
// Unlike props, state can change over time
this.state.numClicks
```
```javascript
getInitialState: function () { return { numClicks: 0 } }
```

Change State
```javascript
// from handleClick()
this.setState({
  numClicks: this.state.numClicks + 1
})
``` 

Render Function
```javascript
// render function
render: function() {  
    return (<div onClick={this.handleClick}>
      Num clicks: {this.state.numClicks}
    </div>);
  }
```

- Mixins (React 0.12), React.renderToString, statics, contexts, ES6 Classes

---

[Component Lifecycle methods](https://facebook.github.io/react/docs/component-specs.html#lifecycle-methods)

```javascript
// beforeRender
componentWillMount: function() {
  // initial code to be invoked once
}

// afterRender
componentDidMount: function() {
  // can use 3rd-party libraries like Kendo, setTimeout, AJAX
  var node = this.getDOMNode(); // get access to the actual DOM
}

// Destroy
componentWillUnmount: function() {
  // can unbind/remove event listeners here
}

// Before props change
componentWillReceiveProps: function(nextProps) {}

// Before state change
componentWillUpdate: function(nextProps) {}

// after DOM is updated
componentDidUpdate: function(prevProps, prevState) {}

// Whether to re-render or not
shouldComponentUpdate: function(nextProps, nextState) {
  // return true or false
}
```

---

![:scale 100%](https://i.imgur.com/lIM3rLA.png)

---

class: center, middle
Misc

---

#### Seperate data-fetching and rendering concerns (see [Relay](https://facebook.github.io/react/blog/2015/02/20/introducing-relay-and-graphql.html))

```javascript
class CommentListContainer extends React.Component {
  constructor() { this.state = { comments: [] } }
  componentDidMount() {
    $.ajax({
      url: "/my-comments.json",
      dataType: 'json',
      success: function(comments) {
        this.setState({comments: comments});
      }.bind(this)
    });
  }
  render() {
    return <CommentList comments={this.state.comments} />;
  }
}
```

```javascript
class CommentList extends React.Component {
  constructor(props) { super(props); }
  renderComment({body, author}) {
    return <li>{body}—{author}</li>;
  }
  render() { 
    return <ul> {this.props.comments.map(renderComment)} </ul>;
  }
}
```

https://medium.com/@learnreact/container-components-c0e67432e005

???
Also can reuse the UI component and check PropTypes.

---

#### Seperation of concerns: props (immutable) vs. state (changable)
  * Encourages less state in less places
    - "shared mutable state is the root of all evil"
    - Can have stateless components and stateful components
  * Simpler to test: [Jest](https://facebook.github.io/jest/docs/tutorial-react.html)
    * Test a component by rendering as a string and and comparing the output. (Events can be created synthetically)

---

background-image: url(immutable-js.png)

### Immutable data structures: [immutable-js](https://github.com/facebook/immutable-js)
- Can optimize rendering with `shouldComponentUpdate` (check equality by reference)

---

- Easy to [snapshot](http://blog.circleci.com/local-state-global-concerns/) (the view is a function of the state)
- Easy to incorporate undo/redo

<iframe width="640" height="480" src="https://www.youtube.com/embed/5yHFTN-_mOo" frameborder="0" allowfullscreen></iframe>


---

Server rendering (`React.renderToString`)

- A faster initial experience for the user (remove extra http requests).
- Isomorphic JavaScript: shared javascript code (on client and server)
- Was difficult to do SEO for client apps since they render on DOM load until [google bot changed](http://googlewebmastercentral.blogspot.com/2014/05/understanding-web-pages-better.html)

---

#### Data
+ Normally data is passed down through components and events flow up
+ [Flux](https://facebook.github.io/flux/): a global event system with one way data flow

![:scale 50%](http://www.infoq.com/resource/news/2014/05/facebook-mvc-flux/en/resources/flux-react-mvc.png)

![:scale 50%](https://www.infoq.com/resource/news/2014/05/facebook-mvc-flux/en/resources/flux-react.png)

---

[![:scale 100%](https://i.imgur.com/xkKHtbl.png)](https://facebook.github.io/react-native/)

- Ability to push updates without review
![](https://pbs.twimg.com/media/B_sF4mXVEAAdgJk.png:medium)
- Native iOS Components, Asynchronous Execution, Flexbox, Polyfills, Extensible
