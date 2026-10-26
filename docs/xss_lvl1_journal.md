# FourOrFour

## XSS Level 1 — Reflected Cross-Site Scripting

**Platform:** Google XSS Game  
**Target:** https://xss-game.appspot.com/level1/frame  
**Exercise:** Level 1  
**Status:** HTML injection demonstrated; JavaScript execution not yet documented as successful.

---

## 1. Journal Entry

### Goal

Inject JavaScript through the search interface to execute an `alert()` function within the challenge frame.

Secondary research objectives:

- Understand how the search query is transmitted and processed.
- Identify where untrusted input enters the HTML document.
- Investigate whether the browser interprets injected HTML.
- Examine the relationship between the challenge iframe and its parent page.
- Understand how the game detects successful XSS execution.
- Investigate unexpected cached search values.
- Trace the sequence of events from search submission to browser rendering.

### Initial Observation

**Initial URL:**  
https://xss-game.appspot.com/level1/frame

The application contains a non-interactive header using purple and green colors, with a page title.

Below the header is a search field and a button labeled "Search."

When selecting the search field, a previously entered value appears as a suggestion.

**Observed cached entry:**

`as02832mr-2-r`

Submitting that value produces the following message:

> Sorry, no results were found for as02832mr-2-r. Try again.

**URL after search:**

`https://xss-game.appspot.com/level1/frame?query=as02832mr-2-r`

### Initial Hypothesis

The search field submits a value using an HTTP GET request.

Because the entered search term appears in the returned page, the `query` parameter may provide an injection point.

**Research question:** Can a custom HTML element or JavaScript expression be submitted through the `query` parameter and interpreted by the browser when the server returns the search results?

---

## 2. Inspecting the Source Code

### Initial Findings

The HTML form uses the `GET` method.

The Python application uses `webapp.RequestHandler` to process requests.

The `MainPage` class provides a `render_string()` method that writes a string directly to the HTTP response.

The `get()` method retrieves the `query` parameter and uses it to construct an HTML response.

The application explicitly disables the legacy reflected-XSS browser filter using the `X-XSS-Protection` header.

### Source Code

```python
page_header = """
<!doctype html>
<html>
  <head>
    <!-- Internal game scripts/styles, mostly boring stuff -->
    <script src="/static/game-frame.js"></script>
    <link rel="stylesheet" href="/static/game-frame-styles.css" />
  </head>

  <body id="level1">
    <img src="/static/logos/level1.png">
      <div>
"""

page_footer = """
    </div>
  </body>
</html>
"""

main_page_markup = """
<form action="" method="GET">
  <input id="query" name="query" value="Enter query here..."
    onfocus="this.value=''">
  <input id="button" type="submit" value="Search">
</form>
"""

class MainPage(webapp.RequestHandler):

  def render_string(self, s):
    self.response.out.write(s)

  def get(self):
    # Disable the reflected XSS filter for demonstration purposes
    self.response.headers.add_header("X-XSS-Protection", "0")

    if not self.request.get('query'):
      # Show main search page
      self.render_string(page_header + main_page_markup + page_footer)
    else:
      query = self.request.get('query', '[empty]')

      # Our search engine broke, we found no results :-(
      message = "Sorry, no results were found for <b>" + query + "</b>."
      message += " <a href='?'>Try again</a>."

      # Display the results page
      self.render_string(page_header + message + page_footer)

    return

application = webapp.WSGIApplication([ ('.*', MainPage), ], debug=False)
```

### Vulnerability Analysis

The critical statement is:

```python
message = "Sorry, no results were found for <b>" + query + "</b>."
```

The application concatenates the user-controlled `query` parameter directly into an HTML string.

No HTML escaping or sanitization is performed before writing the response.

This creates a potential reflected cross-site scripting vulnerability.

The application assumes that `query` contains ordinary text, but the browser may interpret HTML markup within the returned response.

### Escaped versus Unescaped HTML

An unescaped HTML element:

```html
<b>Hello World</b>
```

Is rendered as bold text by the browser.

An escaped equivalent:

```html
&lt;b&gt;Hello World&lt;/b&gt;
```

Is displayed as the literal characters:

`<b>Hello World</b>`

Common HTML character references:

| Character | HTML Escape |
|---|---|
| `<` | `&lt;` |
| `>` | `&gt;` |
| `&` | `&amp;` |
| `"` | `&quot;` |
| `'` | `&#39;` |

**Finding:** The search handler does not apply context-appropriate HTML escaping before placing the query into the document.

### X-XSS-Protection Header

The application explicitly sets:

```python
self.response.headers.add_header("X-XSS-Protection", "0")
```

This disables a legacy browser XSS filter.

It does not itself create the vulnerability. The underlying issue is the unsafe handling of user-controlled input.

Modern browsers generally do not rely on this obsolete protection mechanism.

---

## 3. Test 1 — HTML Embedding

### Hypothesis

If the server returns the search parameter without HTML escaping, submitting an HTML element may cause the browser to create that element.

Rather than immediately attempting JavaScript execution, an embedded external website can be used to investigate whether the browser interprets the supplied markup.

### Test Input

```html
<embed src="https://www.mandedesign.studio">
```

### Expected Result

If the browser interprets the HTML markup, it should attempt to create an embedded browsing context and load the specified website.

The destination's own security policies may prevent the website from being displayed.

### Actual Result

The search results attempted to embed `www.mandedesign.studio`.

The browser displayed a refusal-to-connect message inside the embedded area instead of the website.

The screenshot showed an embedded region with an error message.

### Initial Interpretation

I initially suspected that the external website might not respond because it uses HTTPS.

Further investigation showed that HTTPS is not inherently the cause of this failure.

The destination website may restrict embedding through:

- `X-Frame-Options`
- Content Security Policy `frame-ancestors`
- Other application or browser restrictions

The screenshot supports the conclusion that the browser interpreted the injected HTML element and attempted to load an external resource.

### Conclusion

**HTML injection: Demonstrated.**

The query parameter is reflected into the HTML response, and the browser interprets the submitted markup.

However, this test does not independently demonstrate JavaScript execution.

---

## 4. Test 2 — External Website as an Injection Mechanism

### Research Question

If the embedded website were specifically configured to accept cross-origin embedding and communication, could it return JavaScript or information to the host page?

### Hypothesis

An attacker-controlled or researcher-controlled website could be configured to permit embedding.

For example:

```html
<iframe src="https://lab.example.com/embed-test.html"></iframe>
```

If the destination allows embedding, the browser may display it inside the host document.

However, this does not automatically grant the embedded document access to its parent's JavaScript context.

### Same-Origin Policy

Browsers restrict interaction between documents from different origins.

An origin is defined by the combination of:

- Scheme
- Hostname
- Port

For this investigation:

**Challenge origin:**

`https://xss-game.appspot.com`

**External website origin:**

`https://www.mandedesign.studio`

These are different origins.

The Same-Origin Policy normally prevents JavaScript running in the embedded website from directly reading or modifying the challenge document.

### JavaScript Context

An embedded document may access its own DOM.

A cross-origin embedded document generally cannot directly access the parent's DOM.

For example:

```javascript
window.parent.document.body
```

This access would normally be prohibited when the parent and child have different origins.

### Conclusion

Embedding a page and executing JavaScript within that page does not inherently execute JavaScript in the parent's origin.

Communication across this boundary requires an authorized mechanism, such as `postMessage()`, or an additional vulnerability.

---

## 5. Cross-Origin Communication

### Research Question

Can an embedded page communicate with its parent document and return information that the parent might incorrectly accept as trusted?

### Discovery

Browsers provide a built-in cross-origin communication interface:

```javascript
window.postMessage()
```

A child browsing context can send a message to its parent without obtaining direct access to the parent's DOM.

Example:

```javascript
parent.postMessage("test-message", "*");
```

The second argument defines the permitted destination origin.

The wildcard `"*"` permits delivery without requiring a specific destination origin.

It does not disable the Same-Origin Policy.

### Receiving Messages

A parent document can receive messages using an event listener:

```javascript
window.addEventListener("message", function(event) {
  console.log(event.origin);
  console.log(event.source);
  console.log(event.data);
});
```

Relevant message properties:

| Property | Description |
|---|---|
| `event.origin` | Origin of the sending document when the message was sent |
| `event.source` | Reference to the sending browsing context |
| `event.data` | Message contents |

### Trust Boundary

A message is not automatically trustworthy because it was delivered through the browser's messaging interface.

A vulnerable receiving application might accept data without properly validating the sender.

Potential implementation errors include:

- Failing to validate `event.origin`.
- Failing to validate `event.source`.
- Treating message data as trusted HTML.
- Passing untrusted message data into dynamic code execution.

### Conclusion

Cross-origin communication is possible by design.

Whether it creates a vulnerability depends on the receiving application's validation and handling of messages.

---

## 6. Discovery — game-frame.js

### Observation

The original HTML includes an external JavaScript resource:

```html
<script src="/static/game-frame.js"></script>
```

Inspection of that script revealed how the challenge frame communicates with its parent.

### Discovered Source Code

```javascript
/* If we're being iframed, let the parent know our URL */
/* Kids: don't do this at home! */
parent.postMessage(window.location.toString(), "*");

/* Override window.alert */
var originalAlert = window.alert;
window.alert = function(s) {
  parent.postMessage("success", "*");
  setTimeout(function() {
    originalAlert("Congratulations, you executed an alert:\n\n"
      + s + "\n\nYou can now advance to the next level.");
  }, 50);
}
```

### Analysis — Initial Message

```javascript
parent.postMessage(window.location.toString(), "*");
```

This sends the current frame URL to the parent browsing context.

`window.location.toString()` includes the URL's query string.

The message is transmitted when this script executes, rather than specifically when the search form is submitted.

### Analysis — Alert Override

```javascript
var originalAlert = window.alert;
```

This stores a reference to the original browser alert function.

Next:

```javascript
window.alert = function(s) {
```

The application replaces `window.alert` with a custom function.

This technique is known as *monkey patching*.

When the overridden function is called, it performs:

```javascript
parent.postMessage("success", "*");
```

The game sends a success signal to its parent document.

The function then schedules the original alert using:

```javascript
setTimeout(function() {
  originalAlert("Congratulations, you executed an alert:\n\n"
    + s + "\n\nYou can now advance to the next level.");
}, 50);
```

The 50-millisecond delay defers the display of the original alert.

It does not guarantee that the parent has already processed the message.

### Inferred Success Sequence

1. User submits a query containing executable JavaScript.
2. The server reflects that query into the HTML response.
3. The browser parses the returned HTML.
4. The injected JavaScript executes.
5. The JavaScript calls `window.alert()`.
6. The game's overridden function sends `"success"` to the parent.
7. The original alert function displays a congratulatory message.

**Important:** This is an inferred sequence based on the source code. Successful execution of the complete sequence has not yet been recorded in the journal.

### Implications for Message Spoofing

The script transmits the literal string:

```javascript
"success"
```

This value is not a cryptographic authentication mechanism.

In principle, another browsing context could send the same message.

Whether the parent accepts that message depends on how its message listener validates the sender and processes the contents.

The discovered code establishes the sender's behavior but does not reveal the parent's complete validation logic.

### Additional Research Question

Does the parent challenge page validate both the sender's origin and source before accepting the `"success"` message?

**Status:** Unresolved.

---

## 7. Parent Frame Message Handling and URL Validation

### Research Objective

Determine how the parent page processes messages received from embedded frames and whether an externally controlled frame could influence the game's behavior.

### Source Code Findings

The parent page uses a message event listener to process communications from other browsing contexts.

The listener validates the message origin only when the message contains `"success"`.

Other messages are passed to:

```javascript
updateURLBar('1', event.data);
```

The `updateURLBar()` function writes the received message into the URL input field:

```javascript
function updateURLBar(frameNum, value) {
  var urlbar = document.getElementById('input' + frameNum);
  urlbar.value = unescape(value);
}
```

### Observation

Messages that do not satisfy the success condition can modify the displayed URL input value without passing an origin or source validation check.

The assignment uses the input's `.value` property, which does not directly interpret the supplied data as executable HTML or JavaScript.

### Navigation Validation

The `updateFrame()` function performs several URL checks before permitting navigation, including protocol, hostname, pathname, and directory-traversal checks.

If validation succeeds, it performs:

```javascript
frame.src = url;
frame.contentWindow.postMessage(url, "*");
```

Changing the URL input field does not automatically invoke `updateFrame()`.

### Hypothesis

An embedded external page may be able to send a message that changes the URL displayed in the parent interface.

However, the current source code does not demonstrate that such a message can automatically navigate the frame or trigger the game's success condition.

### Potential Security Concern

The parent page applies different trust requirements to different incoming messages.

- Success messages require a matching origin but do not explicitly validate `event.source`.
- Other messages can reach `updateURLBar()` without an origin check.
- Navigation is subject to additional validation inside `updateFrame()`.

This suggests a potential client-side UI-spoofing weakness, separate from the reflected XSS vulnerability.

### Conclusion

**Status: Potential UI-spoofing weakness identified through source-code analysis. Not yet experimentally demonstrated.**

### Next Investigation

Identify all calls to `updateFrame()` and determine whether any can be triggered automatically following an untrusted message.

Test whether cross-origin messages can change the URL input field without affecting the actual iframe navigation.


---

## 8. JavaScript Execution Context

### Research Question

Can JavaScript submitted through the search field inspect information about the document in which it executes?

### Example Test

```html
<script>
  alert(window.location.origin);
</script>
```

If the browser executes the injected script, the alert should display the origin of the current document.

This would help distinguish JavaScript executing directly in the vulnerable frame from JavaScript executing inside a separately embedded website.

### Additional Diagnostic Example

```html
<script>
  console.log({
    origin: window.location.origin,
    url: window.location.href,
    title: document.title
  });
</script>
```

The output would appear in the browser's developer console.

### Relevant Distinctions

- JavaScript running directly in the vulnerable document operates in that document's execution context.
- JavaScript running inside a cross-origin iframe normally operates in the iframe's own origin.
- Modifying a document's DOM does not change the browser's actual security origin.
- Changing displayed content does not necessarily modify the original HTTP response.

### Status

These examples were discussed but their execution results have not yet been documented.

---

## 9. Investigation — Cached Search Entries

### Initial Observation

Clicking the search field presented an unexpected value:

`as02832mr-2-r`

The value appeared while testing in both Chrome and Brave.

Initially, I suspected that it might be an application clue, a remnant of a previous user's activity, or an intentionally planted value.

### Additional Observation

Subsequent search entries, including the `mandedesign.studio` test, also appeared as cached suggestions.

This establishes a pattern consistent with browser form-history functionality.

### Relevant HTML

```html
<form action="" method="GET">
  <input id="query" name="query" value="Enter query here..."
    onfocus="this.value=''">
  <input id="button" type="submit" value="Search">
</form>
```

The field has a stable identifier and name:

```html
id="query"
name="query"
```

These attributes allow the form to submit its value and may help the browser associate the input with previously entered values.

### Possible Sources

1. Browser autocomplete history.
2. Browser autofill.
3. Restored form state.
4. JavaScript assignment to the input value.
5. Browser profile synchronization or imported history.

The provided Python handler does not implement persistent search history.

### Diagnostic JavaScript

```javascript
const field = document.querySelector("#query");

console.log({
  currentValue: field.value,
  defaultValue: field.defaultValue,
  attributeValue: field.getAttribute("value"),
  autocomplete: field.autocomplete
});
```

This can help distinguish between the current field value, the default markup value, and browser-side suggestions.

### Interpretation

The observation that subsequent searches reappear as suggestions strengthens the form-history hypothesis.

Seeing the same unexpected value in Chrome and Brave does not definitively rule out browser-side history because profiles may have shared, synchronized, or imported data.

### Conclusion

**Browser form history is the leading hypothesis.**

The original value `as02832mr-2-r` remains unexplained.

No evidence currently establishes that it is a deliberate challenge clue or a value originating from another user.

---

## 10. Browser Event Chain Investigation

### Research Objective

Observe what happens behind the scenes when a user submits a query.

The investigation should distinguish:

1. User interaction events.
2. Browser form processing.
3. HTTP request generation.
4. Server-side request handling.
5. HTTP response generation.
6. HTML parsing and DOM construction.
7. JavaScript execution.
8. Cross-frame messaging.

### Expected Execution Sequence

```text
User enters search query
        |
        v
Browser processes input events
        |
        v
User submits the form
        |
        v
Browser creates an HTTP GET request
        |
        v
/level1/frame?query=...
        |
        v
Python MainPage.get()
        |
        v
Server constructs an HTML response
        |
        v
Browser receives the response
        |
        v
HTML parser constructs the DOM
        |
        v
JavaScript and embedded resources are processed
        |
        v
Game frame communicates with parent
```

### Network Inspection

Chrome DevTools provides a Network panel for observing HTTP traffic.

Proposed procedure:

1. Open DevTools.
2. Select the Network tab.
3. Enable **Preserve log**.
4. Select the **Doc** filter.
5. Submit a distinctive search value.
6. Locate the `/level1/frame?query=...` request.
7. Examine the request headers, query parameters, response HTML, and timing.

This allows comparison of the HTTP response against the document rendered by the browser.

### Browser Event Monitoring

The following JavaScript can be executed in the challenge frame's DevTools Console while the search form is present:

```javascript
const form = document.querySelector("form");
const input = document.querySelector("#query");

["focus", "input", "change", "keydown"].forEach(type => {
  input.addEventListener(type, event => {
    console.log("INPUT EVENT", {
      type: event.type,
      value: event.target.value,
      timestamp: performance.now()
    });
  });
});

form.addEventListener("submit", event => {
  console.log("FORM SUBMIT", {
    action: form.action,
    method: form.method,
    data: [...new FormData(form).entries()]
  });
});
```

This instrumentation records local browser events.

The event listeners will normally be destroyed when the frame navigates to a new document.

Enabling **Preserve log** in DevTools helps retain console messages across navigation.

### Event Listener Breakpoints

The DevTools Sources panel provides event listener breakpoints.

Relevant event types include:

- `submit`
- `keydown`
- `click`

These can pause client-side execution and permit examination of the JavaScript call stack.

They do not directly reveal execution inside the remote Python server.

### HTTP Response versus DOM

Two representations should be compared.

**Network Response:** The HTML returned by the server.

**Elements Panel:** The DOM created by the browser after interpreting the HTML.

This is especially important when investigating HTML injection because the server may transmit text that the browser subsequently interprets as executable markup.

---

## 11. Browser Automation Event

### Captured Event

The following event was recorded while interacting with the search field.

```json
{
  "type": "click",
  "assertedEvents": [
    {
      "type": "navigation",
      "url": "https://xss-game.appspot.com/level1",
      "title": "Title"
    }
  ],
  "timeout": 5000,
  "target": "main",
  "frame": [
    0
  ],
  "selectors": [
    [
      "aria/[role=\"form\"]",
      "aria/[role=\"textbox\"]"
    ],
    "#query",
    "xpath///*[@id=\"query\"]",
    "pierce/#query",
    "text/Enter query here..."
  ],
  "offsetX": 161.8125,
  "offsetY": 17.333328247070312,
  "duration": 50,
  "deviceType": "mouse",
  "button": "primary"
}
```

### Interpretation

This is a browser automation action describing a mouse click.

It is not an XSS payload, JavaScript source file, or HTTP response.

The automation identifies the search field using several selectors, including:

```text
#query
```

The `frame: [0]` field indicates that the automation targets a frame within the browser page.

It does not demonstrate that code can cross the security boundary between the frame and parent.

The `assertedEvents` entry identifies an expected navigation to the parent challenge URL, but the recording alone does not prove that the click caused that navigation.

### Conclusion

The captured event documents how browser automation locates and interacts with the search field.

It provides useful information about the browser's interaction layer but does not directly establish JavaScript execution or message spoofing.

---

## 12. Monitoring Cross-Frame Messages

### Research Objective

Observe communications received by the parent document from the challenge frame.

### Diagnostic Script

Run the following in the parent page's JavaScript execution context:

```javascript
window.addEventListener("message", event => {
  console.log("MESSAGE RECEIVED", {
    origin: event.origin,
    sourceIsChild: event.source ===
      document.querySelector("iframe")?.contentWindow,
    data: event.data
  });
});
```

This records messages received after the listener is installed.

The `sourceIsChild` comparison assumes the relevant challenge iframe is the first iframe returned by the selector.

For pages containing multiple frames, the correct iframe should be identified explicitly.

### Expected Observations

Based on the discovered `game-frame.js`, the parent may receive:

- A message containing the challenge frame's URL.
- A `"success"` message when the overridden `window.alert()` function executes.

These are source-code-supported expectations, not yet recorded test results.

### Next Investigation

Locate the parent page's message event handler.

Determine whether it validates:

- `event.origin`
- `event.source`
- `event.data`

Also determine what action the parent performs after receiving `"success"`.

---

## 13. Findings Summary

| Finding | Status |
|---|---|
| Search input uses HTTP GET | Confirmed from source |
| Query is reflected into HTML response | Confirmed |
| Query is not HTML-escaped | Confirmed from source |
| Browser interprets injected HTML | Demonstrated through embedding test |
| External website attempted to load | Observed |
| External website refused embedding | Observed |
| JavaScript can be injected through the query | Strongly supported; execution not yet documented |
| Challenge script overrides `window.alert()` | Confirmed from source |
| Challenge frame sends URL to parent | Confirmed from source |
| Alert override sends `"success"` to parent | Confirmed from source |
| Parent validates message origin and source | Unknown |
| Original cached query is a deliberate clue | Unsubstantiated |
| Browser form history stores search suggestions | Strong working hypothesis |

---

## 14. Unresolved Questions

### Q1. JavaScript Execution

Will a script submitted through the search field execute directly in the challenge frame and trigger the overridden alert?

### Q2. Parent Message Handler

How does the parent page receive and validate the `"success"` message?

Does it verify the origin and source of the sender?

### Q3. Cross-Origin Trust

Could a different embedded frame submit a message that appears equivalent to the challenge frame's success notification?

What validation mechanisms prevent this?

### Q4. Browser Form History

Why was `as02832mr-2-r` present before the documented experiments?

Does the value persist in a completely fresh browser profile?

### Q5. Browser Event Chain

What is the exact order of browser events, navigation, response processing, script execution, and parent-frame messaging when the query is submitted?

### Q6. Server Response versus Browser Interpretation

How does the server-returned HTML differ from the constructed DOM after submitting injected markup?

---

## 15. Next Experiments

### Experiment A — JavaScript Execution

Test whether the vulnerable page executes JavaScript supplied through the `query` parameter.

Record:

- Submitted input.
- Generated URL.
- Server response.
- Browser behavior.
- Console output.
- Whether the game's alert override was invoked.

### Experiment B — Parent Message Inspection

Inspect the parent page's scripts and observe messages received from the challenge frame.

Document validation of message origin, source, and contents.

### Experiment C — Form History Isolation

Repeat the search-field test in a fresh private browser session or clean browser profile.

Determine whether the previously observed value remains present.

### Experiment D — Network and DOM Comparison

Submit a controlled HTML element through the search field.

Compare the server response in the Network tab with the resulting DOM in the Elements panel.

---

## 16. Current Conclusion

The FourOrFour Level 1 challenge contains a reflected HTML injection vulnerability caused by concatenating an untrusted query parameter directly into an HTML response.

The initial `<embed>` experiment demonstrated that the browser interprets submitted HTML rather than displaying it exclusively as text.

Further examination revealed that the challenge's JavaScript overrides `window.alert()` and communicates with the parent page using `postMessage()`.

This establishes the expected relationship between successful JavaScript execution in the challenge frame and the game's completion mechanism.

The investigation also identified a separate potential area of interest: trust validation in cross-origin message handling.

**Current status:** Reflected HTML injection demonstrated. Alert-based JavaScript execution and parent-frame message validation remain to be experimentally documented.

---

## 17. References

- Google XSS Game, Level 1: https://xss-game.appspot.com/level1
- Challenge frame: https://xss-game.appspot.com/level1/frame
- Challenge JavaScript: https://xss-game.appspot.com/static/game-frame.js
- MDN — Cross-site scripting (XSS): https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS
- MDN — Same-origin policy: https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy
- MDN — Window.postMessage(): https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage
- OWASP — Cross Site Scripting Prevention Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
