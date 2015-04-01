# react-spark-scroll

React port of [spark-scroll](https://github.com/gilbox/spark-scroll/). 

# install

    npm install react-spark-scroll

# [demo](http://gilbox.github.io/react-spark-scroll/examples/demo/demo.html)

Documentation still needs to be updated, in the meantime checkout the
[demo](http://gilbox.github.io/react-spark-scroll/examples/demo/demo.html)
and the [source code](https://github.com/gilbox/react-spark-scroll/blob/master/examples/demo/app.js).
It's so declarative you might not even need documentation ;-)

## why?

I was curious to find out how difficult it would be to create complex animations 
with React. At first, I thought that React's lack of a direct equivalent to 
angular's attribute-type directive (`restrict: 'A'`) would be a major drawback. However, using
[higher-order components](https://gist.github.com/sebmarkbage/ef0bf1f338a7182b6775) 
to generate variations of the same component turned out to be a remarkably
[elegant](https://github.com/gilbox/react-spark-scroll/blob/master/src/index.js#L70)
[solution](https://github.com/gilbox/react-spark-scroll/blob/master/examples/demo/app.js#L25). 
Ie., `<SparkScroll.div />`, `<SparkScroll.span />`,  `<SparkScroll.h1 />`, etc...

The one place where angular might have an advantage is
through it's ability to fascilitate more expressive 
syntax. For example, to toggle a class in angular:

    <!-- angular: -->
    <section 
      class="pin" 
      spark-trigger="pin-cont"
      spark-scroll="{
          topTop: { 'downAddClass,upRemoveClass': 'pin-pin' },
          bottomBottom: {  'downAddClass,upRemoveClass': 'pin-unpin' }
      }">

...vs in react:

    <SparkScroll.section
      className={cx("pin",{
        'pin-pin':this.state.pinPin,
        'pin-unpin':this.state.pinUnpin})}
      proxy="pin-cont"
      timeline={{
        topTop: {
          onDown: () => this.setState({pinPin:true}),
          onUp:   () => this.setState({pinPin:false})
        },
        bottomBottom: {
          onDown: () => this.setState({pinUnpin:true}),
          onUp:   () => this.setState({pinUnpin:false})
        }
      }}>

However, it is *much much much* easier to reason about what is
actually happening in the react version. All the tricks employed by
angular to achieve the expressiveness is not worth the confusion it 
often creates for developers, IMO.

# status

### Completed:

- Keyframe animations w/Rekapi
- Formulas
- Actions (only supports `onUp` and `onDown` with different callback semantics than `spark-scroll`)
- onScroll `callback` prop (previously in angular was `spark-scroll-callback` attribute)
- Custom formulas, actionProps
- sparkSetup
- `SparkProxy` (in angular called `sparkTrigger`)
- publish to npm
- Demo
- Invalidation
    * Manual invalidation mechanism
    * Invalidation interval
    * Automatic invalidation on window resize

### Todo:

- Test on various browsers
- Re-parsing of data when changed
- README
- Support for GSAP

### Probably Won't do:

- [spark-scroll-ease](https://github.com/gilbox/spark-scroll/blob/master/src/spark-scroll.coffee#L213)
  attribute (Not really liking this feature)
