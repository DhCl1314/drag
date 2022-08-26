<!--
 * @Author: dh
 * @Date: 2022-08-26 15:00:12
 * @LastEditTime: 2022-08-26 16:24:13
 * @LastEditors: dh
 * @Description: 
 * @FilePath: \drag\src\views\AboutView.vue
 * 可以输入预定的版权声明、个性签名、空行等
-->
<template>
  <div class="about">
    <template>
      <div>
        <div class="drop-zone" @drop="onDrop($event, 1)" @dragover.prevent>
          <div v-for="item in listOne" draggable @dragstart="startDrag($event, item)" :key="item.title" class="drag-el">
            {{ item.title }}
          </div>
        </div>
        <div class="drop-zone" @drop="onDrop($event, 2)" @dragover.prevent>
          <div class="drag-el" v-for="item in listTwo" :key="item.title" draggable @dragstart="startDrag($event, item)">
            {{ item.title }}
          </div>
        </div>
      </div>
    </template>
  </div>
</template>
<script>
export default {
  computed: {
    listOne() {
      return this.items.filter((item) => item.list === 1);
    },
    listTwo() {
      return this.items.filter((item) => item.list === 2);
    },
  },
  data() {
    return {
      items: [
        {
          id: 0,
          title: "Item A",
          list: 1,
        },
        {
          id: 1,
          title: "Item B",
          list: 1,
        },
        {
          id: 2,
          title: "Item C",
          list: 2,
        },
      ],
    };
  },
  methods: {
    onDrop(evt, list) {
      console.log(222);
      const itemID = evt.dataTransfer.getData("itemID");
      const item = this.items.find((item) => item.id == itemID);
      item.list = list;
    },
    startDrag: (evt, item) => {
      evt.dataTransfer.dropEffect = "move";
      evt.dataTransfer.effectAllowed = "move";
      evt.dataTransfer.setData("itemID", item.id);
    },
  },
};
</script>
<style scoped>
.drop-zone {
  background-color: #eee;
  margin-bottom: 10px;
  padding: 10px;
}

.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 5px;
}
</style>
