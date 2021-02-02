<template>
  <div id="app">
    <h1>Todo List</h1>
    <div class="new">
      <div class="name">
        <input type="text" name="name" id="name" v-model="newName" />
      </div>
      <button @click="insertContact">追加</button>
    </div>
    <div class="table">
      <table>
        <tr>
          <th>更新</th>
          <th>削除</th>
        </tr>
        <tr v-for="item in contactLists" :key="item.id">
          <td>{{ item.id }}</td>
          <td>
            <input type="text" v-model="item.name" />
          </td>
          <td>
            <input type="email" v-model="item.email" />
          </td>
          <td>
            <button @click="updateContact(item.id, item.name, item.email)">
              更新
            </button>
          </td>
          <td>
            <button @click="deleteContact(item.id)">削除</button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newName: "",
      newEmail: "",
      contactLists: [],
    };
  },
  methods: {
    async getContact() {
      const resData = await axios.get("<http://127.0.0.1:8000/api/contact/>");
      this.contactLists = resData.data.data;
    },
    async insertContact() {
      const sendData = {
        name: this.newName,
        email: this.newEmail,
      };
      await axios.post("<http://127.0.0.1:8000/api/contact/>", sendData);
      await this.getContact();
    },
    async updateContact(id, name, email) {
      const sendData = {
        name: name,
        email: email,
      };
      await axios.put("<http://127.0.0.1:8000/api/contact/>" + id, sendData);
      await this.getContact();
    },
    async deleteContact(id) {
      await axios.delete("<http://127.0.0.1:8000/api/contact/>" + id);
      await this.getContact();
    },
  },
  created() {
    this.getContact();
  },
};
</script>

<style>
.app {
  width: 300px;
  padding: 20px 12px 10px;
  color: #333;
  border: 1px solid #e9eaea;
  border-radius: 3px;
  transition: 0.3s;
}

.new.name{
 margin: 0;
}


table,
td,
th {
  border: 1px solid #000;
  border-collapse: collapse;
  text-align: center;
}
td,
th {
  padding: 5px;
}
th {
  background: #f0e6cc;
}
</style>
