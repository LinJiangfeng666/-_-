<script setup>
// <!-- 专门负责怎么动。定义数据（变量）、编写方法（函数）、处理逻辑（添加、删除、修改） -->
// 从vue框架中导入ref函数，用来创建响应式变量（页面改数据自动更新）
 import { ref } from 'vue'
 // 创建响应式变量 list，初始值是空字符串 ''
// ref包裹后，页面template可以直接使用这个list
const value = ref('')
const list = ref([
  {
    iscompleted: false,
    text: '吃饭'
  },
  {
    iscompleted: false,
    text: '睡觉'
  },
  {
    iscompleted: false,
    text: '打豆豆'
  },
])  // 用来存储todo列表的数组

// 定义添加按钮点击触发的函数
function add() {
  list.value.push({
    iscompleted: false,
    text: value.value
  })
  value.value = ''
}

function del(index) {
  list.value.splice(index, 1)
}
</script>
<!-- template 负责长什么样 -->
<template>   
    <div class="Todo-App">
        <div class="title">Todo-App</div>
        <div class="todo-form">
            <input v-model="value" class="todo-input" type="text" placeholder="Add a todo">
            <div @click="add" class="todo-button">Add Todo</div>
            <!-- @click="add"：事件监听，点击按钮执行 add 函数。 -->
        </div>
        <div v-for="(item, index) in list" 
        :key="index"
        :class="item.iscompleted ? 'completed' : 'item'">
            <div>
                <input type="checkbox" v-model="item.iscompleted">
                <span class="name">{{ item.text }}</span>
            </div>
            <div @click="del(index)" class="del">del</div>
        </div>
    </div>

</template>

<style scoped>
/* 加上的 scoped（作用域）会自动给模板里的每个元素打上独特的“门牌号（data 属性） */
:global(body){
   background: linear-gradient(135deg, #667eea, #764ba2);
   min-height: 100vh;
   margin: 0;
}
.photo{
  width: 350px;
  border-radius: 9999px;
}
.Todo-App{
  width: 98%;
  max-width: 600px;   /* 我加了个最大宽度，更美观 */
  height: 500px;
  padding-top: 30px;
  box-sizing: border-box;
  background-color: white;
  border-radius: 5px;
  margin: 40px auto;  /* 居中 */
}
.title{
  font-size: 30px;
  font-weight: 700;
  text-align: center;
}
.todo-form{
  display: flex;
  margin-top: 20px;
  justify-content: center;
}
.todo-input{
  border: 1px solid #dfe1e5;
  padding-left: 15px;
  outline: none;
  width: 60%;
  height: 50px;
  border-radius: 20px 0 0 20px;
}
.todo-button{
  width: 100px;
  height: 53px;
  line-height: 53px;
  border-radius: 0 20px 20px 0;
  text-align: center;
  background: linear-gradient(135deg, #667eea, #764ba2);
  user-select: none;
  color: white;
  cursor: pointer;
}
.item {
  margin-top: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap:8px;
  box-sizing: border-box;
  width: 80%;
  height: 50px;
  margin: 8px auto;
  padding: 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 20px;
}
.del {
  color: red;
  cursor: pointer;
}
.completed {
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  height: 50px;
  margin: 8px auto;
  padding: 16px;
  border-radius: 20px;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 20px;
  text-decoration: line-through;
  opacity: 0.4;
}
</style>

