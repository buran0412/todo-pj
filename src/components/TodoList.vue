<template>
  <div class="todolist">
    <div
      class="input-update"
      v-for="(item, index) in items"
      v-bind:key="item.id"
    >
      <input type="item.message" v-model="item.message" />
      <button class="edit-button" @click="$emit('edit', $event, index)">
        更新
      </button>
      <button class="remove-button" @click="$emit('remove', $event, index)">
        削除
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  props: {
    items: {
      type: Array,
      default: function() {
        return [];
      },
    },
  },
};
</script>

<style>
.todolist {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  font-size: 100%;
  vertical-align: baseline;
  background: transparent;
}


.edit-button {
  text-align: left;
  border: 2px solid #fa9770;
  font-size: 12px;
  color: #fa9770;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
}
.remove-button {
  text-align: left;
  border: 2px solid #71fadc;
  font-size: 12px;
  color: #71fadc;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
}
</style>
