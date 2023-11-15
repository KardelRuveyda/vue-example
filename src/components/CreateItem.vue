<template>
      <div class="create-item">
        <div class="create-item-text">Title :</div>
        <div class="create-item-input">
          <input type="text" v-model="itemText" placeholder="Enter your task title." @keyup.enter="onAddClick" />
        </div>
        <div class="create-item-button"><button @click="onAddClick" @keyup.enter="onAddClick" >Add</button></div>
      </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Emit, Component } from 'vue-property-decorator';

@Component
export default class CreateItem extends Vue {

  itemText = "";
  onAddClick(){
    //event gönderme
    this.addItemEvent(this.itemText);
    this.itemText='';
  }

  @Emit('add:item')
  addItemEvent(itemText:string){

  }
}
</script>

<style scoped lang="scss">

    .create-item {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      padding: 5px;

      div {
        padding: 0 5px 0 5px;
      }

      .create-item-input {
        display: flex;
        flex: 1;

        input[type='text'] {
          flex: 1;
          font-family: Roboto, Helvetica, Arial, sans-serif;
          font-size: 12pt;
          padding: 10px;
          border: 1px solid #ccc;
          border-radius: 10px;
        }
      }

      .create-item-button {
        display: flex;

        button {
          font-family: Roboto, Helvetica, Arial, sans-serif;
          font-size: 12pt;
          padding: 10px;
        }
      }
    }
</style>
