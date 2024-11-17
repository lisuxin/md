# Vue3

[toc]

## 基于vite创建vue3

### 创建

1. 步骤
   1. 进入项目终端
   2. `npm init vite@latest`：初始化项目
   3. `项目名称`：输入项目名称后回车
   4. 选择基于`vite`创建项目的名称
   5. 通过方向键选择顶目的编程语言，配置编程环境
   6. 安装默认依赖
   7. `cd 项目名称`切换到项目目录
   8. `npm install`：安装依赖
   9. `npm run dev`：启动项目
   10. `loca`：项目访问地址

### 创建常见异常处理

1. `ideaITree:npm: sill ideaITree buiIdDeps`：npm镜像问题更换镜像
   1. 更换：`pm config set registry 镜像地址`
   2. 查看：`npm config get registry`

### 项目结构

![](../typoratuxiang/JavaScript/vuexmjg.png)

1. `vue-boot3`：项目名称
2. `node_modules`：项目创建时的依赖
3. `public`：公共资源
4. `src`：工作区
   1. `assets`：静态资源、如图片等
   2. `components`：vue的组件
   3. `App.vue`：根组件
   4. `main.js`：全局配置文件
   5. `style.css`：样式文件
5. `.gitignore`：协同开发互联文件
6. `index.html`：项目首页入口
7. `package-lock.json`：固定模块的版本
8. `package.json`：导包、相当于`pom.xml`
9. `reanme.md`：项目说明文件
10. `vite.config.js`：vite的配置文件、可以做跨域用

### 组件调用

1. 删除不需要的文件

   1. `style.css`：样式文件

   2. `main.js`：中引入样式文件的代码

   3. `App.vue`根组件只保留结构

      ![image-20240715102135108](../typoratuxiang/JavaScript/zj.png)

      1. `script`：写行为动作
      2. `template`：写HTML、显示标签、在template中的标签必须包裹在一个根元素中
      3. `style`：写样式、`scoped`：该样式只对当前组件起作用

2. 在根组件中引入其他组件

   1. 在components文件夹下新建其他组件
   2. 在跟组件的script中引入`import HelloWorld from './components/HelloWorld.vue';`
      1. `import 引入组件名称 from '从根组件到引入组件地址';`

### 插值表达式

==插值表达式是一种将数据绑定到模板的方式，它使用双花括号`{{}}`来包裏==

例：

`<div>{{ mages }}</div>`

1. 导入函数：使用插值表达式必须导入到组件

   `import {ref,reactive} from 'vue';`

   1. 要想变量原始值发生改变必须是响应式数据`let deom = ref("asafa")`

   2. 定义方法

      ```js
      const 方法名=() =>{
          方法体;
      };
      ```

   3. 试例
   
      ```vue
      <script setup>
      import {ref,reactive} from 'vue';
      let mage = ref("boot");
      const updated=() =>{
          mage.value="vue";
      };
      </script>
      <template>
      <div>
          <h1>{{mage}}</h1>
          <button @click="updated">Update Mage</button>
      </div>
      </template>
      ```
   
   4. `v-mode`：双向绑定、响应式数据
   

### 响应式数据

==vue3 的响应式数据是通过组合式 API 中的 ref 、 reactive 等方法直接构建的。通过 ref 、reactlve 方法，可以将数据包装成一个响应式副本，当数据变化时，副本也会自动更新。==

1. 响应式数据需要导入组件

   ```vue
   import {ref,reactive} from 'vue';
   ```

2. 对数据的修改

   1. 简单数据使用ref

   2. 复杂数据使用reactive

      ```vue
      <script setup>
      import {ref,reactive} from 'vue';
      let updatedd = reactive({
          id:"vue",
          name:"Vue.js",
          age:20
      });
      const updatede = () =>{
          updatedd.id="vue3";
          updatedd.name="Vue3.js";
          updatedd.age=18;
      };
      </script>
      <template>
      <div>
          <h2>=={{updatedd.id}} == {{updatedd.name}} == {{updatedd.age}}</h2>
          <button @click="updatede">Update updatedd</button>
      </div>
      </template>
      ```

3. toRef和toRefs函数

   1. 引入

      ```js
      import {ref,reactive,toRef,toRefs} from 'vue';
      ```

   2. 用于数据解构、将复杂对象里面的数据改为响应式数据

      ```js
      let {id,name,age} = toRefs(updatedd);
      let id = toRef(updatedd,"id");//对单个属性解构
      let {id:d,name,age} = toRefs(updatedd);//id:d、起别名，id的别名为d
      ```

   3. 式例

      ```vue
      <script setup>
      import {ref,reactive,toRef,toRefs} from 'vue';
      let updatedd = reactive({
          id:"vue",
          name:"Vue.js",
          age:20
      });
      let {id,name,age} = toRefs(updatedd);
      const updatede = () =>{
          id.value="vue3";
          name.value="Vue3.js";
          age.value=18;
      };
      </script>
      
      <template>
      <div>
          <h2>=={{updatedd.id}} == {{updatedd.name}} == {{updatedd.age}}</h2>
          <button @click="updatede">Update updatedd</button>
      </div>
      </template>
      ```

## 常用指令

vue 指令 (Directives) 是 vue.js 的一项核心功能，它们可以在 HTML 模板中以 v- 开头的特殊属性形式使用，用于将响应式数据绑定到 DOM 元素上或在 DOM 元素上进行一些操作； vue 指令是带有前缀 v- 的特殊 HTML 属性，它赋予 HTML 标签额外的功能；与传统的 JavaScript 方法相比，使用 vue 创建响应式页面要容易得多，并且需要的代码更少。以下是常用的 vue 指令：

### v-text和v-html

1. v-text 用于输出纯文本内容；v-html 用于解析包含标签元素的内容

   ```vue
   <script setup>
   import {ref,reactive,toRef,toRefs} from 'vue';
   let context = ref("可能");
   let content = ref("<p style='color:red'>可能</p>");
   </script>
   
   <template>
   <div>
       <p v-text="context"></p><!-- 输出为纯文本 -->
       <p v-html="context"></p>
       <p>==============</p>
       <p v-text="content"></p><!-- 输出为纯文本 -->
       <p v-html="content"></p>
   </div>
   </template>
   ```

### v-model

1. 双向绑定、相当于绑定文本框的value值、v-mode使用场景

2. 用于表单输入元素如 `<input>`, `<textarea>`, `<select>` 等。

   ```vue
   <script setup>
   import { ref,reactive } from 'vue';
   let setup = ref("vue3");
   let database = reactive({
       sex:18,
       checkbox:[],
       remeber:false,
       select:""
   })
   </script>
   <template>
       <div>
           <h1>{{setup}}</h1><br>
           <p>{{database.sex}}</p><br>
           <p>{{database.checkbox}}</p><br>\
           <p>{{database.remeber}}</p><br>
           <p>{{database.select}}</p><br>
           <p>=====================================</p>
           <input type="text" v-model="setup"><br>
           <input type="radio" v-model="database.sex" value="20"/> <input type="radio" v-model="database.sex" value="21"/><br>
           <input type="checkbox" v-model="database.checkbox" value="01"/> <input type="checkbox" v-model="database.checkbox" value="02"/>
           <input type="checkbox" v-model="database.checkbox" value="03"/> <input type="checkbox" v-model="database.checkbox" value="04"/><br>
           <input type="checkbox" v-model="database.remeber"/><br>
           <select v-model="database.select">
               <option value="">--请选择 --</option>
               <option value="1">Option 1</option>
               <option value="2">Option 2</option>
               <option value="3">Option 3</option>
               <option value="4">Option 4</option>
           </select>
       </div>
   </template>
   ```

3. 

### v-bind

1. 单向绑定v-bind可以简写为`:`

2. 动态绑定一个或多个特性，或一个组件 prop 到表达式。

   ```vue
   <script setup>
   import { ref,reactive } from 'vue';
   let setup = ref("vue3");
   </script>
   <template>
       <div>
           <h1>{{ setup }}</h1>
           <input type="text" v-bind:value="setup"/>
       </div>
   </template>
   ```

### v-if

- 条件性渲染一个块。
- 示例：`<div v-if="ok">OK!</div>`
- 条件为真着展示标签、为flase则不展示

### v-else

- 与 `v-if` 结合使用，作为 `v-if` 的补丁。
- 示例：`<div v-else>Not OK!</div>`
- `v-if`为true、`v-else`所在标签不展示；`v-if`为flase、`v-else`所在标签展示

### v-else-if

- 可以连续使用与 `v-if` 结合，作为另一个条件分支。
- 示例：`<div v-else-if="age > 18">Adult</div>`

### v-for

- 循环遍历一个数组或对象的属性。
- 示例：`<li v-for="item in items" :key="item.id">{{ item.text }}</li>`

### v-on` 或简写为 `@

- 添加一个事件监听器到元素。
- 示例：`<button @click="doSomething">Click me</button>`

### v-show

- 通过切换元素的 CSS 属性 `display` 来控制显示/隐藏。
- 示例：`<div v-show="ok">Show me!</div>`

### v-pre

- 跳过该元素和其子元素的编译过程。
- 示例：`<div v-pre>This will not be compiled.</div>`

### v-once

- 指令只执行一次，之后不会再响应数据变化。
- 示例：`<span v-once>{{ message }}</span>`

### 组件相关指令

1. **`v-slot`** 或简写为 `#`
   - 用于定义作用域插槽。
   - 示例：`<template v-slot:item="{ item }">{{ item.title }}</template>`
2. **`v-app`**
   - 用于标记根组件，虽然不是必须的，但在 Vue 2 中用于一些全局样式和特性，如过渡效果。

### 重要注意事项

- `v-if` 和 `v-for` 不应该在同一元素上同时使用，因为 `v-for` 优先级高于 `v-if`。
- 使用 `v-model` 时，对于复杂的数据类型，如数组或对象，你可能需要使用 `.sync` 修饰符或使用计算属性。
- `v-bind` 和 `v-on` 的缩写分别是 `:` 和 `@`，这可以让你的模板更简洁。

### 计算属性computed

计算属性的特点是，当依赖的属性发生变化时，计算属性会自动重新计算并更新其值。这意味着我们不需要手动去监听属性的变化，也不需要手动去更新计算属性的值， Vue 会自动帮我们完成这些操作。计算属性的另一个特点是，它会进行缓存。也就是说，只要依赖的属性没有发生变化，计算属性就会返回之前计算好的值，而不会重新计算。这样可以提高性能，避免不必要的计算。

1. 下面是一个 Vue 3 的计算属性 `computed` 的基本使用实例：

   ```html
   <template>
     <div>
       <p>First Name: <input v-model="firstName"></p>
       <p>Last Name: <input v-model="lastName"></p>
       <p>Full Name: {{ fullName }}</p>
     </div>
   </template>
   
   <script setup>
   import { ref, computed } from 'vue';
   
   const firstName = ref('John');
   const lastName = ref('Doe');
   
   // 使用 computed 创建一个计算属性
   const fullName = computed(() => {
     return `${firstName.value} ${lastName.value}`;
   });
   </script>
   ```

   1. 在这个例子中：
      * 我们有两个响应式状态变量 `firstName` 和 `lastName`，它们是由 `ref` 函数创建的。
      * 我们定义了一个计算属性 `fullName`，它依赖于 `firstName` 和 `lastName`。
      * 当 `firstName` 或 `lastName` 的值发生变化时，`fullName` 的值也会自动更新。

2. 计算属性不仅限于 getter，还可以定义 setter。下面的例子展示了如何使用计算属性的 setter：

   ```html
   <template>
     <div>
       <p>First Name: <input v-model="firstName"></p>
       <p>Last Name: <input v-model="lastName"></p>
       <p>Full Name: <input v-model="fullName"></p>
     </div>
   </template>
   
   <script setup>
   import { ref, computed } from 'vue';
   
   const firstName = ref('John');
   const lastName = ref('Doe');
   
   // 使用 computed 创建一个读写计算属性
   const fullName = computed({
     get() {
       return `${firstName.value} ${lastName.value}`;
     },
     set(value) {
       const parts = value.split(' ');
       firstName.value = parts[0];
       lastName.value = parts[1];
     }
   });
   </script>
   ```

   1. 在这个例子中：

      - 我们定义了一个计算属性 `fullName`，它有一个 getter 和一个 setter。
      - 当 `fullName` 的值被更新时，setter 会被调用，将 `fullName` 的新值分割成两部分，然后分别赋值给 `firstName` 和 `lastName`。

      ==注意，计算属性是基于它们的依赖进行缓存的，这意味着除非它们的依赖发生变化，否则计算属性不会重新计算。这可以提高应用的性能，特别是在处理大量数据或复杂的计算逻辑时==

### 监听属性

监听器 (watch) 是 Vue.js 的一种响应数据变化的技术，监听器允许开发人员监听 Vue 实例中的数据变化，并在数据变化时执行特定的动作。监听器可以作为 Vue 实例的方法，它们接收与被监听的数据相关的属性作为参数。当监听的数据发生变化时， Vue.js 会自动调用监听器函数。

Vue 3 中的 `watch` 是一个非常有用的 API，用于观察响应式引用（由 `ref` 创建的）或响应式对象（由 `reactive` 创建的）。`watch` 可以帮助你在数据变化时执行某些操作。

下面是一个使用 `watch` 的简单示例，这个例子展示了如何监听一个 `ref` 的变化，并在变化时执行一个函数：

```html
<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const count = ref(0);

// 监听 count 的变化
watch(count, (newValue, oldValue) => {
  console.log(`Count changed from ${oldValue} to ${newValue}`);
});

function increment() {
  count.value++;
}
</script>
```

在这个例子中：
- 我们定义了一个 `ref` 对象 `count` 并初始化为 `0`。
- 使用 `watch` 函数来监听 `count` 的变化。`watch` 接收两个参数：要监听的引用和一个回调函数。回调函数接收两个参数，`newValue` 和 `oldValue`，分别代表新的值和旧的值。
- 在模板中，我们显示了 `count` 的值，并且有一个按钮用于调用 `increment` 函数，这个函数会增加 `count` 的值。
- 每次 `count` 的值改变时，`watch` 的回调函数会被调用，并在控制台打印出变化的信息。

此外，如果你想监听一个对象的多个属性，你可以使用 `reactive` 而不是 `ref`，并使用更复杂的 `watch` 配置。例如：

```html
<template>
  <div>
    <p>Name: {{ person.name }}</p>
    <p>Age: {{ person.age }}</p>
    <button @click="updatePerson">Update Person</button>
  </div>
</template>

<script setup>
import { reactive, watch } from 'vue';

const person = reactive({
  name: 'John Doe',
  age: 30
});

// 监听 person 的变化
watch(person, (newVal, oldVal) => {
  console.log('Person changed:', newVal, oldVal);
}, { deep: true });

function updatePerson() {
  person.name = 'Jane Doe';
  person.age = 28;
}
</script>
```

在这个例子中：
- 我们使用 `reactive` 创建了一个包含 `name` 和 `age` 属性的对象 `person`。
- 使用 `watch` 监听整个 `person` 对象的变化，通过设置 `{ deep: true }` 来启用深度监听，这样就可以监听到对象内部属性的变化。
- 在模板中，我们显示了 `person` 的 `name` 和 `age` 属性。
- 点击按钮时，`updatePerson` 函数会更改 `person` 的属性值，触发 `watch` 的回调函数，从而在控制台上记录变化的信息。

## 组件间通信

在 Vue 3 中，组件间通信是一个关键的概念，它允许不同组件之间共享数据和事件。Vue 提供了多种机制来实现这一目标，以下是一些主要的通信方式：

1. **Props (父组件向子组件通信)**
   父组件可以向子组件传递数据，这通常通过 `props` 来完成。可以使用`definProps`进行接收、按属性名称接收
   
   ```html
   <!-- 子组件 -->
   <template>
     <div>{{ message }}</div>
   </template>
   <script>
   export default {
     props: ['message']
   };
   </script>
   
   <!-- 父组件 -->
   <template>
     <ChildComponent :message="parentMessage"/>
   </template>
   <script>
   import ChildComponent from './ChildComponent.vue';
   export default {
     components: { ChildComponent },
     data() {
       return {
         parentMessage: 'Hello from Parent'
       };
     }
   };
   </script>
   ```
   
2. **Events (子组件向父组件通信)**
   子组件可以通过触发事件来向父组件发送信息，父组件可以监听这些事件。通过`emits`把数据传给父组件的自定义函数，然后在父组件中的子标签中绑定方法，来获取自定义函数传过来的数据。
   
   ```html
   <!-- 子组件 -->
   <template>
     <button @click="sendMessage">Send Message</button>
   </template>
   <script>
   export default {
     methods: {
       sendMessage() {
         this.$emit('message-sent', 'Hello from Child');
       }
     }
   };
   </script>
   
   <!-- 父组件 -->
   <template>
     <ChildComponent @message-sent="handleMessage"/>
   </template>
   <script>
   import ChildComponent from './ChildComponent.vue';
   export default {
     components: { ChildComponent },
     methods: {
       handleMessage(message) {
         console.log(message);
       }
     }
   };
   </script>
   ```
   
3. **Refs 和 Custom Elements**
   使用 `ref` 和 `CustomElementsAPI`（如果适用）可以访问子组件的实例和方法。

4. **Provide / Inject**
   这是一种在组件树中向下传递数据的方法，而不必逐层传递 props。
   ```javascript
   // 父组件
   provide() {
     return {
       theme: 'dark'
     };
   }
   
   // 子组件或更深的组件
   inject: ['theme']
   ```

5. **Vuex**
   Vuex 是 Vue 的状态管理库，适合管理全局状态和复杂的状态流。

6. **Event Bus**
   一个全局的事件中心，可以用于没有直接父子关系的组件间通信。

7. **Teleport**
   Teleport 允许你将一个元素或一个片段“传送”到当前组件树之外的位置，这可以作为一种间接的通信方式。

8. **Composition API 中的组合逻辑**
   使用 `useFetch`, `useStore`, `useRouter` 等组合式函数可以提供组件间共享的逻辑。

9. **Global State Management**
   除了 Vuex，还有 Pinia 等替代方案，提供更现代的状态管理解决方案。

10. **Context 和 Props Drilling**
    尽管这不是 Vue 特有的，但在使用 Composition API 时，可以利用 ES6 的 Context API 来传递 prop 和 state。

## 插槽

在 Vue3 中，插槽 (slot) 是一个极为强大的功能，可以让我们更好地组织和重用组件。 Vue3 中的插槽分为三种类型：默认插槽、具名插槽和作用域插槽。每种类型的插槽都有各自的用处。通过使用插槽，我们可以将复杂的组件拆分成更小的、更独立的组件，并且将它们组合在一起，从而实现更高效灵活的开发。

### 默认插槽

在 Vue3 中，默认插槽是指在组件中没有特定命名的槽，也就是没有使用 `v-slot` 指令进行命名的插槽。默认插槽可以用来传递组件的内容，对于需要在组件中嵌入不同内容的情况非常有用。

1. 组件模板

   ```vue
   <template>
       <div>
           <slot></slot>
       </div>
   </template>
   ```

2. 父组件使用组件

   ```vue
   <template>
       <div>
           <MyComponent>
               <p>第一个插槽</p>
               <p>第二个插槽</p>
           </MyComponent>
       </div>
   </template>

### 具名插槽

Vue3中的具名插槽 (named slots) 是一种允许我们在组件中定义多个插槽，并根据名称将内容插入到相应的插槽位置上的功能。

具名插槽的使用场景通常是一个组件需要接受多个不同的内容，而这些内容在组件中的位置是不固定的。具名插槽可以让我们在组件的模板中定义不同名称的插槽然后在组件使用时，动态地向不同的插槽中插入相应的内容。

1. 父组件

   ```vue
   <template>
       <div>
           <chacao>
               <template v-slot:header>header/header</template>
               <template #footer>footer/footer</template>
               qwer
           </chacao>
       </div>
   </template>
   ```

2. 子组件

   ```vue
   <template>
     <div>
       <header>
           <slot name="header"></slot>
       </header>
       <main>
           <slot></slot>
       </main>
       <footer>
           <slot name="footer"></slot>
       </footer>
     </div>
   </template>
   ```

### 作用域插槽

作用域插槽 其实就是带数据的插槽@ 即带参数的插槽，简单的来说就是子组件提供给父组件的参数，该参数仅限于插槽中使用，父组件可根据子组件传过来的插槽数据来进行不同的方式展现和填充插槽内容。

1. 父组件

   ```vue
   <template>
       <div>
           <chacao>
               <template v-slot="slotPrpos">{{slotPrpos.text}}===={{slotPrpos.url}}</template>
           </chacao>
       </div>
   </template>
   ```

2. 子组件

   ```vue
   <template>
     <div>
       <slot :text="msg" url="www.baidu.com"></slot>
     </div>
   </template>
   ```

### 总结

 Vue3中的届槽是一个非常方便、强大、高效的功能。通过使用不同类型的插槽，我们可以将大型组件分解成更小、更可维护的子组件，同时可以极大地提高代码的可重用性和可扩展性。Vue3中的插槽可以帮助我们更好地组织代码、提高开发效率、优化用户 体验，是Vue3中不可或缺的一个特性。

## 生命周期

1. 生命周期钩子函数

   * setup ：组件实例创建之初，此时组件实例已经被创建，但 data 、 props 等属性还未初始化。可以在该钩子函数中进行一些数据初始化操作。
   * beforeMount: 组件即将被挂载到 DOM 树中，此时组件的模板已经编译完成。
   * onMounted: 组件成功地挂载到 DOM 树中，此时可以对 DOM 进行操作。
   * onBeforeUpdate: 组件的数据即将更新，重新渲染前调用。
   * onUPdated: 组件的数据已经更新完成， DOM 已经重新渲染。
   * onUnmounted: 组件即将被卸载，此时可以进行一些清理工作，比如取消定时器、解绑事件等。
   * onErrorCaptured：当捕获到来自子孙组件的错误时调用。
   * beforeUnmount: 在组件卸载之前调用，可以在这里做一些最后的清理工作。
   * unmounted: 组件已经被销毁，此时组件的所有内容都已经从 DOM 树中移除。
   * 需要注意的是，在 vue3 中， beforecreate 和 created 钩子函数合并为了 setup ，而且在 setup 函数中不能使用this 关键字，而是采用了新的响应式API。

2. 组件

   ```vue
   <template>
     <div>
       <h1>{{ message }}</h1>
     </div>
   </template>
   
   <script>
   import { onMounted, onUpdated, onBeforeUnmount, ref } from 'vue';
   
   export default {
     setup() {
       const message = ref('');
   
       // 在组件挂载完成后执行
       onMounted(() => {
         fetch('https://api.example.com/data')
           .then(response => response.json())
           .then(data => {
             message.value = data.message;
           });
       });
   
       // 在组件更新之前执行
       onUpdated(() => {
         console.log('Component has been updated');
       });
   
       // 在组件卸载前执行
       onBeforeUnmount(() => {
         console.log('Component is about to be unmounted');
       });
   
       return { message };
     }
   }
   </script>
   ```

3. 调整

   Vue 3 对生命周期钩子进行了一些调整，引入了组合式API（Composition API）来替代原有的选项式API（Options API），使得状态管理和逻辑复用更加灵活。不过，Vue 3 仍然支持传统的基于选项的组件形式，但同时也提供了基于组合式的生命周期函数。

   在传统的基于选项的组件中，Vue 3 的生命周期钩子如下：

   1. **beforeCreate**: 在实例初始化之后，数据观测 (data observer) 和事件/ watcher 事件配置之前被调用。
   2. **created**: 实例创建完成后被立即调用。此时，实例已完成以下的配置：数据观测、属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
   3. **beforeMount**: 在挂载开始之前被调用：相关的 render 函数首次被调用。
   4. **mounted**: el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。
   5. **beforeUpdate**: 数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。
   6. **updated**: 组件 DOM 更新后调用，指令 / 组件自定义数据已更新。
   7. **activated**: 当 keep-alive 组件激活时调用。
   8. **deactivated**: 当 keep-alive 组件停用时调用。
   9. **beforeUnmount**: 实例销毁之前调用。在这一步，实例仍然完全可用。
   10. **unmounted**: 实例销毁后调用。调用后，Vue 完全卸载实例，解绑所有的指令，移除事件监听器。

   而在组合式API中，使用的是`setup()`函数，可以使用以下的组合式生命周期函数：

   - **onBeforeMount()**: 在 `beforeMount` 钩子中执行。
   - **onMounted()**: 在 `mounted` 钩子中执行。
   - **onBeforeUpdate()**: 在 `beforeUpdate` 钩子中执行。
   - **onUpdated()**: 在 `updated` 钩子中执行。
   - **onBeforeUnmount()**: 在 `beforeUnmount` 钩子中执行。
   - **onUnmounted()**: 在 `unmounted` 钩子中执行。
   - **onActivated()**: 在 `activated` 钩子中执行。
   - **onDeactivated()**: 在 `deactivated` 钩子中执行。

   组合式API还提供了其他一些功能，如`ref`, `reactive`, `computed`等，这些可以帮助开发者更好地管理组件的状态和副作用逻辑。
   
   

## router（路由）

vue-router 是 Vue 官方准出的路由管理器主要用于管理 URL ，实现 URL 和组件的对应，以及通过 IJ RL 进行组件之间的切换，从而使构建单页面应用变得更加简单。

### 路由的安装及配置

1. 安装路由

   ```
   npm i vue-router@3//指定具体版本添加路由
   npm install --save vue-router//安装最新的路由
   ```

2. 配置独立路由文件

   1. 在src目录下新建路由文件夹`router`、和路由配置文件`index.js`

      ```js
      //引入VueRouter
      import { createRouter,createWebHashHistory } from 'vue-router';
      //引入Luyou 组件
      import About from '../components/About' 
      import Home from '../components/Home'
      //创建router实例对象，去管理一组一组的路由规则
      const routes=[
            {
                path:'/about',
                component: About },
            {
                path:'/home',
                component:Home
            },]  
      //注册路由
      const router = createRouter({
          history:createWebHashHistory(),//路由模式
          routes
      })
      //导出路由实例
      export default router;
      ```

   2. 在main.js中引入路由配置文件

      ```js
      import router from './router/index.js'
      
      createApp(App).use(router).mount('#app')
      ```

   3. 实现切换(active-class可配置高亮样式)

      ```vue
      <router-link active-class="active" to="/about">About</router-link>
      ```

   4. 指定展示位置

      ```vue
      <router-view></router-view>
      ```

### 动态路由

上面讲到的路由，都是严格匹配的，只有 route-link 中的 to 属性和 js 中定义的路由中的 path 一样时，才会显示对应的 componento 但实际开发时，这种方式是明显不足的，例如当用户去访问网站并登录成功之后，在页面中会显示"欢迎您“+用户名，不同的登录用户，只有"用户名“部分不同，其它部分一样，这就相当于一个组件，这里假设为是 User 用户组件；此时不同的用户（使用 id 来区分）都会导航到同一个 User 组件，这种情况下在配置路由的时候，需要把用户 id 作为参数传入，这就需要利用动态路由来实现；动态路由传参分两种： query 方式和 params 方式。

1. **query方式传参**

   步骤：

   1. 在跳转过程中携带参数

      ```vue
      <router-link  to="/about?name=baidu">About</router-link>//问号之后
      ```

   2. 在详情页读取路由携带的参数

      ```vue
      <p>{{ $route.query.name }} 不等于baidu</p>

2. **params方式传参**

   步骤

   1. 在跳转过程中携带

      ```vue
      <router-link  to="/about/baidu">About</router-link>
      ```

   2. 在路由配置文件中携带

      ```js
      {
      path:"/about/:name",
      component:About },
      ```

   3. 在详情页读取

      ```vue
      <p>{{ this.$route.params.name }} 不等于baidu</p>
      ```

### 嵌套路由

配置路由规则,使用children配置项:redirect可以设置默认路由地址

是否是嵌套路由主要是由页面结构来决定的，实际项目中的应用页面，通常由多层嵌套的组件组合而成。简而言之，嵌套路由就是在路由里面嵌套它的子路由；嵌套子路由的关键属性是 children，children 也是一组路由，相当于前面讲到的 routes。children 可以像 routes 一样去配置路由数组，每一个子路由里面可以嵌套多个组件，子组件又有路由导航和路由容器。嵌套路由案例如下．

```js
routes:[
    {
        path:'/about',
        component:About,
    },
    {
        path:'/home',
        component:Home,
        redirect:"/home/news"
        children:[ //通过children配置子级路由
            {
                path:'news', //此处一定不要写: /news
                component:New,
            },
            {
                path:'message',//此处一定不要写: /message
                component:Message
            }
        ]
    }
]
```

### 命名路由

1. 作用：可以简化路由的跳转。

   1. 如何使用

      1. 给路由命名：

         ```js
         {
             path:'/demo',
             component:Demo,
             children:[
                 {
                     path: 'test',
                     component:Test,
                     children:[
                         {
                             name:'hello' //给路由命名
                             path:'welcome',
                             component:Hello,
                         }
                     ]
                 },
                 {
                   path:"/about/:name",
                   name:"about",
                   component:About }
             ]
         }
         ```

      2. 简化跳转：

         ```vue
         <！--简化前，需要写完整的路径 -->
         <router-link to="/demo/test/welcome">跳转</router-link>
         <！--简化后，直接通过名字跳转-->
         <router-link :to="{name:'hello'}">跳转</router-link>
         <！--简化写法配合传递参数 -->
         <router-link 
             :to="{
                   name: 'hello',
                   query:{
                          id:666,
                          title:'你好'
                   }
         }"
         >跳转</router-link>
         //跳转
         <router-link  :to="{name:'about',params:{name:'baidu'}}">About</router-link>
         //接收
         <p>{{ this.$route.params.name }} 不等于baidu</p>    
         ```

### 命名视图

在开发中，有时候想同时或同级展示多个视图，而不是嵌套展示，则可以在页面中定义多个单独命名的视图。例如创建一个布局有 header( 头部区域）、 sidebar (侧导航区域）和 mainBox（主体区域） 3 个视图，这时候就可以用命名视图来实现。使用`<router-view>`可以为视图进行命名，它主要用来负责路由跳转后组件的展示。在`<router-view>`上定义 name 属性表示视图的名字，然后就可以根据不同的 name 值展示不同的页面，例如：left、main等，如果`<router—V1ew>`没有设置名字，那么默认为 default。

1. 分别创建 header （头部区域）、 sidebar （侧导航区域）和 mainBox（主体区域）组件

   ```vue
   //头
   <script setup>
   import { ref,reactive } from 'vue';
   </script>
   <template>
       <div class="square">header</div>
   </template>
   <style scoped>
   .square {
       width: 150px; /* 宽度 */
       height: 50px; /* 高度 */
       background-color: #777; /* 背景颜色 */
   }
   </style>
   //左
   <script setup>
   import { ref,reactive } from 'vue';
   </script>
   <template>
       <div class="square">left</div>
   </template>
   <style scoped>
   .square {
       width: 50px; /* 宽度 */
       height: 100px; /* 高度 */
       background-color: #f00; /* 背景颜色 */
   }
   </style>
   //主体
   <script setup>
   import { ref,reactive } from 'vue';
   </script>
   <template>
       <div class="square">left</div>
   </template>
   <style scoped>
   .square {
       width: 100px; /* 宽度 */
       height: 100px; /* 高度 */
       background-color: #f7893f; /* 背景颜色 */
   }
   </style>
   ```

2. 路由配置文件

   ```js
   import { createRouter,createWebHashHistory } from 'vue-router';
   
   import About from '../components/About.vue'
   import Header from '../components/Header.vue';
   import Left from '../components/Left.vue';
   import Mainbox from '../components/Mainbox.vue';
   
   const routes=[
         {
             path:"/about/:name",
             name:"about",
             component:About },
         {
             path:"/home",
             components:{//命名
               'default':Header,
               'left':Left,
               'main':Mainbox
             }          
         },]  
   
   const router = createRouter({
       history:createWebHashHistory(),
       routes
   })
   
   export default router;
   ```

3. App.vue组件

   ```vue
   <script setup>
   </script>
   
   <template>
     <div>
       <router-link  :to="{name:'about',params:{name:'baidu'}}">About</router-link>
       <router-link to="/home">Home</router-link>
       <router-view>
   
       </router-view>
       <div class="con">
         <router-view name="left"></router-view>
         <router-view name="main"></router-view>
       </div>
     </div>
   </template>
   
   <style scoped>
   .con{
     display: flex;
   }
   </style>
   ```

### 路由守卫

路由守卫就是路由跳转过程中的一些钩子函数，在路由啭的时候，做一些判断或其它的操作。类似于组件生命周期钩子函数。

在Vue 3中，路由守卫是一种控制导航流程的方法，可以在导航发生之前、之后执行一些逻辑，例如验证用户身份、保存表单数据、重定向等。Vue Router 提供了几种类型的路由守卫，包括全局守卫、单个路由守卫和组件内的守卫。

#### 全局守卫

全局守卫是在整个应用级别设置的，它们可以作用于任何路由。主要有以下几种：

1. **全局前置守卫 (`beforeEach`)**: 在路由转换之前调用。
2. **全局解析守卫 (`beforeResolve`)**: 在路由解析之前调用。
3. **全局后置守卫 (`afterEach`)**: 在路由转换完成后调用。

**示例：全局前置守卫**

```javascript
import { createRouter, createWebHistory } from 'vue-router';
import store from './store';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    // 路由配置...
  ],
});

// 全局前置守卫
router.beforeEach((to, from, next) => {
  // 检查用户是否登录
  if (to.meta.requiresAuth && !store.state.isLoggedIn) {
    next({ name: 'login' }); // 重定向到登录页
  } else {
    next();
  }
});

// 全局后置守卫
router.afterEach(() => {
  // 导航完成后执行的操作
  console.log('Navigation completed.');
});

export default router;
```

1. **`to`**: 是一个Route对象，表示目标路由。它包含了即将进入的目标路由的信息，比如路径、查询参数等。
2. **`from`**: 同样也是一个Route对象，表示当前导航正要离开的路由。这包含了当前正在离开的路由的信息。
3. **`next`**: 是一个回调函数，必须被调用来完成路由跳转。它的调用方式决定了导航的行为：
   - 调用 `next()` 表示无条件地允许导航。
   - 调用 `next(false)` 会取消当前的导航，并确保当前的路由不会改变。
   - 调用 `next('/somepath')` 或者 `next({ path: '/somepath' })` 会重定向到一个新的位置。

#### 单个路由守卫

单个路由守卫只针对特定的路由配置，可以定义在路由配置对象的 `beforeEnter` 属性中。

**示例：单个路由守卫**

```javascript
const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/secret',
      name: 'secret',
      component: SecretComponent,
      beforeEnter: (to, from, next) => {
        // 检查用户是否有权限访问此路由
        if (store.state.userRole === 'admin') {
          next();
        } else {
          next({ name: 'home' }); // 重定向到主页
        }
      },
    },
    // 其他路由...
  ],
});
```

#### 组件内的守卫

组件内的守卫是在组件内定义的，用于控制组件级别的导航。

1. **`beforeRouteEnter`**: 在进入该组件的对应路由前调用。
2. **`beforeRouteUpdate`**: 在当前路由改变，但是该组件被复用时调用。
3. **`beforeRouteLeave`**: 在离开该组件的对应路由时调用。

**示例：组件内的守卫**

```javascript
// SecretComponent.vue
export default {
  name: 'SecretComponent',
  beforeRouteEnter(to, from, next) {
    // 在进入组件前执行
    if (store.state.isLoggedIn) {
      next();
    } else {
      next(false); // 中断导航
    }
  },
  beforeRouteUpdate(to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    console.log('Route updated but the component was reused.');
    next();
  },
  beforeRouteLeave(to, from, next) {
    // 在离开该组件的对应路由时调用
    const answer = window.confirm('Are you sure you want to leave?');
    if (answer) {
      next();
    } else {
      next(false); // 中断离开操作
    }
  },
};
```

这些守卫可以帮助你更好地管理应用的导航流程，确保只有经过验证的用户才能访问某些页面，并且可以在导航发生前后执行必要的逻辑。如果你有更具体的需求或者想了解更复杂的用例，请随时提问。

## Axios（异步请求）

`axios` 是一个基于 Promise 的 HTTP 客户端，用于浏览器和 Node.js 中的 AJAX 请求。它被广泛用于与 RESTful API 进行交互。`axios` 提供了许多有用的功能，例如拦截请求和响应、转换请求数据和响应数据、取消请求等。

### 安装 Axios

要在项目中使用 `axios`，首先需要安装它。可以通过 npm 或 yarn 进行安装：

```bash
npm install axios
npm install --save axios
# 或者
yarn add axios
```

### 基本使用

#### 发送 GET 请求

发送一个 GET 请求以获取数据：

```javascript
import axios from 'axios';//在组件中引入axios

axios.get('https://api.example.com/data')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error("Error fetching data:", error);
  });
```

#### 发送 POST 请求

发送一个 POST 请求以提交数据：

```javascript
import axios from 'axios';

const data = {
  username: 'john_doe',
  password: 'secret'
};

axios.post('https://api.example.com/login', data)
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error("Error logging in:", error);
  });
```

**例：**

```vue
<script setup>
import {  reactive, onMounted } from "vue";
import axios from "axios";

let emp = reactive({
  id: 0,
  username: "",
  password: "",
  classg: ""
});

onMounted(() => {
  axios({
    method: "get", //请求方式
    url: "http://localhost:8080/web/axioss",
  }).then((res) => {
    emp.id = res.data.id;
    emp.username = res.data.username;
    emp.password = res.data.password;
    emp.classg = res.data.classg;
    console.log(res.data);
  });
});
</script>
<template>
  <div>
    <p>{{ emp.id }}</p><br />
    <p>{{ emp.username }}</p><br />
    <p>{{ emp.password }}</p><br />
    <p>{{ emp.classg }}</p><br />
  </div>
</template>
<style scoped>
</style>
```

### 	Axios的网络封装

在日常应用过程中，一个项目中的网络请求会很多，此时一般采取的方案是将网络请求封装起来

1. 安装 

   1. axios ：` npm install axios` ； 
   1.  querystring: `npm install querystring`

2. 创建src/utils/request.js

   ```js
   import axios from 'axios';
   import querystring from 'querystring';
   
   // 错误处理函数，根据HTTP状态码输出相应的错误信息
   const errorHandle = (status, info) => {
       switch (status) {
           case 400:
               console.log("语义错误");
               break;
           case 401:
               console.log("服务器认证失败");
               break;
           case 403:
               console.log("服务器拒绝访问");
               break;
           case 404:
               console.log("地址错误");
               break;
           case 500:
               console.log("服务器报出异常");
               break;
           case 502:
               console.log("服务器报无响应");
               break;
       }
   };
   
   // 创建一个axios实例，并配置一些公共属性
   const instance = axios.create({
       // 设置请求超时时间为5秒
       timeout: 5000,
   });
   
   // 请求拦截器
   instance.interceptors.request.use(
       config => {
           // 如果请求方式是 POST，则将请求体转换为查询字符串格式
           if (config.method === "post") {
               config.data = querystring.stringify(config.data);
           }
           // 返回配置对象，以便继续执行请求
           return config;
       },
       error => {
           // 如果请求发送失败，可以在这里处理错误
           // 通常不需要返回任何值，因为错误会被传递给响应拦截器
       }
   );
   
   // 响应拦截器
   instance.interceptors.response.use(
       response => {
           // 如果HTTP响应状态码为200，则返回Promise解析后的响应对象
           return response.status === 200 ? Promise.resolve(response) : Promise.reject(response);
       },
       error => {
           // 如果HTTP响应状态码不是200，则返回Promise拒绝，并调用错误处理函数
           const { response } = error;
           errorHandle(response.status, response.data);
           return Promise.reject(error);
       }
   );
   
   // 导出axios实例供其他模块使用
   export default instance;
   ```

   1.  **说明**
      1. **错误处理函数** (`errorHandle`):
         - 该函数接收两个参数：HTTP状态码 (`status`) 和错误信息 (`info`)。
         - 根据状态码输出相应的错误信息。
      2. **创建axios实例** (`instance`):
         - 使用 `axios.create()` 创建一个axios实例。
         - 设置了请求超时时间为5秒。
      3. **请求拦截器** (`request interceptor`):
         - 对于POST请求，使用 `querystring.stringify()` 将请求体转换为查询字符串格式。
         - 最终返回配置对象，继续执行请求。
      4. **响应拦截器** (`response interceptor`):
         - 如果HTTP响应状态码为200，则返回Promise解析后的响应对象。
         - 如果HTTP响应状态码不是200，则返回Promise拒绝，并调用错误处理函数。
      5. **导出axios实例**:
         - 通过 `export default instance;` 将自定义的axios实例导出，以便在其他模块中使用。

3. 创建src/api/path.js和src/api/index.js

   ```js
   //src/api/path.js
   
   const base ={
       //请求前公共部分
       baseUrl:"http://localhost:8080",
       //ResquestMapping地址
       jtr:"/web/axioss"
   }
   export default base;
   ```

   ```js
   // src/api/index.js
   
   import instance from "../utils/request"
   import base from "./path";
   
   const api = {
       getWeb(){
           return instance.get(base.baseUrl+base.jtr);
       }
   }
   
   export default api;
   ```

4. 组件使用

   ```vue
   <script setup>
   import {  reactive, onMounted } from "vue";
   import api from "../api";
   
   let emp = reactive({
     id: 0,
     username: "",
     password: "",
     classg: ""
   });
   
   onMounted(() => {
       api.getWeb().then((res) => {
       emp.id = res.data.id;
       emp.username = res.data.username;
       emp.password = res.data.password;
       emp.classg = res.data.classg;
       console.log(res.data);
     });
   });
   </script>
   <template>
     <div>
       <p>{{ emp.id }}</p><br />
       <p>{{ emp.username }}</p><br />
       <p>{{ emp.password }}</p><br />
       <p>{{ emp.classg }}</p><br />
     </div>
   </template>
   <style scoped>
   </style>
   ```

### 配置选项

`axios` 允许你通过配置选项来自定义请求行为。例如，你可以设置超时、身份验证、请求头等。

```javascript
axios({
  method: 'post',
  url: 'https://api.example.com/login',
  data: {
    username: 'john_doe',
    password: 'secret'
  },
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  auth: {
    username: 'admin',
    password: 'password'
  },
  timeout: 5000 // 设置超时为5秒
})
.then(response => {
  console.log(response.data);
})
.catch(error => {
  console.error("Error logging in:", error);
});
```

### 拦截器

`axios` 支持请求和响应拦截器，可以用来添加一些通用逻辑，例如自动添加认证令牌或处理错误响应。

```javascript
axios.interceptors.request.use(
  config => {
    // 在发送请求之前做些什么
    return config;
  },
  error => {
    // 对请求错误做些什么
    return Promise.reject(error);
  }
);

axios.interceptors.response.use(
  response => {
    // 对响应数据做点什么
    return response;
  },
  error => {
    // 对响应错误做点什么
    return Promise.reject(error);
  }
);
```

### 创建实例

为了复用相同的配置，你可以创建一个 `axios` 实例：

```javascript
const instance = axios.create({
  baseURL: 'https://api.example.com',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});

instance.get('/data')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error("Error fetching data:", error);
  });
```

### 提取`axios` 中将 URL 的公共部分

 要在 `axios` 中将 URL 的公共部分（如 `localhost` 或其他基础 URL）提取到一个公共配置文件中，你可以按照以下步骤操作：

1. **创建配置文件**

首先，创建一个配置文件，例如 `config.js`，并在其中定义基础 URL：

```javascript
// config.js
export const API_BASE_URL = 'http://localhost:3000/api';
```

2. **导入配置文件**

在你的应用中导入这个配置文件，以便可以在需要的地方使用它。

3. **创建 `axios` 实例**

接着，你可以创建一个 `axios` 实例，并将基础 URL 设置为实例的默认值。这样，在所有的请求中都可以使用这个基础 URL。

```javascript
// axiosInstance.js
import axios from 'axios';
import { API_BASE_URL } from './config';

const instance = axios.create({
  baseURL: API_BASE_URL,
  // 其他配置...
});

export default instance;
```

4. **使用 `axios` 实例**

在你的组件或其他地方使用这个 `axios` 实例来发送请求。

```javascript
// Example.vue
import axiosInstance from './axiosInstance';

export default {
  methods: {
    fetchData() {
      axiosInstance.get('/data')
        .then(response => {
          console.log(response.data);
        })
        .catch(error => {
          console.error("Error fetching data:", error);
        });
    }
  }
};
```

5. **使用环境变量**

如果你希望在不同的环境中使用不同的基础 URL（例如开发环境使用 `localhost`，而生产环境使用实际的服务器地址），你可以使用环境变量来动态设置基础 URL。这通常通过 `.env` 文件来实现。

首先，你需要安装 `dotenv` 库来加载环境变量：

```bash
npm install dotenv
```

然后，在项目的根目录下创建一个 `.env` 文件，例如：

```plaintext
VUE_APP_API_BASE_URL=http://localhost:3000/api
```

接下来，修改你的配置文件，使其读取环境变量：

```javascript
// config.js
import dotenv from 'dotenv';
dotenv.config();

export const API_BASE_URL = process.env.VUE_APP_API_BASE_URL;
```

最后，在 `axiosInstance.js` 中使用配置文件中的 `API_BASE_URL`：

```javascript
// axiosInstance.js
import axios from 'axios';
import { API_BASE_URL } from './config';

const instance = axios.create({
  baseURL: API_BASE_URL,
  // 其他配置...
});

export default instance;
```

这样，无论是在开发环境还是生产环境，你都可以通过更改 `.env` 文件中的值来轻松切换基础 URL。同时，由于 `axios` 实例已经使用了配置文件中的基础 URL，所以你的代码不需要做出任何改变。

请注意，在生产环境中部署时，你需要确保 `.env` 文件不在版本控制系统中，并且在生产环境中正确设置了相应的环境变量。

### axios跨域

（cors）跨域支持

1. 在 Vite 的配置文件中，可以通过 proxy 选项来配置代理，使得前端代码与接口请求在同一域下。例如：

2. `vite.config.js`

   ```js
   import { defineConfig } from 'vite'
   import vue from '@vitejs/plugin-vue'
   
   // https://vitejs.dev/config/
   export default defineConfig({
     plugins: [vue()],
     server:{
       proxy:{
         '/api':{
           target:'http://localhost:8080',
           changeOrigin:true,
           rewrite:path => path.replace(/^\/api/,'')
         }
       }
     }
   })
   ```

3. 组件

   ```vue
   <script setup>
   import {  reactive, onMounted } from "vue";
   import axios from "axios";
   
   
     axios.get('http://localhost:5173/api/web/axioss').then(res => {
       console.log(res.data);
     }).catch(error => {
       console.error("Error fetching data:", error);
     });
   </script>
   <template>
     <div>
       
     </div>
   </template>
   <style scoped>
   </style>
   ```

### Aixos发送接收后端数据

需要axios支持

1. Axios.vue==组件==

2. vite.config.js==vite构建vue发送axios需要的设立==

3. path.js==新建文件夹api作为项目访问地址分类使用==

4. index.js==新建api文件夹,在里面拼接访问路径==

5. request.js==返回值接收信息处理、新建utils文件夹==

   1. Axios

      ```vue
      <script lang="ts" setup>
      import { ref, onMounted } from "vue";
      import api from "../api";
      
      const tableData = ref([]);
      
      onMounted(() => {
        fetchData();
      });
      
      const fetchData = async () => {
        let data = {
          id: 5,
          username: "张三",
          password: "123654",
          classg: "2",
        };
      
        try {
          const response = await api.getMvca(data);
          tableData.value = response.data.date;
          console.log(tableData.value);
        } catch (error) {
          console.error("Error fetching data:", error);
        }
      };
      </script>
      <template>
        <div>
          <el-table :data="tableData" style="width: 100%">
            <el-table-column prop="id" label="ID" width="180" />
            <el-table-column prop="username" label="Name" width="180" />
            <el-table-column prop="password" label="密码" width="180" />
            <el-table-column prop="classg" label="班级" />
          </el-table>
        </div>
      </template>
      <style scoped>
      </style>
      ```

   2. vite.config.js

      ```js
      import { defineConfig } from 'vite'
      import vue from '@vitejs/plugin-vue'
      
      // https://vitejs.dev/config/
      export default defineConfig({
        plugins: [vue()],
        server:{
          proxy:{
            '/api':{
              target:'http://localhost:8080',
              changeOrigin:true,
              rewrite:path => path.replace(/^\/api/,'')
            }
          }
         }
      })
      ```

   3. path.js

      ```js
      const base ={
          //请求前公共部分
          baseUrl:"http://localhost:5173/api",
          //ResquestMapping地址
          jtr:"/web/axioss",
          jts:"/web/b/",
          jta:"/web/a"
      }
      
      
      export default base;
      ```

   4. index.js

      ```js
      //import instance from "../utils/request"
      import axios from 'axios';
      import base from "./path";
      const instance = axios.create({
          baseURL: 'http://localhost:5173/api', // 替换为您的 API 基础 URL
          headers: {
            'Content-Type': 'application/json' // 设置 Content-Type 为 JSON
          }
        });
      
      const api = {
          getWeb(){
              return instance.get(base.jtr);
          },
          getMvc(id){
              return instance.get(base.baseUrl+base.jts+id);
          },
          getMvca(data){
              return instance.post(base.baseUrl+base.jta,data)
          }
      }
      
      export default api;
      ```

   5. request.js

      ```js
      import axios from 'axios';
      import querystring from 'querystring'
      
      const errorHandle = (status, info) => {
          switch (status) {
              case 400:
                  console("语义错误")
                  break;
              case 401:
                  console("服务器认证失败")
                  break;
              case 403:
                  console("服务器拒绝访问")
                  break;
              case 404:
                  console("地址错误")
                  break;
              case 500:
                  console("服务器报出异常")
                  break;
              case 502:
                  console("服务器报无响应")
                  break;
          }
      }
      
      
      
      const instance = axios.create({
          timeout: 5000, //请求超时时间
      });
      //拦截器最常用的
      
      //发送数据之前
      instance.interceptors.request.use(
          config => {
              if (config.method == "post") {
                  config.data = querystring.stringify(config.data)
              }
              //包含网络请求的所有信息
              return config
          },
          error => {
              return Promise.reject(error)
              //异常
          }
      );
      
      //获取数据之前
      instance.interceptors.response.use(
          response => {
              return response.status == 200 ? Promise.resolve(response) : Promise.reject(response)
          },
          error => {
              const { response } = error;
              errorHandle(response.status, response.info)
          }
      );
      
      export default instance;
      ```

## 集成Element

在 Vue 3 中结合使用 Element Plus 是一个常见的需求，尤其是当你希望利用 Element Plus 提供的丰富的 UI 组件库时。下面是详细的步骤来演示如何在 Vue 3 项目中集成并使用 Element Plus。

### 步骤 1: 安装必要的依赖

确保你已经在项目中安装了 Vue 3 和 Element Plus。如果你还没有安装，可以通过 npm 或 yarn 来安装：

```bash
npm install vue@next element-plus
npm install element-plus
# 或者使用 yarn
yarn add vue@next element-plus
```

1. **`npm install vue@next element-plus`**:
   - 这条命令安装的是 Vue.js 的下一个主要版本（通常是指最新的稳定版或即将发布的版本），以及 Element Plus 的最新版本。
   - 使用 `@next` 标签通常意味着安装的是 Vue.js 的最新稳定版本，或者是即将到来的主要版本（如果有 alpha/beta/rc 版本发布的话）。
   - Element Plus 会安装其最新版本。
2. **`npm install element-plus`**:
   - 这条命令仅安装 Element Plus 的最新版本。
   - 默认情况下，不会指定 Vue.js 的版本，这意味着您需要确保已经安装了与 Element Plus 兼容的 Vue.js 版本。
3. 总结
   - 如果您想要安装 Vue 3 和 Element Plus 的最新版本，您应该使用 `npm install vue@next element-plus`。
   - 如果您已经安装了 Vue 3 或者打算使用 Vue 3，并且只想要安装 Element Plus 的最新版本，可以使用 `npm install element-plus`。

### 步骤 2: 引入 Element Plus

在你的主入口文件（通常是 `main.js` 或 `main.ts`）中引入并使用 Element Plus。你需要引入 Element Plus 的样式文件和组件。

```javascript
// main.js
import { createApp } from 'vue';
import App from './App.vue';
import ElementPlus from 'element-plus';
import 'element-plus/dist/index.css';//导入样式表

const app = createApp(App);
app.use(ElementPlus);
app.mount('#app');
```

### 步骤 3: 在组件中使用 Element Plus 组件

一旦你完成了以上步骤，你就可以在 Vue 3 的组件中使用 Element Plus 的组件了。例如，使用一个按钮组件：

```html
<!-- src/components/MyComponent.vue -->
<template>
  <el-button type="primary">Hello Element Plus</el-button>
</template>

<script>
export default {
  name: 'MyComponent',
};
</script>
```

### 步骤 4: 配置按需加载（可选）

为了优化你的应用程序，你可能希望只引入你需要的 Element Plus 组件，而不是整个库。这可以通过使用像 `unplugin-vue-components` 和 `unplugin-auto-import` 这样的插件来实现，它们可以自动按需导入 Element Plus 的组件和 Vue 的 API。

在你的 `vite.config.js` 或 `webpack.config.js` 文件中添加相应的插件配置。

1. 将数据插入表格

   ```vue
   <script lang="ts" setup>
   import { ref, onMounted } from "vue";
   import api from "../api";
   
   const tableData = ref([]);
   
   onMounted(() => {
     fetchData();
   });
   
   // 获取数据
   const fetchData = async () => {
     try {
       const response = await api.getWeb(); // 假设这是您的 API 调用
       tableData.value = [response.data]; // 假设 response.data 是符合格式的 JSON 数据
       console.log(tableData.value);
     } catch (error) {
       console.error('Error fetching data:', error);
     }
   };
   </script>
   <template>
     <div>
       <el-table :data="tableData" style="width: 100%">
         <el-table-column prop="id" label="ID" width="180" />
         <el-table-column prop="username" label="Name" width="180" />
         <el-table-column prop="password" label="密码" width="180" />
         <el-table-column prop="classg" label="班级" />
       </el-table>
     </div>
   </template>
   <style scoped>
   </style>
   ```

#### 对于 Vite:

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import Components from 'unplugin-vue-components/vite';
import AutoImport from 'unplugin-auto-import/vite';
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';

export default defineConfig({
  plugins: [
    Components({
      resolvers: [ElementPlusResolver()],
    }),
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
  ],
});
```

## 引入Bootstrap

要在 Vue 3 中使用 Bootstrap，你需要安装并配置 Bootstrap 和其相关的 JavaScript 插件。以下是详细的步骤：

### 1. 安装 Bootstrap 和相关依赖

首先，你需要安装 Bootstrap 和 Popper.js（Bootstrap 5 的必需依赖）以及一个可选的图标库如 Font Awesome。你可以使用 npm 或 yarn 来安装这些包。

```bash
npm install bootstrap popper.js font-awesome
# 或者使用 yarn
yarn add bootstrap popper.js font-awesome
```

### 2. 配置全局样式

接下来，在你的 Vue 项目的 `main.js` 或 `main.ts` 文件中引入 Bootstrap 的 CSS 和 JavaScript 文件。

#### 引入 CSS

在项目的入口文件（通常是 `src/main.js` 或 `src/main.ts`）中，添加以下代码以引入 Bootstrap 的 CSS：

```javascript
import 'bootstrap/dist/css/bootstrap.min.css';
// 如果你想使用 Font Awesome 图标，也需要引入它的 CSS
import 'font-awesome/css/font-awesome.min.css';
```

#### 引入 JavaScript

同时，引入 Bootstrap 的 JavaScript 文件和 Popper.js：

```javascript
import 'bootstrap/dist/js/bootstrap.bundle.min';
```

### 3. 使用 Bootstrap 组件

现在你可以在 Vue 组件中直接使用 Bootstrap 的 HTML 类。例如，创建一个按钮：

```vue
<template>
  <button type="button" class="btn btn-primary">Hello Bootstrap</button>
</template>
```

### 4. 使用 Vue 3 的 Composition API

Vue 3 推荐使用 Composition API 进行组件开发。你可以在 `<script setup>` 中使用 Vue 3 的 Composition API 特性。

### 5. 使用 Vue 3 的 TypeScript 支持

如果你的项目是基于 TypeScript 的，你可能还需要安装 `@types/bootstrap` 和 `@types/popper.js`。

```bash
npm install @types/bootstrap @types/popper.js
# 或者使用 yarn
yarn add @types/bootstrap @types/popper.js
```

### 6. 使用 Bootstrap Vue 3 (可选)

如果你希望使用专门针对 Vue 的 Bootstrap 组件库，你可以考虑使用 `bootstrap-vue-3`。

#### 安装 Bootstrap Vue 3

```bash
npm install bootstrap-vue-3
# 或者使用 yarn
yarn add bootstrap-vue-3
```

#### 配置 Bootstrap Vue 3

在 `main.js` 或 `main.ts` 中配置 Bootstrap Vue 3：

```javascript
import { createApp } from 'vue';
import { BootstrapVue3, BIcon } from 'bootstrap-vue-3';
import 'bootstrap/dist/css/bootstrap.min.css';

const app = createApp(App);

app.use(BootstrapVue3);
app.component('b-icon', BIcon);

app.mount('#app');
```

这样你就可以在 Vue 3 组件中使用 `bootstrap-vue-3` 提供的组件了。

以上步骤应该可以帮助你在 Vue 3 项目中成功地集成 Bootstrap。如果你遇到任何问题或有更具体的需求，请告诉我！

## 打包部署

在Vue 3中使用Vite创建的应用，打包和部署的过程相对简单。以下是基本的步骤：

### 1. 打包应用
首先，你需要使用Vite提供的构建命令来打包你的应用。确保你在项目的根目录下运行以下命令：

```bash
npm run build
```

或者如果你使用的是Yarn：

```bash
yarn build
```

这将会生成一个`dist`文件夹，里面包含了你的应用的静态资源，包括HTML、CSS和JavaScript文件。

### 2. 部署应用
一旦你有了`dist`文件夹，你就可以将其部署到任何支持静态文件托管的服务提供商上，比如GitHub Pages、Netlify、Vercel、AWS S3等等。

#### 部署到GitHub Pages
如果你打算将应用部署到GitHub Pages，你可以遵循以下步骤：

1. **确保你的GitHub仓库已经设置为包含一个`gh-pages`分支**，并且这个分支将用于部署你的应用。

2. **在你的`vite.config.js`文件中配置base路径**。如果应用将在子目录下部署，你需要在Vite配置文件中指定正确的`base`路径。

   ```javascript
   // vite.config.js
   import { defineConfig } from 'vite';
   import vue from '@vitejs/plugin-vue';

   export default defineConfig({
     plugins: [vue()],
     base: process.env.NODE_ENV === 'production' ? '/your-app-name/' : '/'
   });
   ```

3. **使用GitHub Actions进行自动化部署**。你可以创建一个GitHub Action来自动化构建和部署过程。下面是一个简单的示例`.github/workflows/deploy.yml`文件，用于自动部署到GitHub Pages：

   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches:
         - main  # 你的主分支名称

   jobs:
     deploy:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
         - uses: actions/setup-node@v3
           with:
             node-version: 18
         - run: npm ci
         - run: npm run build
         - uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./dist
             user_name: 'github-actions[bot]'
             user_email: 'github-actions[bot]@users.noreply.github.com'
   ```

   这个配置文件会监听`main`分支上的提交，并在每次提交后自动运行构建和部署流程。

4. **推送更改**。确保你的`vite.config.js`和`.github/workflows/deploy.yml`文件已经被提交到你的GitHub仓库。

5. **等待部署完成**。一旦你的GitHub Action运行完成，你的应用就会被部署到GitHub Pages上。

6. **访问应用**。你的应用现在可以通过以下URL访问：
   ```
   https://<username>.github.io/<repo-name>/
   ```

   或者，如果你使用了子目录作为`base`路径，那么URL将是：
   ```
   https://<username>.github.io/<repo-name>/<your-app-name>/
   ```

这就是使用Vite创建的Vue 3应用打包和部署的基本步骤。当然，你可以根据自己的需求调整这些步骤。如果你有特定的部署目标或者需要更详细的配置，请告诉我，我可以提供更多的帮助。

