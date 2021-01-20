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
#### Truyền dữ liệu giữa các components
1) Parent component -> child component
- Sử dụng props
```html
<template>
  <div id="app">
    <ComponentFirst msg="Welcome to Your Vue.js App"/>
    //OR <ComponentFirst :msg="Welcome to Your Vue.js App">
    //OR <ComponentFirst v-bind:msg="Welcome to Your Vue.js App"></ComponentFirst>
  </div>
</template>

<script>
import ComponentFirst from './components/componentFirst';

export default {
  name: 'App',
  components: {
    ComponentFirst
  }
}
</script>
```

```html
<template>
    <div>{{msg}}</div>
</template>

<script>
export default {
    name: "Component first",
    props: {
        msg: String
    }
};
</script>
```
- props chỉ được truyền một chiều từ cha xuống con – không có chiều ngược lại
 - Vì thằng cha có thể cũng truyền data này cho nhiều thằng con nữa, mà một thằng con lại có quyền thay đổi data của cha thì không được
 
 2. child component -> parent component
 - Sử dụng $emit()
 ```html
<template>
    <div id="app">
        <ComponentFirst @inputData="updateMessage"/>
        <h3>{{message}}</h3>
    </div>
</template>

<script>
import ComponentFirst from './components/componentFirst';

export default {
    name: 'App',
    components: {
        ComponentFirst
    },
    data() {
        return {
            message: 'Message default.'
        }
    },
    methods: {
        updateMessage(mes) {
            this.message = mes;
        }
    }
}
</script>
```
 ```html
<template>
    <div>
        <input
            placeholder="Enter Text Here"
            v-model="tempMessage"
        />
        <div>
            <button @click="sendMessage">@Emit event</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "ComponentFirst",
    data() {
        return {
            tempMessage: ''
        }
    },
    methods: {
        sendMessage() {
            this.$emit('inputData', this.tempMessage);
            this.tempMessage = '';
        }
    }
};
</script>
```
3. Event Bus
4. Vuex
### Component
#### [a component’s data option must be a function](https://vuejs.org/v2/guide/components.html#data-Must-Be-a-Function)
- each time you use a component, a new instance of it is created
```js
// Define a new component called button-counter
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```
```html
<div id="components-demo">
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
</div>
```
# Nuxt js
### Plugin

 
