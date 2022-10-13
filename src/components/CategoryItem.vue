
<template>
  <div
    :class="
      show && category.elements.length !== 0
        ? 'categories-category'
        : 'categories-category categories-border'
    "
  >
    <div class="category">
      <div class="category-left">
        <ui-button
          :class="
            show && category.elements.length !== 0
              ? 'category-arrow-transform'
              : 'category-arrow'
          "
          icon="chevron"
          @click="show = !show"
        />
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
    <transition name="slide">
      <div class="elements" v-show="show" v-if="category.elements.lenght !== 0">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>

<script>
import UiButton from "@/components/ui/UiButton.vue";

export default {
  components: {
    UiButton,
  },
  props: {
    category: {
      title: String,
      desc: String,
      circles: {
        background: String,
        border: String,
        shadow: String,
      },
      elements: Array,
    },
  },
  data() {
    return {
      show: false,
    };
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
  transition: 0.3s;
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

.categories-category + .categories-category {
  border-top: 0;
}

.categories-border:not(:last-child) .category {
  border-bottom: none;
}

.category-desc {
  font-size: 11px;
  line-height: 108%;
  color: #8e9cbb;
}
.category-arrow-transform {
  width: 22px;
  height: 22px;
  border-radius: 50%;
  border: 1px solid #d3d8df;
  margin-right: 14px;
  transform: rotate(180deg);
  transition: 0.3s;
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

.slide-enter-active {
  transition: opacity 0.4s;
}

.slide-leave-active {
  transition: opacity 0.1s;
}

.slide-enter-from,
.slide-leave-to {
  opacity: 0;
}
</style>