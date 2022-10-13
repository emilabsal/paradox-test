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
      <div class="categories-block">
        <draggable
          v-model="blocks.categories"
          :group="{
            name: 'categories',
            pull: ['category'],
            put: ['category'],
          }"
          v-bind="dragOptions"
          @start="drag = true"
          @end="drag = false"
          item-key="index"
          handle=".category-button-drag"
        >
          <template #item="{ element }">
            <category-item :category="element">
              <!-- <div class="categories-elements"> -->
              <draggable
                v-model="element.elements"
                group="elements"
                v-bind="dragOptions"
                @start="drag = true"
                @end="drag = false"
                item-key="index"
                handle=".element-button-drag"
              >
                <template #item="{ element }">
                  <element-item :element="element" />
                </template>
              </draggable>
              <!-- </div> -->
            </category-item>
          </template>
        </draggable>
      </div>
      <div class="elements-common">
        <draggable
          :list="blocks.elements"
          :group="{ name: 'elements', pull: 'elements', put: true }"
          v-bind="dragElementOptions"
          @start="drag = true"
          @end="drag = false"
          item-key="index"
          handle=".element-button-drag"
        >
          <template #item="{ element }">
            <element-item :element="element" />
          </template>
        </draggable>
      </div>
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
      show: false,
      drag: true,
      blocks: {
        categories: [
          {
            title: "Обязательные для всех",
            circles: [
              { background: "#FF238D" },
              { background: "#FFB800" },
              {
                background: "#FF8D23",
                border: "#000000",
                shadow: "0px 4px 4px rgba(0, 0, 0, 0.25)",
              },
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
            title: "Специальные",
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
        ],
        elements: [
          {
            title: "Тестовое задание кандидата",
            circle: false,
            require: false,
            status:
              "Россия, Белоруссия, Украина, администратор филиала, повар-сушист, повар-пиццмейкер, повар горячего цеха",
          },
          {
            title: "Трудовой договор",
            circle: true,
            require: false,
          },
          {
            title: "Мед. книжка",
            circle: false,
            require: false,
          },
        ],
      },
    };
  },
  computed: {
    dragOptions() {
      return {
        animation: 200,
        disabled: false,
        ghostClass: "ghost",
        chosenClass: "chosen",
        dragClass: "drag",
      };
    },
    dragElementOptions() {
      return {
        animation: 200,
        disabled: false,
        ghostClass: "ghostElement",
        chosenClass: "chosenElement",
        dragClass: "dragElement",
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

.categories-elements {
  transition: 0.3s;
  // animation: slide 0.5s linear forwards;
}

@keyframes slide {
  0% {
    height: 0;
  }

  100% {
    height: auto;
  }
}

.ghost {
  opacity: 0.2;
}

.elements {
  .element {
    border-top: none;
  }

  .element:last-child {
    border-bottom: none;
    border-top: none;
  }
}

.elements-common {
  margin-top: 14px;

  .element:not(:last-child) {
    border-bottom: none;
  }
}

.chosen {
  opacity: 1 !important;
}
.drag {
  opacity: 0 !important;
}
.ghost {
  background: #0066ff;
  height: 5px;
  width: 100%;
  opacity: 1;
  overflow: hidden;
  // opacity: 15;
  // border: 1px solid #dfe4ef;
  // box-shadow: 0px 3px 16px rgba(0, 102, 255, 0.7);
}
</style>
