# Frontend Nanodegree Project 4: Website Optimization

### Getting Started:

To launch the app you can:
- open this [link](https://github.com/Pasquale-Guglielmi/frontend-nanodegree-mobile-portfolio)
- clone or download this repository and open the *index.html* file on your browser

### Optimizations made:

##### Part 1: Optimize PageSpeed Insights score for index.html:
The following changes were made to index.html to optimize the critical rendering path:
- *pizzeria.jpg* was resized, compressed and added to the `/img` folder;  *profilepic.jpg* was optimized with ImageOptim
- links to wasteful external fonts stylesheets were deleted from the `<head>` to reduce number of critical resources
- `media=“print”` attribute added to *print.css* `<link>` to move this resource out of the critical rendering path
- `async` attribute added to *analytics.js* `<script>` to make analytics non parser blocking
- inlined scripts were moved at the end of the `<body>` to let the browser parse them only after the rest of the html document
- *style.css* was minified and inlined inside index.html `<head>` to reduce number and size of critical resources
- *index.html* was minified to reduce size of critical resources

##### Part 2: Optimize Frames per Second in pizza.html
The following changes were made to *views/js/main.js* to make *views/pizza.html* render with a consistent 60 fps frame-rate while scrolling the page:
- *pizza.png* and *pizzeria.jpg* were served resized, compressed and optimized
- `resizePizzas()` code was retailored to prevent forced synchronous layout on user’s interaction with the `#sizeSlider`:
  * `changePizzaSizes()` was drastically simplified getting rid of useless and odd code
  * `document.querySelectorAll(".randomPizzaContainer")` was moved outside of the `for` loop to avoid forced reflow
- function to generate moving pizzas elements was retailored to minimize number of generated pizzas, basing the calculation of this number on the client's viewport dimensions; a dedicated resized and optimized version of *pizza.png* (moving_pizza.png) was added to the `/views/images` folder and served to generate moving pizzas elements
- `updatePositions()` was retailored and decoupled from the `'scroll'` event and made handled by a `requestAnimationFrame`to free the browser from expensive reflow and repaint operations:
  * new functions were added ( `onScroll()` and `requestAnimation()` ) and global variables declared (`scrollTop` and `animation`) in order to manage the `requestAnimationFrame(updatePositions)` request while scrolling the page
  * methods querying the DOM, such as `.scrollTop` and `document.querySelectorAll`, have been grouped and separated from methods manipulating it, and kept outside loops managing styles changes to prevent forced synchronous layout
- `.querySelector` was replaced by `.getElementById` where possible to reduce the time to select elements

### Resources:

- **Udacity Courses:** [Website Performance Optimization](https://www.udacity.com/course/website-performance-optimization--ud884) and [Browser Rendering Optimization](https://www.udacity.com/course/browser-rendering-optimization--ud860)
- [Leaner, Meaner, Faster Animations with requestAnimationFrame](http://www.html5rocks.com/en/tutorials/speed/animations/?redirect_from_locale=it) by [Paul Lewis](http://www.html5rocks.com/en/profiles/#paullewis)
- [How (not) to trigger a layout in WebKit](http://gent.ilcore.com/2011/03/how-not-to-trigger-layout-in-webkit.html) by [Tony Gentilcore](https://plus.google.com/118178843327307114710)

---
### Original Project Instructions:

## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository and inspect the code.

### Getting started

####Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

####Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js.

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>
