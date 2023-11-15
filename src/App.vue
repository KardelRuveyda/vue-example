<template>
  <div class="app-container">
    <div id="app">
      <PageHeader title="To Do App" />
      <CreateItem :itemText="itemText" @add:item="onAddItem" />
      <div class="list">
        <div class="list-header">Total item count: {{ itemCount }}, 
        completed: {{ completedItemCount }}</div>
        <div :class="'list-row' + (item.isCompleted ? ' completed ' : '')" v-for="(item,index) in items">
          <div class="item-checkbox"><input type="checkbox" v-model="item.isCompleted" /></div>
          <div class="item-id">{{item.id}}</div>
          <div class="item-text">{{ item.text }}</div>
          <div class="item-date">{{ item.createdDate.toLocaleDateString() }}</div>
          <div class="item-delete-button"><button @click="onDeleteClick(index)" :title="index">Delete</button></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import PageHeader from './components/PageHeader.vue';
import {ToDoItem} from './services';
import CreateItem from './components/CreateItem.vue';

@Component({
  components: {
    PageHeader,
    CreateItem
  },
})

export default class App extends Vue {
  pageTitle = "To Do App";

  itemText = "";
  nextId=1;
  

  items:ToDoItem[] =[];


 get itemCount(){
   return this.items.length;
 }

get completedItemCount(){
  return this.items.filter(x=>x.isCompleted).length;
}
  onAddItem(itemText: string){
    console.log(itemText);
    this.items.push(
      {
         id:this.nextId++,
         text:itemText,
         createdDate:new Date(),
         isCompleted:false});
  }
onDeleteClick(index: number) {
  const find = this.items.findIndex(item => item.id === index);

  if (index > -1) {
    this.items.splice(index, 1);
  }
}
}
</script>

<style lang="scss">
body {
  background-color: rgb(241, 255, 232);
  margin: 0;
  padding: 0;
}
.app-container {
  display: flex;
  justify-content: center;
  background-color: rgb(241, 255, 232);
  padding: 0;
  margin: 0;

  #app {
    font-family: Rubik, Helvetica, Arial, sans-serif;
    font-size: 14pt;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-color: rgb(232, 247, 221);
    color: #2c3e50;

    .list {
      display: flex;
      flex-direction: column;
      padding-top: 5px;
      color: black;

      .list-header {
        text-align: center;
      }

      .list-row {
        display: flex;
        flex-direction: row;
        align-items: center;
        font-family: Roboto, Helvetica, Arial, sans-serif;
        font-size: 13pt;

        &:nth-child(odd) {
          background-color: #ddd;

          &:hover {
            background-color: #bbb;
            cursor: pointer;
          }
        }

        &:nth-child(even) {
          background-color: #eee;

          &:hover {
            background-color: #bbb;
            cursor: pointer;
          }
        }

        div {
          padding: 5px;
        }

        .item-text {
          flex: 1;
        }

        .item-date {
          font-size: 10pt;
          text-align: center;
        }

        .item-delete-button {
          button {
            font-family: Roboto, Helvetica, Arial, sans-serif;
            font-size: 12pt;
            padding: 7px;
          }
        }

        &.completed {
          color: #444;
          .item-id,
          .item-text {
            text-decoration: line-through;
          }
        }
      }
    }
  }
}

@media (min-width: 960px) {
  .app-container #app {
    width: 720px;
  }
}
</style>
