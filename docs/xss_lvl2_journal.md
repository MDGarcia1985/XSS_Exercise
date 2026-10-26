Google XSS security game

# level two

## objective 

Inject a script to pop up a javascript alert() in the application

## mission description

Web applications often keep user data in server-side and, increasingly, client-side databases and later display it to users. No matter where such user-controlled data comes from, it should be handled carefully.

This level shows how easily xss bugs can be introduced in complex apps.

## observations

The website is a message board. It has users sign in and post messages. There must be a database storing those messages. There appears to be HTML in the message spaces that are user input.

Found the hints by mistake looking through the dev tools. The third hint is the key. <img> in JS retrieves and displays an image. Also, it's a void element so doesn't require a closing </img> tag. onerror is an event handler attribute that specifies JS to run when an error event occurs on the element.

### index.html

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
 
    <!-- This is our database of messages -->
    <script src="/static/post-store.js"></script>
   
    <script>
      var defaultMessage = "Welcome!<br><br>This is your <i>personal</i>"
        + " stream. You can post anything you want here, especially "
        + "<span style='color: #f00ba7'>madness</span>.";
 
      var DB = new PostDB(defaultMessage);
 
      function displayPosts() {
        var containerEl = document.getElementById("post-container");
        containerEl.innerHTML = "";
 
        var posts = DB.getPosts();
        for (var i=0; i<posts.length; i++) {
          var html = '<table class="message"> <tr> <td valign=top> '
            + '<img src="/static/level2_icon.png"> </td> <td valign=top '
            + ' class="message-container"> <div class="shim"></div>';
 
          html += '<b>You</b>';
          html += '<span class="date">' + new Date(posts[i].date) + '</span>';
          html += "<blockquote>" + posts[i].message + "</blockquote";
          html += "</td></tr></table>"
          containerEl.innerHTML += html; 
        }
      }
 
      window.onload = function() { 
        document.getElementById('clear-form').onsubmit = function() {
          DB.clear(function() { displayPosts() });
          return false;
        }
 
        document.getElementById('post-form').onsubmit = function() {
          var message = document.getElementById('post-content').value;
          DB.save(message, function() { displayPosts() } );
          document.getElementById('post-content').value = "";
          return false;
        }
 
        displayPosts();
      }
 
    </script>
 
  </head>
 
  <body id="level2">
    <div id="header">
      <img src="/static/logos/level2.png" /> 
      <div>Chatter from across the Web.</div>
      <form action="?" id="clear-form">
        <input class="clear" type="submit" value="Clear all posts">
      </form>
    </div>
 
    <div id="post-container"></div>
 
    <table class="message">
      <tr>
        <td valign="top">
          <img src="/static/level2_icon.png">
        </td>
        <td class="message-container">
          <div class="shim"></div>
          <form action="?" id="post-form">
            <textarea id="post-content" name="content" rows="2"
              cols="50"></textarea>
            <input class="share" type="submit" value="Share status!">
            <input type="hidden" name="action" value="sign">
          </form>
        </td>
      </tr>
    </table>
 
  </body>
</html>
```

### level.py

```py
class MainPage(webapp.RequestHandler):
 
  def render_template(self, filename, context={}):
    path = os.path.join(os.path.dirname(__file__), filename)
    self.response.out.write(template.render(path, context))
 
  def get(self):
    self.render_template('index.html')
 
application = webapp.WSGIApplication([ ('.*', MainPage) ], debug=False)
```

### post-store.js

```javascript
/*
 * Objects to implement a client-side post database.
 */
 
function Post(message) { 
  this.message = message;
  this.date = (new Date()).getTime();
}
 
function PostDB(defaultMessage) {
  // Initial message to display to users
  this._defaultMessage = defaultMessage || "";
 
  this.setup = function() {
    var defaultPost = new Post(defaultMessage);
    window.localStorage["postDB"] = JSON.stringify({
      "posts" : [defaultPost]
    });
  }
 
  this.save = function(message, callback) {
    var newPost = new Post(message);
    var allPosts = this.getPosts();
    allPosts.push(newPost);
    window.localStorage["postDB"] = JSON.stringify({
      "posts" : allPosts
    });
 
    callback();
    return false;
  }
 
  this.clear = function(callback) {
    this.setup();
 
    callback();
    return false;
  }
 
  this.getPosts = function() {
    return JSON.parse(window.localStorage["postDB"]).posts;
  }
 
  if(!window.localStorage["postDB"]) { 
    this.setup();
  }
}
```

### Post data workflow
User submits message -> PostDB.save(message) -> Stores serialized message in localStorage ->
-> DB.getPosts() -> Retrieves stored messages -> posts[i].message -> Concatenated into an HTML string ->
-> containerEl.innerHTML += html -> Untrusted markup is parsed into DOM elements

## Source Code Analysis — Level 2

Further inspection revealed that the message board uses client-side persistence through `window.localStorage["postDB"]`.

The `PostDB.save()` function serializes submitted messages using `JSON.stringify()` and saves them under the `postDB` key.

The rendering function retrieves the posts through `DB.getPosts()` and concatenates each `posts[i].message` directly into an HTML string:

```javascript
html += "<blockquote>" + posts[i].message + "</blockquote";
containerEl.innerHTML += html;
```

The vulnerability occurs at `containerEl.innerHTML += html`, where the browser interprets the user-controlled message as HTML rather than plain text.

The test payload was:

```html
<img src="bad" onerror="alert('test')">
```

The invalid image source produces an error event, which executes the JavaScript contained in the `onerror` attribute.

This demonstrates how persistent user-controlled data can become executable code when passed into an unsafe DOM rendering operation.

The messages persist in browser-local storage; the provided source does not demonstrate server-side storage or sharing between users.

## Results

Upon submitting the payload, the browser attempted to load the invalid image. The resulting error event executed the onerror handler, displaying the JavaScript alert. This confirmed that the stored message was being interpreted as HTML rather than plain text.