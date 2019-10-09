# Task: Califia Farms
Create a single page HTML file "UI" similar to the [example](https://github.com/vengojafar/vengo-ui-task/tree/master/example).
The user should be able to click through the screens and submit data.
JSON info should be printed to the console

## User Journey

### Start Screen
- Tap anywhere on the screen to progress to the second page

![](https://github.com/vengojafar/vengo-ui-task/blob/master/task/califia_farms/CalifiaFarms_1.png)

### Survey Question #1
- At least one selection should be made before user can progress.
- Either hide the next button or display an error using sweetalert

![](https://github.com/vengojafar/vengo-ui-task/blob/master/task/califia_farms/CalifiaFarms_2.png)

### Survey Question #2
- At least one selection should be made before user can progress.
- Either hide the next button or display an error using sweetalert

![](https://github.com/vengojafar/vengo-ui-task/blob/master/task/califia_farms/CalifiaFarms_3.png)

### Data Input
- First and Last Name input fields should have a different keyboard than Email (see boilderplate code below)
- Elements may need to be shifted up to accommodate keyboard

![](https://github.com/vengojafar/vengo-ui-task/blob/master/task/califia_farms/CalifiaFarms_4.png)

### Confirmation Screen
![](https://github.com/vengojafar/vengo-ui-task/blob/master/task/califia_farms/CalifiaFarms_5.png)


## Notes
- Background image file included (if needed)
- Gotham font included (if needed)


## Boilerplate Code

### Generic keyboard

```js
$('#input-firstname, #input-lastname').keyboard({
	display: {
		'bksp': "\u2190",
		'accept': 'Enter',
		'default': 'ABC',
		'meta1': '.?123',
		'meta2': '#+=',
		's': "\u21e7"
	},
	layout: 'custom',
	customLayout: {
		'default': [
			'q w e r t y u i o p {bksp}',
			'a s d f g h j k l',
			'{s} z x c v b n m , . {s}',
			'{meta1} {space} {meta1}'
		],
		'shift': [
			'Q W E R T Y U I O P {bksp}',
			'A S D F G H J K L',
			'{s} Z X C V B N M ! ? {s}',
			'{meta1} {space} {meta1}'
		],
		'meta1': [
			'1 2 3 4 5 6 7 8 9 0 {bksp}',
			'- / : ; ( ) \u20ac & @',
			'{meta2} . , ? ! \' " {meta2}',
			'{default} {space} {default}'
		],
		'meta2': [
			'[ ] { } # % ^ * + = {bksp}',
			'_ \\ | ~ < > $ \u00a3 \u00a5',
			'{meta1} . , ? ! \' " {meta1}',
			'{default} {space} {default}'
		]
	},
	usePreview: false,
	preventPaste: true,
	autoAccept: true
});
```


### Email keyboard
```js
$('#input-email').keyboard({
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
