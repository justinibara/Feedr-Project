# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Unit Project #2: Feedr

### Overview

The web is an ever growing medium and it is getting more and more difficult
to filter useful information. In our journey to writing beautiful JavaScript we
have come and will come across a great many reference points that will guide our
learning. This is where personal feeds come in very useful. Online feeds are
like to-do lists in that they can be infinitely personalized and there is not
one solution that works for everybody.

For our Unit 2 project we will build __Feedr__, a personalized feed reader. Our
feed reader will pull feeds from our favorite blogs. The user will be able to
filter between publications through the dropdown on the header menu.
Clicking/tapping on one of the articles will load a pop up with more
information. The user from that point will be able to either dismiss the
additional information or go to the referenced article.

This will be our first single page app. All of our application views will be
contained in the provided [index.html](index.html) file. Our task, after we pull from the
respective feed APIs, will be to toggle the appropriate classes and content for
the provided site architecture.

---

### Technical Requirements

#### Your core application rules:

__Feed sources:__

Give the user the ability to pull from a multiple news sources. Here are a few news sources we suggest:

- [Chronicling America](https://chroniclingamerica.loc.gov/about/api/)
- [News API](https://newsapi.org/)
- [Hearst publishing group](http://developer.hearst.com/) (Cosmopolitan, Elle, Popular Mechanics, Road and Track, etc.)
- [Reddit](https://www.reddit.com/top.json)

If you use your own feeds, they must have APIs with the following minimum
requirements:

- Each article must provide an image source for the circular thumbnail at the
  left of the article.
- Must provide either a category, tag, or custom taxonomy to display below the
  title (of course title of article is also required).
- Must provide a point, ranking, or some type of total impressions for the
  respective article.
- Must provide either a full version or a summary of the article for the pop up
  screen.

__Feed rules:__

- When the application first loads display the loading container (see below on
  instructions to toggle this). When you successfully retrieve information from
  the default API hide the loader and replace the content of the `#main`
  container with that of the API. The DOM structure of each article must adhere
  to the `.article` structure.
- When the user selects an article's title show the `#popUp` overlay. The
  content of the article must be inserted in the `.container` class inside
  `#popUp`. Make sure you remove the `.loader` class when toggling the article
  information in the pop-up.
- Change the link of the "Read more from source" button to that of the
  respective article.
- When the user selects a source from the dropdown menu on the header, replace
  the content of the page with articles from the newly selected source. Display
  the loading pop up when the user first selects the new source, and hide it on
  success.
- Add an error message (either alert or a notification on the page) if the app
  cannot load from the selected feed.

__Additional UI interaction rules:__

- When the user clicks/taps the search icon, expand the input box. Best approach
  for this is to toggle the `.active` class for the `#search` container. If the
  search input box is already expanded tapping the search icon again will close
  the input. Pressing the "Enter" key should also close the opened input box.
  _See Bonus 2 for search filtering functionality._
- When the app is first loading and when the user selects to load a new feed
  from the dropdown, display the `#popUp` container with the `.loader` class.
  You can toggle the `.hidden` class from the container to display/hide the
  overlay container.
- Add functionality to hide the pop-up when user selects the "X" button on the
  pop-up.
- Clicking/tapping the "Feedr" logo will display the main/default feed.


#### Bonus

1. Merge all feeds into one main feed in chronological order for the initial
   view. When the user clicks/taps the "Feedr" logo at the top, they should be
   return to this feed. This will be the new "home view."
2. Filter feed by title according to user keyboard input on the search input
   box. This should run the filter on every keystroke. When the input box is
   cleared, all articles should display in the respective feed.
3. Add infinite scrolling. Start displaying only the first 20 articles and keep
   loading more on user scrolling.
4. To avoid long load times every time you go to the homepage, try storing the data locally, try looking into the browsers `localStorage`. Also try implementing a time frame so that your website knows to only retrieve new data from the APIs after a certain amount of time has passed.

---

### Common Issues

#### CORS Issues
You will find that many APIs that do not support either [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) or [JSONp](https://en.wikipedia.org/wiki/JSONP) will result in a cross-domain restriction error ("No 'Access-Control-Allow-Origin' header is present...") in the browser. To get around this, you can use the following proxy server to filter your API requests.

Let's say you wanted to use the Reddit API, which has the following endpoint:

`https://www.reddit.com/top.json`

If you preface the request with the proxy server API as follows...

`https://cors.bridged.cc/https://www.reddit.com/top.json`

...you should be able to use the Reddit API without encountering a cross-domain restriction error. Here's a code example of how you might use the proxy server:

```js
let apiCall = fetch('https://cors.bridged.cc/https://www.reddit.com/top.json');

apiCall
  .then(res => res.json())
  .then(results => {
    console.log(results.data.children);
    results.data.children.forEach(function(result){
      // renderRows(result.data.title);
    });
  })
  .catch(err => console.log(err));
```

#### Request location

APIs have certain restrictions and for good reason. Here is an issue you may run into using the News API:
```js
{
  status: "error", 
  code: "corsNotAllowed", 
  message: "Requests from the browser are not allowed on the Developer plan, except from localhost."
}
```
In that case, we have done this before. We will have to launch a local server. Either use VS Code's Live Server extension or run the `http-server` command. From there replace the url with `localhost:` followed by the port number is opened on. Should look like this: `localhost:<PORT NUMBER>`


---

### Necessary Deliverables

* A __working Feedr, built by you__, that can be run locally
* A __new git repository hosted on Github__, where your codebase is maintained.
  - Most of the your will be done on the __app.js__ file. You may update
  the index.html and style.css files if you would like to further customize your
  app.
* A 5-10 minute **presentation** including 3 technical hurdles, 2 new things you learned, Q&A.

---

### Getting Started

Begin by looking at the starter code [here](https://github.com/generalassembly-studio/JS-Unit-2-Project-Starter-Code). Make sure you have the starter code on local machine:

```
$ git pull upstream master
```
Remember to commit as you complete different functions and features:
```
$ git add .
$ git commit -m "A description of what was added"
$ git push -u origin master
```


## Suggested Ways to Get Started

> Below are some more specific ways for ways in which you can help students get started on the project.

  - Start by doing a `console.log` of the incoming feeds to confirm you have a successful transaction before you start mapping anything out
  - Map out all of the needed fields/properties from each respective feed.
  - Normalize the data from the feeds to get a uniform data set to work with
  - Add the DOM functionality and populate the values from the API calls  
  - (Optional) Have the [JSON View chrome extension](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en)
    to get a clean view of the JSON dump in your browser.
  - Test small pieces of functionality frequently, to make sure everything is working.
  - Use tools such as Stack Overflow, Google and documentation resources to solve problems.

---

### Useful Resources

**Key Resources**

- [MDN JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [jQuery Event Basics](https://learn.jquery.com/events/event-basics/)
- [Understanding Event Delegation](http://learn.jquery.com/events/event-delegation/)
- [jQuery Tutorial](http://tutorials.jenkov.com/jquery/index.html#jquery-version-used-in-this-tutorial)
- [A beginner's guide to HTTP and REST](http://code.tutsplus.com/tutorials/a-beginners-guide-to-http-and-rest--net-16340)
- [Async JS Callbacks](http://sporto.github.io/blog/2012/12/09/callbacks-listeners-promises/)
- [SitePoint: Intro to jQuery Shorthand AJAX Methods](http://www.sitepoint.com/introduction-jquery-shorthand-ajax-methods/)

---

### Project Feedback + Evaluation

Students will fork the "feedr" application and commit their code as they
complete pieces of functionality.

The instructional team will grade each technical requirement and provide a
numeric grade on a scale.

- __Technical Requirements__: Did you deliver a project that met all the
  technical requirements? Given what the class has covered so far, did you build
  something that was reasonably complex?
- __Creativity__: Did you added a personal spin or creative element into your
  project submission? Did you deliver something of value to the end user (not
  just a hello world response)?
- __Code Quality__: Did you follow code style guidance and best practices
  covered in class, such as spacing, modularity, and semantic naming? Did you
  comment your code as your instructors have in class?
- __Total__: Your instructors will give you a total score on your project
  between:

Score | Expectations
----- | ------------
**0 - 10** | _Does not meet expectations._
**11 - 20** | _Meets expectactions, good job!_
**21 - 30** | _Exceeds expectations, you wonderful creature, you!_

This will serve as a helpful overall gauge of whether you met the project goals, but __the more important scores are the individual ones__ above, which can help you identify where to focus your efforts for the next project!
