<script setup>
  import AddToListModal from './AddToListModal.vue'
  import ListDisplay from './ListDisplay.vue'
</script>

<script>
  export default {
    name: "AddToListForm",
    components: {
      AddToListModal,
      ListDisplay
    },
    data: function () {
      return {
        newListItem: '',
        modalIsOpen: false,
        list: [],
      }
    },
    mounted () {
      if (localStorage.list) {
        this.list = JSON.parse(localStorage.list)
      } else {
        localStorage.list = JSON.stringify([])
      }
    },
    methods: {
      handleInitialSubmit: function () {
        if (!this.newListItem.length) {
          return;
        }
        this.modalIsOpen = true;
      },
      handleCloseModal: function () {
        this.modalIsOpen = false;
      },
      updateList: function (newList) {
        this.list = newList;
        this.modalIsOpen = false;
        this.newListItem = '';
        localStorage.list = JSON.stringify(this.list)
      }
    }
  }
</script>

<template>
  <div class="container">
    <input v-model="newListItem" type="text" ref="newItemTextBox" class="newItemTextBox" placeholder="Add new item to a list..." @keyup.enter="handleInitialSubmit"/>
    <AddToListModal v-if="modalIsOpen" @closeModal="handleCloseModal" :list="list" :newListItem="newListItem" @updateList="updateList"></AddToListModal>
    <ListDisplay v-if="list.length" :list="list"></ListDisplay>
  </div>

</template>

<style scoped>
  .container {
    width: 100%;
    min-height: 100%;
    border: 1px solid lightgrey;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    position: relative
  }

  .newItemTextBox {
    width: 90%;
    max-width: 500px;
    padding: 10px;
    outline: none;
  }
</style>
