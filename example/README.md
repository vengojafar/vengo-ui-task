# Example: Clinique
 - Single HTML file
 - Javascript and CSS in head (to avoid caching)

## Main Folders and Content

### assets
All of the image, video, and font assets for displaying on the webpage.
- Images can be in JPG, PNG, or GIF formats
- Videos **must** be in WEBM format

### js
Javascript libraries
- jquery-3.3.1.min.js - [JQuery](https://jquery.com/) (older version used when this file was created)
- jquery.keyboard.min.js - [JQuery keyboard](https://github.com/Mottie/Keyboard) for onscreen input
- sweetalert2.all.min.js - [SweetAlert2](https://sweetalert2.github.io/) for popup alerts

### css
CSS files utilized by JS libraries
- jquery-ui.min.css - used by [JQuery keyboard](https://github.com/Mottie/Keyboard)
- keyboard.min.css - used by [JQuery keyboard](https://github.com/Mottie/Keyboard)
- sweetalert2.min.css - used by [SweetAlert2](https://sweetalert2.github.io/)

## Walkthrough: [`index.html`](https://github.com/vengojafar/vengo-ui-task/blob/master/example/clinique/index.html)

### `<head>`

#### Links
- All JS and CSS are referenced from local folders
- Vengo machines can operate offline therefore using online CDN's are restricted

```html
<script src="js/jquery-3.3.1.min.js"></script>
<script src="js/sweetalert2.all.min.js"></script>
<link href="css/sweetalert2.min.css" rel="stylesheet">
<link href="css/jquery-ui.min.css" rel="stylesheet">
<script src="js/jquery.keyboard.min.js"></script>
<link href="css/keyboard.min.css" rel="stylesheet">
```

### `<script>`

#### Reset timer due to onscreen inactivity
```js
var resetTimer;
var DEFAULT_TIMEOUT = 60000 * 2;

resetTimer = setTimeout(function () { resetUI(); }, DEFAULT_TIMEOUT);
```

#### Click handler for most elements
```js
$(document).click(function(e) { ... });
```

#### Onscreen keyboard (linked to `<input>`)
```js
$('#inputEmail').keyboard({
	display: {
		'bksp': '\u2190',
		'accept': 'Enter',
		'default': 'ABC',
		'meta1': '.?123',
		'meta2': '#+=',
		'com': ".com",
		's': "\u21e7"
	},
	maxLength: 70,
	layout: 'custom',
	customLayout: {
		'default': [
			'q w e r t y u i o p {bksp}',
			'a s d f g h j k l',
			'{s} z x c v b n m @ . .com',
			'{meta1} _ - @gmail.com @yahoo.com @hotmail.com'
		],
		'shift': [
			'Q W E R T Y U I O P {bksp}',
			'A S D F G H J K L',
			'{s} Z X C V B N M @ . .com',
			'{meta1} _ - @gmail.com @yahoo.com @hotmail.com'
		],
		'meta1': [
			'1 2 3 4 5 6 7 8 9 0 {bksp}',
			'` | { } % ^ * / \'',
			'{meta2} $ & ~ # = + . {meta2}',
			'{default} {space} ! ? {default}'
		],
		'meta2': [
			'[ ] { } \u2039 \u203a ^ * " , {bksp}',
			'\\ | / < > $ \u00a3 \u00a5 \u2022',
			'{meta1} \u20ac & ~ # = + . {meta1}',
			'{default} {space} ! ? {default}'
		]
	},
	usePreview: false,
	preventPaste: true,
	autoAccept: true
});
```

#### Navigate between pages
- Assumption that `div` `id` starts with `page`
```js
function navigateToPage(to, from) {
	$("#page" + from).hide();
	$("#page" + to).show();
}
```

#### Check email for valid formatting
```js
function validateEmail(email) {
	var re = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
	//var re = /^([\w-]+(?:\.[\w-]+)*)@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$/i;
	return re.test(email);
}
```

#### Assemble JSON to be passed to Vengo app
```js
function assembleJson() { ... }
```
Example output:
```json
{
   "type": 0,
   "info": "jafar@vengolabs.com",
   "properties":
   {
      "email_address": "jafar@vengolabs.com",
      "opt_in": true,
      "timestamp": "2019-10-09T19:12:26.244Z",
      "survey_responses":
      [
         {
	    "survey_question_text": "Have you tried a Clinique product before?",
	    "survey_answer_text": "Yes"
	 },
	 {
	    "survey_question_text": "Where do you shop for skincare products?",
	    "survey_answer_text": "Sephora"
	 },
	 {
	    "survey_question_text": "Where do you shop for skincare products?",
	    "survey_answer_text": "Ulta"
	 }
      ]
   }
}
```

### `<style>`
#### Set SweetAlert font
```css
.swal2-popup {
    font-family: 'Segoe UI';
}
```

#### Fix keyboard to bottom of screen
```css
.ui-keyboard {
    font-size: 30px;
    text-align: center;
    background: rgba(0, 0, 0, .8);
    width: 100%;
    height: auto;
    left: 0;
    top: auto;
    bottom: 0px;
    position: fixed;
    white-space: nowrap;
    overflow-x: auto;
    padding-bottom: 20px;
}
```

#### Hide overflow
```css
body {
    background: url(assets/background.jpg) repeat center center fixed;
    background-size: cover;
    background-size: 100% 100%;
    margin: 0;
    overflow: hidden;
}
```

### `<body>`

#### Close button
- Allows user to go back to the standard Vengo UI
```html
<div class="closeButtonContainer">
   <button id="btnClose" class="buttonClose">Close</button>
</div>
```

#### Pages are `<div>`
- Naming convention: name[page#]
- All are hidden except `#page1`
```html
<div id="page1">...</div>
```
```html
<div id="page2" hidden>...</div>
```

#### Hidden checkboxes
- Used to record user selections
- Data contains question and answer text
```html
<div style="visibility: collapse;">
   <input type="checkbox" id="chkTried1" data-survey-answer-text="Yes" data-survey-question-text="Have you tried a Clinique product before?"/>
   <input type="checkbox" id="chkTried2" data-survey-answer-text="No" data-survey-question-text="Have you tried a Clinique product before?"/>
</div>
```
```html
<div style="visibility: collapse;">
   <input type="checkbox" id="chkShop1" data-survey-answer-text="Online" data-survey-question-text="Where do you shop for skincare products?" />
   <input type="checkbox" id="chkShop2" data-survey-answer-text="Sephora" data-survey-question-text="Where do you shop for skincare products?" />
   <input type="checkbox" id="chkShop3" data-survey-answer-text="Ulta" data-survey-question-text="Where do you shop for skincare products?" />
   <input type="checkbox" id="chkShop4" data-survey-answer-text="Department stores" data-survey-question-text="Where do you shop for skincare products?" />
   <input type="checkbox" id="chkShop5" data-survey-answer-text="Drug stores" data-survey-question-text="Where do you shop for skincare products?" />
</div>
```
