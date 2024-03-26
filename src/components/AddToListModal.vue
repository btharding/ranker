<script>
    export default {
        name: "AddToListModal",
        components: {},
        props: {
            list: Array,
            newListItem: String
        },
        data: function () {
            return {
                subListStartPointer: 0,
                subListEndPointer: -1,
                currentComparisonPointer: -1
            }
        },
        mounted () {
            this.subListEndPointer = this.list.length - 1;
            this.currentComparisonPointer = Math.floor(this.subListEndPointer/2)
        },
        methods: {
            toggleModal: function () {
                this.$emit('closeModal');
            },
            handleComparison: function (newIsBetter) {
                let nextEnd = this.subListEndPointer;
                let nextStart = this.subListStartPointer;
                if (newIsBetter) {
                    nextEnd = this.currentComparisonPointer - 1;
                } else {
                    nextStart = this.currentComparisonPointer + 1;
                }

                if (nextStart > nextEnd) {
                let newIndex = null;
                if (newIsBetter) {
                    newIndex = nextEnd + 1;
                } else {
                    newIndex = nextStart;
                }

                this.$emit('updateList', [...this.list.slice(0, newIndex), this.newListItem, ...this.list.slice(newIndex)]);
                return;
                }

                this.subListEndPointer = nextEnd;
                this.subListStartPointer = nextStart;
                this.currentComparisonPointer = Math.floor((nextEnd - nextStart) / 2) + nextStart
            },
            submitNewListEntry: function () {
                this.$emit('updateList', [this.newListItem]);
            }
        },
    }
</script>

<template>
    <div class = "AddItemModalContainer" @click.self="toggleModal">
      <div class="container AddItemModal">
        <div class="comparisonContainer" v-if="list.length">
            <h1 @click="handleComparison(true)">{{  newListItem }}</h1>
            <h1 @click="handleComparison(false)">{{ list[currentComparisonPointer] }}</h1>
        </div>
        <div v-else @click="submitNewListEntry">{{ newListItem }}</div>
      </div>
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

    .AddItemModal {
        max-width: 1200px;
        background-color: white;
    }
    .AddItemModalContainer {
        width: 100%;
        height: 100%;
        background-color: rgba(0,0,0,0.2);
        position: absolute;
        top: 0;
        left: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 40px;
    }
    .newItemTextBox {
    width: 90%;
    max-width: 500px;
    padding: 10px;
    outline: none;
  }
</style>