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

#### Computed  vs method, watcher
```html
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

```
| Computed   | method
|--------------|-------|
| {{ convertToUpper }}|  {{ convertToUpper() }} | 
| không thể nhận tham số đầu vào    |  | 
| chỉ nên dùng với các dữ liệu có sẵn trong data của component   |  | 
| được cached, chỉ tính toán lại mỗi khi các biến phụ thuộc trong nó thay đổi|   tính toán bất kì khi nào nó được gọi | 

- Getter and setter
```js
var app = new Vue({
    el: '#app',
    data: {
        name: 'Vu Thanh Tai'
    },
    computed : {
        convertToUpper: {
            get : function () {
                return this.name.toUpperCase();
            },
            set: function (name) {
                this.name = name;
            }
        }
    }
});

//thiết lập lại giá trị
app.convertToUpper = "Hoc Lap Trinh Online Toidicode.com";
```
- Watcher: theo dõi sự thay đổi của dữ liệu và thực thi hành động kèm theo
  - tên của watcher phải trùng với tên của data cần theo dõi.
  - Và các watcher phải được đặt trong watch scope.
```js
var app = new Vue({
    el: '#app',
    data: {
        firstName: 'Vu Thanh',
        lastName: 'Tai',
        fullName: 'Vu Thanh Tai',
    },
    watch: {
        firstName : function (val) {
           this.fullName = val + ' ' + this.lastName;
       },
       lastName : function (val) {
           this.fullName = this.firstName + ' ' + val;
       }
   }
});
```
