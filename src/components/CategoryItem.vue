
<template>
  <div class="category-wrapper">
    <div class="category">
      <div class="category-left">
        <ui-button class="category-arrow" icon="chevron" />
        <span class="category-title">{{ category.title }}</span>
        <div class="category-circles" v-if="category.circles">
          <span
            v-for="(circle, index) in category.circles"
            :key="index"
            class="category-circle"
            :style="`background-color: ${
              circle.background || '#FF238D'
            }; border: 1px solid ${
              circle.border || 'transparent'
            }; box-shadow: ${circle.shadow};`"
          ></span>
        </div>
        <p class="category-desc" v-if="category.desc">
          {{ category.desc }}
        </p>
      </div>
      <div class="category-controls">
        <ui-button class="category-button" icon="edit" />
        <ui-button class="category-button" icon="delete" />
        <ui-button class="category-button category-button-drag" icon="drag" />
      </div>
    </div>
    <div class="elements" v-if="category.elements">
      <element-item
        :element="item"
        v-for="(item, index) in category.elements"
        :key="index"
      />
    </div>
  </div>
</template>

<script>
import UiButton from "@/components/ui/UiButton.vue";
import ElementItem from "@/components/ElementItem.vue";

export default {
  components: {
    UiButton,
    ElementItem,
  },
  props: {
    category: {
      title: String,
      desc: String,
      circles: Number,
      item: {
        background: String,
        border: String,
        shadow: String,
      },
      elements: Array,
    },
  },
};
</script>

<style lang="scss" scoped>
.category {
  border: 1px solid #dfe4ef;
  padding: 13px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.category-left {
  display: flex;
  align-items: center;
}

.category-arrow {
  width: 22px;
  height: 22px;
  border-radius: 50%;
  border: 1px solid #d3d8df;
  margin-right: 14px;
}

.category-title {
  display: inline-block;
  margin-right: 16px;
}

.category-circles {
  display: flex;
  gap: 6px;
  margin-right: 15px;
}

.category-circle {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  flex-shrink: 0;
}

.category-desc {
  font-size: 11px;
  line-height: 108%;
  color: #8e9cbb;
}

.category-controls {
  display: flex;
  align-items: center;
  gap: 20px;
}

.category-button {
  border: none;

  &:last-child {
    cursor: move;
  }

  &:last-child:active {
    cursor: grabbing;
    cursor: -moz-grabbing;
    cursor: -webkit-grabbing;
  }
}

.elements {
  width: calc(100% - 16px);
  margin-left: auto;

  & > .element {
    border-top: 0;

    &:last-child {
      border-bottom: 0;
    }
  }
}
</style>