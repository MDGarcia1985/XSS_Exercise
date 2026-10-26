noticed the frame#1 seems to be reactive to user inputs. If I enter frame#alert() the result is Image NaN (Not a Number)

If I enter the numbers directly from the URL it changes the image in the frame.

In game.js I found something interesting. I don't see that there's anything checking the source for the event success message. I wonder if I could break the game itself instead of injecting the DOM attack or if it ammounts to the same thing?

There's an event listener in game.js line 26 with two if statements. One checks the location.origin and the other checks event.origin. If event.origin is an AND logical operation of location.origin and event.data. It is basically saying that if location.origin and event.data equal "success" then userOpenedAlert equals true and the user has solved the level allowing them to continue to the next level.

```
window.addEventListener("message", function(event) {

  if (!window.location.origin) {
    window.location.origin = window.location.protocol + "//" 
        + window.location.hostname 
        + (window.location.port ? ':' + window.location.port: '');
  }

  if (event.origin == window.location.origin && event.data == "success") {
    userOpenedAlert = true;
    levelSolved();
    return;
  }
```

The parent var is userOpenedAlert = False

could I just change that to True?

yes... yes I can.

 
console.log({
    userOpenedAlert,
    nextControlsDisplay: getComputedStyle(
        document.getElementById("next-controls")
    ).display
)};
 
returns
userOpenedAlert: false, nextControls: ''
 
run
userOpenedAlert = true;
 
rerun the console.log and it now reads:
userOpenedAlert: true, nextControls: "none"
 
run
levelSolved();

for the challenge

objective: inject a script to pop up a javescript alert() in the app.

constraint: since you can't enter your payload anywhere in the application, you will have to manually edit the address in the URL bar

observations:

url: https://xss-game.appspot.com/level3/frame#1

entering "12" into the url after frame# produces an error, but not a runtime error. It tries to load image 12, but there is no image 12 for it to load.

looking through the documentation and figuring out what this is used for, what we are after here is some kind of executable on error. In this case, when the page loads, it executes "function" the function on the page is chooseTab(num). This constructs an html string '/static/level3/cloud" + num + ".jpg'

so if we enter something in place of "num" it will be injected into the html

what if we inject something like an event listener for keystrokes and then send that data off somewhere?

either way, the answer to the excercise is much like level 1&2

<img src='/static/level3/cloud1' onerror='alert(1);//.jpg' />

we use "//" in this case to keep the .jpg suffix out of out execution path.