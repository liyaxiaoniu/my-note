<template>
   <div id="app">
      <n-header @tools="changePages"></n-header>
      <section class="container">
        <n-add  v-on:addContent ="showContent"></n-add>
        <n-list  v-bind:pramsMes="prams"></n-list>
        <n-sidebar :is-show="tools"></n-sidebar>
      </section>
   </div>
</template>

<script>
    import nHeader from './components/nHeader.vue';
    import nAdd from './components/event_add.vue';
    import nList from './components/event_list.vue';
    import nSidebar from './components/sidebar.vue';


    export default {
      data(){
            return {
                tools:false,
                dialog: false,
                table: false,
                theme: false,
                prams:{}
            }
        },

        components: {
          nHeader,
          nAdd,
          nList,
          nSidebar
        },
        methods: {
            changePages() {
              if(this.table){
                this.table = !this.table;
              }else if(this.theme){
                this.theme = !this.theme;
              }else{
                this.tools = !this.tools;
              }
            },
            showContent(data) {
              this.prams = data;
            }
        }
    }
</script>
<style lang="scss" rel="stylesheet/scss" src="../static/theme.scss"></style>
<style lang="scss" rel="stylesheet/scss">
   html,body,ul,li,input{
        margin:0;
        padding:0;
    }
    body{
        font-size: 16px;
        font-family: "Helvetica Neue", Helvetica, "microsoft yahei", arial, STHeiTi, sans-serif;
    }
    input,button{
        -webkit-tap-highlight-color: transparent;
    }
    input[type=text]{
        -webkit-appearance: none;
    }
    button{
        padding:7px 0;
        outline: none;
        text-align: center;
        border-radius: 4px;
        box-sizing: border-box;
        font:{
            size:inherit;
            family: inherit;
        }
        cursor: pointer;
    }
    body,#app{
        width:100%;
        overflow-x: hidden;
    }
    ul{
        list-style: none;
    }
    .container{
        width:100%;
        padding: 0 10px;
        max-width:800px;
        margin:auto;
        box-sizing: border-box;
        &.hide{
            display: none;
        }
    }
    .dialog-enter-active, .dialog-leave-active {
        transition: opacity .3s;
    }
    .dialog-enter, .dialog-leave-to{
        opacity: 0;
    }
</style>
