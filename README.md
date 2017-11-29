## 剪切板https://clipboardjs.com/
    <button class="copyBtn submit" data-clipboard-text={{code}}>复制券码</button>
     var clipboard = new Clipboard('.copyBtn');
    clipboard.on('success', function(e) {
        layer.hAlert("已复制好，可粘贴",1);
        e.clearSelection();
    });

    clipboard.on('error', function(e) {
        layer.hAlert("长按复制",1);
    });

clipboard.js
A modern approach to copy text to clipboard

No Flash. No frameworks. Just 3kb gzipped

 
Why

Copying text to the clipboard shouldn't be hard. It shouldn't require dozens of steps to configure or hundreds of KBs to load. But most of all, it shouldn't depend on Flash or any bloated framework.

That's why clipboard.js exists.

Install

You can get it on npm.

Copy to clipboard
npm install clipboard --save
Or if you're not into package management, just download a ZIP file.

Setup

First, include the script located on the dist folder or load it from a third-party CDN provider.

Copy to clipboard
<script src="dist/clipboard.min.js"></script>
Now, you need to instantiate it by passing a DOM selector, HTML element, or list of HTML elements.

Copy to clipboard
new Clipboard('.btn');
Internally, we need to fetch all elements that matches with your selector and attach event listeners for each one. But guess what? If you have hundreds of matches, this operation can consume a lot of memory.

For this reason we use event delegation which replaces multiple event listeners with just a single listener. After all, #perfmatters.

Usage

We're living a declarative renaissance, that's why we decided to take advantage of HTML5 data attributes for better usability.

Copy text from another element

A pretty common use case is to copy content from another element. You can do that by adding a data-clipboard-target attribute in your trigger element.

The value you include on this attribute needs to match another's element selector.


https://github.com/zenorocha/clipboard.js.git
Copy to clipboard
Copy to clipboard
<!-- Target -->
<input id="foo" value="https://github.com/zenorocha/clipboard.js.git">

<!-- Trigger -->
<button class="btn" data-clipboard-target="#foo">
    <img src="assets/clippy.svg" alt="Copy to clipboard">
</button>
Cut text from another element

Additionally, you can define a data-clipboard-action attribute to specify if you want to either copy or cut content.

If you omit this attribute, copy will be used by default.


Mussum ipsum cacilds, vidis litro abertis. Consetis adipiscings elitis. Pra lá , depois divoltis porris, paradis. Paisis, filhis, espiritis santis. Mé faiz elementum girarzis, nisi eros vermeio, in elementis mé pra quem é amistosis quis leo. Manduma pindureta quium dia nois paga.
Cut to clipboard
Copy to clipboard
<!-- Target -->
<textarea id="bar">Mussum ipsum cacilds...</textarea>

<!-- Trigger -->
<button class="btn" data-clipboard-action="cut" data-clipboard-target="#bar">
    Cut to clipboard
</button>
As you may expect, the cut action only works on <input> or <textarea> elements.

Copy text from attribute

Truth is, you don't even need another element to copy its content from. You can just include a data-clipboard-text attribute in your trigger element.

Copy to clipboard
Copy to clipboard
<!-- Trigger -->
<button class="btn" data-clipboard-text="Just because you can doesn't mean you should — clipboard.js">
    Copy to clipboard
</button>
Events

There are cases where you'd like to show some user feedback or capture what has been selected after a copy/cut operation.

That's why we fire custom events such as success and error for you to listen and implement your custom logic.

Copy to clipboard
var clipboard = new Clipboard('.btn');

clipboard.on('success', function(e) {
    console.info('Action:', e.action);
    console.info('Text:', e.text);
    console.info('Trigger:', e.trigger);

    e.clearSelection();
});

clipboard.on('error', function(e) {
    console.error('Action:', e.action);
    console.error('Trigger:', e.trigger);
});
For a live demonstration, just open your console :)

Tooltips

Each application has different design needs, that's why clipboard.js does not include any CSS or built-in tooltip solution.

The tooltips you see on this demo site were built using GitHub's Primer. You may want to check that out if you're looking for a similar look and feel.

Advanced Usage

If you don't want to modify your HTML, there's a pretty handy imperative API for you to use. All you need to do is declare a function, do your thing, and return a value.

For instance, if you want to dynamically set a target, you'll need to return a Node.

Copy to clipboard
new Clipboard('.btn', {
    target: function(trigger) {
        return trigger.nextElementSibling;
    }
});
If you want to dynamically set a text, you'll return a String.

Copy to clipboard
new Clipboard('.btn', {
    text: function(trigger) {
        return trigger.getAttribute('aria-label');
    }
});
For use in Bootstrap Modals or with any other library that changes the focus you'll want to set the focused element as the container value.

Copy to clipboard
new Clipboard('.btn', {
    container: document.getElementById('modal')
});
Also, if you are working with single page apps, you may want to manage the lifecycle of the DOM more precisely. Here's how you clean up the events and objects that we create.

Copy to clipboard
var clipboard = new Clipboard('.btn');
clipboard.destroy();
Browser Support

This library relies on both Selection and execCommand APIs. The first one is supported by all browsers while the second one is supported in the following browsers.

Chrome logo
Chrome 42+
 Edge logo
Edge 12+
 Firefox logo
Firefox 41+
 Internet Explorer logo
IE 9+
 Opera logo
Opera 29+
 Safari logo
Safari 10+
The good news is that clipboard.js gracefully degrades if you need to support older browsers. All you have to do is show a tooltip saying Copied! when success event is called and Press Ctrl+C to copy when error event is called because the text is already selected.

You can also check if clipboard.js is supported or not by running Clipboard.isSupported(), that way you can hide copy/cut buttons from the UI.

Bonus

A browser extension that adds a "copy to clipboard" button to every code block on GitHub, MDN, Gist, StackOverflow, StackExchange, npm, and even Medium.

Install for Chrome and Firefox.

Made with ♥ by Zeno Rocha under MIT license
Brought to you by Liferay
