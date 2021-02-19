# Creating JavaScript functions in Poshi

With the last two Poshi releases, I've been focused on building in more flexibility when using JavaScript functions within Poshi Script syntax. The reason for adding such functionality is that, inevitably, we run into limitations using WebDriver Selenium's built-in API. Solutions usually require some type of custom functionality that's only achievable via JavaScript. 

All of the JavaScript that we run in WebDriver is possible through the [JavascriptExecutor](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/JavascriptExecutor.html) class. When calling `executeScript(...)`, a String representing a JavaScript fragment, and arguments (that can be accessed through a variable array named `arguments` in the JavaScript fragment) are passed in as parameters. Various objects can also be returned through this method. For usage with Poshi, only Strings are allowed to be passed in, but a String of an XPath locator syntax will automatically be passed in as a [WebElement](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/WebElement.html) object and can be available in the JavaScript fragment as an [HTML element](https://www.w3schools.com/jsref/dom_obj_all.asp). 

## Throw an error if the condition is false 
  ```
  assertJavaScript(String javaScript, String message, String argument)
  ```
- Summary: This method will evaluate a JavaScript condition and throw an error if the condition is false. 
- Parameters: 
    - `javaScript` is a String representing a JavaScript snippet. This snippet must return a boolean. 
    - `message` is the error message that will be thrown if the condition is not met.
    - `argument` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[0]`

## Run the JavaScript snippet
  ```
  executeJavaScript(String javaScript, String argument1, String argument2)
  ```
- Summary: This method will run the JavaScript snippet. 
- Parameters: 
    - `javaScript` is a String representing a JavaScript snippet.
    - `argument1` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[0]`.
    - `argument2` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[1]`.
- Poshi Script function example: 
```
javascript
	function javaScriptDragAndDropToObject {
		var javaScript = '''
Simulate = {
	dragAndDrop: function (source, target) {
		const dispatchEvent = function (type, element) {
			const rect = element.getBoundingClientRect();
			const event = document.createEvent('customEvent');
			event.initEvent(type, true, true);
			event.relatedTarget = element;
			(event.clientX = rect.left + rect.width / 2),
				(event.clientY = rect.top + rect.height / 2),
				element.dispatchEvent(event);
			return Promise.resolve();
		};
		dispatchEvent('dragstart', source)
			.then(function () {
				dispatchEvent('dragover', target);
			})
			.then(function () {
				dispatchEvent('drop', target);
			})
			.then(function () {
				dispatchEvent('dragend', source);
			});
	}
};

Simulate.dragAndDrop(arguments[0], arguments[1]);
		''';

		selenium.executeJavaScript("${javaScript}", "${locator1}", "${locator2}");

		selenium.assertJavaScriptErrors();

		selenium.assertLiferayErrors();
	}
```
## Return a string from a snippet
```
getJavaScriptResult(String javaScript, String argument1, String argument2)`
```
- This method will evaluate the JavaScript snippet and return a string from that snippet. 
- Parameters: 
    - `javaScript` is a String representing a JavaScript snippet. This snippet must return a string. 
    - `argument1` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[0]`.
    - `argument2` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[1]`.
- This method returns a String. 

## Wait For a JavaScript condition to be met; an exception will be thrown
```
waitForJavaScript(String javaScript, String message, String argument)`
```
- This method will wait for a JavaScript condition to be met until it reaches the value set by [`timeout.explicit.wait`](https://github.com/liferay/liferay-portal/blob/master/modules/test/poshi-runner/poshi-properties.markdown#timeoutexplicitwait). Upon reaching the timeout, an exception will be thrown. 
- Parameters: 
    - `javaScript` is a String representing a JavaScript snippet. This snippet must return a boolean. 
    - `message` is the error message that will be thrown if the condition is not met.
    - `argument` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[0]`.
- Poshi Script function example: 
```
javascript
	function waitForLiferayEvent {
		var javascript = '''
			try {
				var eventValue = LFR_JS_EVENTS_LOG.getLastEvent("${eventName}").${attributeName};

				return eventValue.includes("${attributeValue}");
			}
			catch(err) {
				return false;
			}
		''';

		var message = '''Event "${eventName}" with attribute "${attributeName}" and value "${attributeValue}" not fired.''';

		selenium.waitForJavaScript("${javascript}", "${message}", "");
	}
```

## Wait For a JavaScript condition to be met; no exceptions will be thrown
```
waitForJavaScriptNoError(String javaScript, String message, String argument)`
```
- This method will wait for a JavaScript condition to be met until it reaches the value set by [`timeout.explicit.wait`](https://github.com/liferay/liferay-portal/blob/master/modules/test/poshi-runner/poshi-properties.markdown#timeoutexplicitwait). Upon reaching the timeout, no exceptions are thrown.
- Parameters: 
    - `javaScript` is a String representing a JavaScript snippet. This snippet must return a boolean. 
    - `message` is the error message that will be thrown if the condition is not met. May be blank, as this error is never thrown.
    - `argument` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[0]`.

## Mark JavaScript condition as a Poshi warning if condition is false
```
verifyJavaScript(String javaScript, String message, String argument)`
```
- **Summary**: This method will evaluate a JavaScript condition but will be marked as a Poshi warning if the condition is false. 
- **Parameters**: 
    - `javaScript` is a String representing a JavaScript snippet. This snippet must return a boolean. 
    - `message` is the error message that will be printed in the console log if the condition is not met. 
    - `argument` is a String that will be passed along to the JavaScript snippet. If the String is an XPath locator it will automatically be converted to a `WebElement` object if the WebElement is available in the DOM. Accessed in the JavaScript fragment as `arguments[0]`