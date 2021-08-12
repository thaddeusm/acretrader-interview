<template>
  <div class="list-container">
    <ListItem :item="list[focusItemIndex]" v-if="itemView" @close-item-view="closeItemView" />
    <section class="full-list" v-else>
      <div class="card" v-for="(item, index) of list" :key="index" @click="endEdit">
        <div class="card-header">
          <input type="text" :name="item.title" v-model="item.title" v-if="editIndex == index">
          <h2 @click="handleTitleClick(index)" v-else>
            {{ item.title }}
          </h2>
        </div>
        <div class="card-body">
          <button @click={openItemView(index)}>
            read more
          </button>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import ListItem from './ListItem.vue';

export default {
  name: 'List',
  components: {
    ListItem
  },
  data: function() {
    return {
      list: [{
        userId: 0,
        id: 0,
        completed: true,
        title: ''
      }],
      itemView: false,
      focusItemIndex: 0,
      editIndex: null
    }
  },
  methods: {
    getList: async function() {
      let req = await fetch('https://jsonplaceholder.typicode.com/todos');

      req.json().then((res) => {
        this.list = res.slice(0, 20);
      })
    },
    openItemView: function(itemIndex) {
      this.itemView = true;
      this.focusItemIndex = itemIndex;
    },
    closeItemView: function() {
      this.itemView = false;
    },
    handleTitleClick: function(index) {
      this.editIndex = index;
    },
    endEdit: function(e) {
      if (e.target.tagName !== "H2" && e.target.tagName !== "INPUT" ) {
        this.editIndex = null;
      }
    }
  },
  mounted: function() {
    this.getList();
  }
}
</script>

<style scoped>
  @media screen and (max-width: 1000px) {
    .full-list {
      grid-template-rows: 1fr 1fr;
    }
  }

  @media screen and (min-width: 1001px) {
    .full-list {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }

  .full-list {
    display: grid;
    list-style: none;
  }

  .card {
    border: 1px solid black;
    margin: 1rem;
    padding: 10px;
  }

  .card-header {
    grid-area: header;
    text-align: left;
  }

  .card-body {
    grid-area: header;
    text-align: left;
  }

  h2 {
    margin: 2rem 0;
  }

  h6 {
    margin: 2rem 0;
  }
</style>
