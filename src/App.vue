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
      <draggable
        v-model="categories"
        :group="{ name: 'categories', pull: 'clone', put: false }"
        v-bind="dragOptions"
        @start="drag = true"
        @end="drag = false"
        item-key="index"
        tag="transition-group"
        :component-data="{ name: 'fade' }"
        handle=".category-button-drag"
      >
        <template #item="{ element }">
          <div class="categories">
            <category-item class="categories-category" :category="element" />
          </div>
        </template>
      </draggable>
      <draggable
        v-model="categories"
        :group="{ name: 'categories', pull: ['categories'], put: false }"
        v-bind="dragOptions"
        @start="drag = true"
        @end="drag = false"
        item-key="index"
        tag="transition-group"
        :component-data="{ name: 'fade' }"
        handle=".category-button-drag"
      >
        <template #item="{ element }">
          <div class="elements">
            <element-item :element="element" v-if="element" />
          </div>
        </template>
      </draggable>
    </div>
  </main>
</template>

<script>
import UiButton from "./components/ui/UiButton.vue";
import SearchItem from "./components/SearchItem.vue";
import CategoryItem from "./components/CategoryItem.vue";
import ElementItem from "./components/ElementItem.vue";
import draggable from "vuedraggable";

export default {
  name: "App",
  components: {
    UiButton,
    SearchItem,
    CategoryItem,
    ElementItem,
    draggable,
  },
  data() {
    return {
      hello: "",
      drag: false,
      categories: [
        {
          title: "Обязательные для всех",
          circles: [
            { background: "red" },
            { background: "red" },
            { background: "red" },
          ],
          desc: "Документы, обязательные для всех сотрудников без исключения",
          elements: [
            {
              title: "Паспорт",
              circle: true,
              require: true,
              status: "Для всех",
            },
            {
              title: "ИНН",
              circle: false,
              require: true,
              status: "Для всех",
            },
          ],
        },
        {
          title: "Обязательные для трудоустройства",
          desc: "Документы, без которых невозможно трудоустройство человека на какую бы то ни было должность в компании вне зависимости от граж",
        },
        {
          title: "Специальные",
        },
        {
          elements: [
            {
              title: "Тестовое задание кандидата",
              status:
                "Россия, Белоруссия, Украина, администратор филиала, повар-сушист, повар-пиццмейкер, повар горячего цеха",
            },
          ],
        },
        {
          elements: [
            {
              title: "Трудовой договор",
            },
          ],
        },
        {
          elements: [
            {
              title: "Мед. книжка",
            },
          ],
        },
      ],
    };
  },
  methods: {},
  computed: {
    dragOptions() {
      return {
        animation: 200,
        disabled: false,
        ghostClass: "ghost",
        chosenClass: "chosen",
        dragClass: "drag",
        onStart: function (e) {
          console.log(e);
          const hello = e.clone;
          hello.style.background = "red";
        },
      };
    },
  },
};
</script>

<style lang="scss" scoped>
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

.ghost {
  opacity: 0.2;
}

.elements {
  margin-top: 14px;
}

// .drag {
//   background: white;
//   opacity: 15;
//   border: 1px solid #dfe4ef;
//   box-shadow: 0px 3px 16px rgba(0, 102, 255, 0.7);
// }
</style>
