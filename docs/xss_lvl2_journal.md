# Level 2 XSS observations

The website is a message board. It has users sign in and post messages. There must be a database storing those messages. There appears to be HTML in the message spaces that are user input.

Found the hints by mistake looking through the dev tools. The third hint is the key. <img> ins JS retrieves and displays an image. Also, it's a void element so doesn't require a closing </img> tag. onerror is an event handler attribute that specifies JS to run when an error event occurs on the element. 