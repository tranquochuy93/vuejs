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

#### Computed  vs method
```
<div id="app">
    <h1 class="text-red">{{ convertToUpper() }}</h1>
</div>
<script  type="text/javascript"></script>
<script type="text/javascript">
    var app = new Vue({
        el: '#app',
        data: {
            name: 'Vu Thanh Tai'
        },
        methods : {
            convertToUpper: function (){
                return this.name.toUpperCase();
            }
        },
	computed : {
        convertToUpper: function (){
            return this.name.toUpperCase();
        }
    }
    });
</script>
html
```
| Computed   | method
|--------------|-------|
| {{ convertToUpper }}|  {{ convertToUpper() }} | 
| không thể nhận tham số đầu vào    |  | 
| chỉ nên dùng với các dữ liệu có sẵn trong data của component   |  không thể có constructor. | 
| được cached, chỉ tính toán lại mỗi khi các biến phụ thuộc trong nó thay đổi|   tính toán bất kì khi nào nó được gọi | 
