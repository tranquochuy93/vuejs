# vuejs
#### this.$refs
- access the DOM element
- change properties of DOM element
```html
<button ref="myButton" @click="clickedButton">Click Me!</button>
```

```js
var vm = new Vue({
	el: '#app',
	data: {
		message: 'Hello World!'
	},
	methods: {
		clickedButton: function() {
			console.log(this.$refs);
			this.$refs.myButton.innerText = this.message;
		}
	}
});
```
