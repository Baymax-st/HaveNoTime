<template>   <!-- // 写结构标签 -->
    <div class="app">
        <!-- <h1>Welcome to BYD 4S</h1> -->
        <!-- <hr> -->
        <person></person>
        <!-- <person></person>
        <hr>
        <person></person>
        <hr> -->
    </div>
</template>

<script>  // 写js代码
import Person from './components/Person.vue'

export default {
    name: 'App', // 组件名
    data() {
        return {
            
        }
    },
    components: {
        Person  // 注册组件
    }
,
        Person}
</script>

<style>   /* 写样式 */
    #app {
        font-family: 'Helvetica Neue', Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin: 40px auto;
        max-width: 1200px;
        padding: 20px;
        background-color: #ffffff;
        box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
    }

    h1 {
        color: #425eb9;
        font-size: 2.5em;
        margin-bottom: 30px;
    }

    hr {
        border: none;
        height: 1px;
        background-color: #e8e8e8;
        margin: 20px 0;
    }
     /* .app {
        background-color: black;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        padding: 20px;
        border-radius: 5px;
        color: white;
    } */
</style>