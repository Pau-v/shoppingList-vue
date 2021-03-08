<template>
  <div class="shopping-list">
    <h1>Lista de la compra</h1>
    <h4>Total de productos {{items.length}} </h4>
  <form class="form" @submit.prevent="createItem">
    <input  class="new" type="text" v-model="newItem" id="item" autofocus placeholder="Escribe aquí...">
    <input class="button" type="submit" value="Añadir producto">
  </form>
    <ul class="list">
        <li class="product"
                 v-for="(item, i) in items"   
                :key="'item' + i"
                :class="{completed: item.completed}"
                @click="completeItem(item.text)"
                >{{item.text}}
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: () => ({
    newItem: "",
    items: []
  }),
  methods: {
    createItem() {
      let item = {
        text: this.newItem,
        completed: false
      };
      this.items.push(item);
      this.newItem = "";
      console.log(this.items);
    },
     completeItem(itemText) {
      for (let i = 0; i < this.items.length; i++) {
        let item = this.items[i];
        if (itemText === item.text) {
          item.completed = !item.completed;
        }
      }
    }
  }
};
</script>

<style scoped>
.shopping-list {
  width: 800px;
  max-width: 100%;
  margin: 0px auto;
}
.form {
  padding: 30px;
  margin-top: 10px;
}
.new {
  height: 35px;
}
.button {
  margin-left: 20px;
  height: 35px;
  border: none;
  border-radius: 5px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, .2);
  background-color: #4c56ad;
  color: #ecf0f1;
  cursor: pointer
}
.list {
  margin-top: 40px;
}
.product {
  cursor: pointer;
  margin: 10px 0;
  list-style-type: square;
  list-style-position: inside;
}
.completed {
  text-decoration: line-through;
  color: lightgrey;
}
</style>