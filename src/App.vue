<template>
  <main class="main">
    <header class="header">
      <h1 class="header-title">Документы</h1>
      <div class="header-controls">
        <ui-button class="header-favor" icon="favor" />
        <ui-button class="header-add" icon="plus" name="Новый тип" />
        <ui-button class="header-add" icon="plus" name="Новый документ" />
      </div>
    </header>
    <div class="search-block">
      <search-item @input="search" />
    </div>
    <div class="blocks">
      <div class="categories">
        <CategoryItem
          @dragstart="startDrag"
          class="categories-category"
          v-for="(item, index) in categories"
          :key="index"
          :category="item"
        />
      </div>
      <div class="elements"></div>
    </div>
  </main>
</template>

<script>
import UiButton from "./components/ui/UiButton.vue";
import SearchItem from "./components/SearchItem.vue";
import CategoryItem from "./components/CategoryItem.vue";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    UiButton,
    SearchItem,
    CategoryItem,
  },
  setup() {
    const items = ref([]);
    const categories = ref([
      {
        title: "Обязательные для всех",
        circles: 3,
        item: [{ background: "red" }],
        desc: "Документы, обязательные для всех сотрудников без исключения",
      },
      {
        title: "Нет",
        circles: 2,
        item: [{ background: "red" }],
        desc: "Документы, обязательные для всех сотрудников без исключения",
      },
      {
        title: "Обязательные для всех",
        circles: 3,
        item: [{ background: "red" }],
        desc: "Документы, обязательные для всех сотрудников без исключения",
      },
      {
        title: "Обязательные для всех",
        circles: 3,
        item: [{ background: "red" }],
        desc: "Документы, обязательные для всех сотрудников без исключения",
      },
    ]);

    // function onDragStart(event, item) {}
    // function onDrop(event, categories.title) {}

    return {
      items,
      categories,
    };
  },

  data() {
    return {
      cats: this.categories,
    };
  },
  methods: {
    search(val) {
      console.log(val);
      this.cats = this.categories.filter((item) => {
        item.title === val;
      });
    },
  },
  startDrag(evt, item) {
    evt.dataTransfer.dropEffect = "move";
    evt.dataTransfer.effectAllowed = "move";
    evt.dataTransfer.setData("itemID", item.id);
  },
  onDrop(evt, list) {
    const itemID = evt.dataTransfer.getData("itemID");
    const item = this.items.find((item) => item.id == itemID);
    item.list = list;
  },
};
</script>

<style lang="scss">
.main {
  padding: 38px 30px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header-title {
  font-size: 22px;
  font-weight: 500;
  line-height: 108%;
}

.header-controls {
  display: flex;
  align-items: center;
  gap: 10px;
}

.header-favor {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  border: 1px solid #d3d8df;
}

.header-add {
  height: 30px;
  padding-left: 10px;
  padding-right: 19px;
  border-radius: 50px;
  border: 1px solid #d3d8df;
  font-size: 12px;
  font-weight: 500;
  line-height: 108%;
}

.search-block {
  padding-top: 23px;
  padding-bottom: 19px;
}

.blocks {
  max-width: 1190px;
}

.categories-category + .categories-category {
  border-top: 0;
}
</style>
