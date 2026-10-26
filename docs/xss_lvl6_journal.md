Google XSS security game

# level six

## Objective

Find a way to make the application request an external file which will cause it to execute an alert().

## Mission Description

Complex web applications sometimes have the capability to dynamically load JavaScript libraries based on the value of their URL parameters or part of location.hash.

This is very tricky to get right -- allowing user input to influence the URL when loading scripts or other potentially dangerous types of data such as XMLHttpRequest often leads to serious vulnerabilities.

## Observations

URL: https://xss-game.appspot.com/level6/frame#/static/gadget.js

Error message: Couldn't load gadget from /static/gadget.js

### gadget.js

```javascript
/* This is a completely awesome invisible gadget */
```

### index.html

```html
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
 
    <script>
    function setInnerText(element, value) {
      if (element.innerText) {
        element.innerText = value;
      } else {
        element.textContent = value;
      }
    }
 
    function includeGadget(url) {
      var scriptEl = document.createElement('script');
 
      // This will totally prevent us from loading evil URLs!
      if (url.match(/^https?:\/\//)) {
        setInnerText(document.getElementById("log"),
          "Sorry, cannot load a URL containing \"http\".");
        return;
      }
 
      // Load this awesome gadget
      scriptEl.src = url;
 
      // Show log messages
      scriptEl.onload = function() { 
        setInnerText(document.getElementById("log"),  
          "Loaded gadget from " + url);
      }
      scriptEl.onerror = function() { 
        setInnerText(document.getElementById("log"),  
          "Couldn't load gadget from " + url);
      }
 
      document.head.appendChild(scriptEl);
    }
 
    // Take the value after # and use it as the gadget filename.
    function getGadgetName() { 
      return window.location.hash.substr(1) || "/static/gadget.js";
    }
 
    includeGadget(getGadgetName());
 
    // Extra code so that we can communicate with the parent page
    window.addEventListener("message", function(event){
      if (event.source == parent) {
        includeGadget(getGadgetName());
      }
    }, false);
 
    </script>
  </head>
 
  <body id="level6">
    <img src="/static/logos/level6.png">
    <img id="cube" src="/static/level6_cube.png">
    <div id="log">Loading gadget...</div>
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
 
application = webapp.WSGIApplication([ ('.*', MainPage), ], debug=False)
```

The game attemps to block external scripts by checking the textual URL prefic rather than validationg the browser-resolved destination's origin.

In previous levels you would see something like 

```
window.location.origin
```
## Test

I created a page at xss_excersize/executable_payload/payload.js and published the page as a static page on github.

### payload.js

```javascript
alert(1);
``` 

## Results

```html
<!doctype html>
<html>
  <head>
    <title>Success!</title>
    <link type="text/css" rel="stylesheet" href="/static/game.css" />
    <script src="/static/game.js"></script>


  </head>
  <body id=game-done>
    <h1 id="level-title">Congratulations!</h1>

    <div id="instructions">
    <pre>
                                                         -oooo:-                                                        
                                                        omhsoosho`                                                      
                                                        Ndo:``:oh-                                                      
                                                        dms+--+ym:                                                      
                                                        -ymhohdh+`                                                      
                                                         `N/`.s.                                                        
                                                          +:  +                                                         
                                                          --  :                                                         
                                                          --  o                                                         
                                                          ..  +                                                         
                                                          ::  s        ..`                                              
                                                .:sssso.  --  +     :syhhyo`                                            
                                ..::::.       `odhhyyhdd. ::  s    .mhhyhhdh.       -:...`                              
                               /dhhhhhhs     .odddhyhdddh+y:  my-syhdhhyhhddy/`   .odhyyhh:                             
                              yNdhyyoyhmo+::+ms/+++//++/odm:  NNmNd+///+++/+ody::omhyssyhdm-                            
                            -sddyyyyyyyoommmmmmdhyyyyyyhddd: `ddmdmdhyssyyhhmmNNNNdhyyyyyhmo-`                          
                        ``-omdyyyssys///shdddddddddmmdddhyy-``yhddddhhhhhdmmmmmmdd/oyssyyyyhmhss-`                      
                     `:ohhdmddhhyyyyyshddddhhyyyyyhddhhyo:-...--shhyysssyyhhdhhhddyyysyyyhdddmNNmyo.                    
                    /hNNmmd/:o+/////:`/osyhhyyys+syyhhyysysooossyyyyyooyyyyyyysyy+./oooooos/:ydNNmNmo.                  
                   +dNmmmmmhoo+///////oossshhyyyyyyyyssoossoosoosssyyyyyyyhsoyyyys/:-..--:/+sdddmmmNMy                  
                  `hNmmdmmdmddddhhhyhysso+.oyssssso-./o:-/+oo++oo--osoooooo..oyyhyyyyyyhhhyhdddmmdmNNN                  
                  `yNmNNhhdmdddhhhyyyyyyys:-......`./+++/:o++oo++/-````..::/+sysysyyyhsshhhydddmmmNNNN                  
                   sMNNNNNNmmdmdhhhhyyyyyyhhssssoo+oo/+//:/+//+:++++ooosyooyssosyyhhyhsshdhdmmNmNmmMMN                  
                   -NNNNNNhmNmdmmmdddddmhhhyyyyssys///+/:://////o+osoo+osoossosyhhdddh+omddmNNmmNmNMMN                  
                   oMNNNNNNNNdydNmmmmmdhydhhsoooodhydhsshys+soyooooosssyhyhymdhdhyddmmmdmNNNNNNmNNNMMM                  
                   yMMNNNMmmNdmmNNNNNNmh/sysyysyhyddmhhyhyhhddyyyhmddhhdmdddmmmdmmmmNNmmmNmNNNNmMNMMMM                  
                  .dMMNNMMNNNmNNNNNNmmNNhsddddNNdmhdmddyyhdhdhdddhdmhhdddhmddmmmNNNNNNNNNNNNNNNNMNMMMM                  
                  :NMMMNMMNMNhhmNNNNmdmNNmhddmdNmmmmmmddddNmdhdhddddmddmmmmmmNdNmdmmNNNmNNNNNdmMMMMMMM                  
                  -mMMMMMNNmNNmNNNNNNNNNNNdmmNmNmNmNmmNNmmNNdhddmmmmNmhhhyohNMNMNmmmmNdmNNMMMNNMMMMMMM                  
                  .dMMMMMMNNNMMMMMNNNNNMNmmmNNNmmmmNNdddmmNNNmmdNNmNNNmmNNNNNNNNNNNNNNNmNNNNNmNMMMMMMM                  
                  :NMMMMMMMMMMMMMMMNmmNMNNNNNNNmmNmNNNNmdmNNNNNNNmNNdmNNMMNMmNNNNNNMMNdmNNNMNmmMMMMMMM                  
                  :NNMMMMMMMMMMMMMMMMNNMNNMNNNMMMNNNNNNmNmdmmmNNNNNNmmNNNNNNNNNNMNNMMMNNNNMMNmMMMMNNMN                  
                  :NMMMNNMMMMMMMMMMMMMNNMMMMNMMMNmNNMNNNNNmhNMNNMNNNMMNMMMMMNNMMNNNMNMMMMNMMNNMMNMNMMM                  
                  `hMMMNdMNNMNNNNNMMNNNNMMMMMMMMNmNMMMMNNNNNNNdmmmMNMMMMMMNNMMNmdNMMNMNNNNMNmmNMNMMMMN                  
                   yMMMMNMMNMNmmNNNMNmddmMMNNNMNNNNNMMNNNNMNNNNNNNmNNNNNNNNNNNNNddNdmdmmNNMNNdMMMMMMMN                  
                   yMMMMNMNMMNNMMNNNNmdmmNMNNdhmMNNNNNNmNMMddddmNNNmNNMMNmNmmmmmNNmmmmNMMMMMMNNNMMMMMN                  
                   yNNNMMNNMMMMMMNNNNNMmmdNNNNNNNNNNNNmNNNNNmNmmNNNNNNNNNNNmNmNNNNNNNNNNNNNMMMNNMMMMMy                  
                   +MMMMMMMMMMMNNNNMMMNNNNmNNNMNMNNMNNmhdNNNNNmNNNmmNNNNNNNNNNNMMNNmNNNNNMNMNMMMMMMMN:                  
                    NMMMMNMMMMMMMNNNNNNdNMNNNNNNmNNNNNNNNNmmhNNNNmdNNNNNNNNNMMNNMNNNNNNNNNMMMMNNMMMNs`                  
                    -sdmNMNNMMMMMNNNNmmmmNNNMNmNMNNNNNNNMNmNNNNNNmmmdmNNNMNmmmmNMNNMNMmmNNMMMNMNmd+-`                   
                      `.ohNNMMNMMNMNNmdmNNNNNNmNMNNMNNNNmNNNmmmNmNMMNNMNNMMNNNNNNNNNNMMMMMMMNNho.`                      
                          :+hdNNNNNNNNNNNNNNmNNNNNNNMNNNmNNNNmMmmmNNNMNNNNNNNNMNNMMMMMNNmdds/-                          
                             `--:+shddmmNmmmmNNNNMNNNMNNNNNNNNNNMMNMMMNNNmNNNMNNNNdh++/-.`                              
                                     `--++osdddddddysNmmhshmmmmmNmddddddho/:++/---                                      
                                                    `-.-. .------.                                 

    </pre>

    <br>  
    You have successfully completed the game!

    <div class=question id=question-1>
      How did you like the game overall?<br>
      <input type=button value="It was awful" onclick="sendFeedbackResponse(1,1)">
      <input type=button value="Meh" onclick="sendFeedbackResponse(1,2)">
      <input type=button value="Alright, I suppose" onclick="sendFeedbackResponse(1,3)">
      <input type=button value="I loved it!" onclick="sendFeedbackResponse(1,4)">
    </div>

    <div class=question id=question-2>
      How about the difficulty?<br>
      <input type=button value="Too easy" onclick="sendFeedbackResponse(2,3)">
      <input type=button value="Just right" onclick="sendFeedbackResponse(2,2)">
      <input type=button value="Too hard" onclick="sendFeedbackResponse(2,1)">
    </div>

    While breaking things is fun, it is also important to know how
    to prevent XSS. For a gentle introduction to the topic of XSS,
    take a look at our <a href="//www.google.com/about/appsecurity/learning/xss/index.html">documentation</a>.
    
    <br><br>
    Thanks for playing!
    </div>



  </body>
</html>
```