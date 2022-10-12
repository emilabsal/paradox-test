
<template>
  <div
    class="category"
    @dragstart="$emit('dragstart', $event, item)"
    @drop="$emit('drop', $event, categoryId)"
  >
    <div class="category-left">
      <ui-button class="category-arrow" icon="chevron" />
      <span class="category-title">{{ category.title }}</span>
      <div class="category-circles" v-if="category.circles">
        <span
          v-for="(item, index) in category.circles"
          :key="index"
          class="category-circle"
          :style="`background-color: ${
            item.background || '#FF238D'
          }; border: 1px solid ${item.border || 'transparent'}; box-shadow: ${
            item.shadow
          };`"
        ></span>
      </div>
      <p class="category-desc" v-if="category.desc">
        {{ category.desc }}
      </p>
    </div>
    <div class="category-controls">
      <ui-button class="category-button" icon="edit" />
      <ui-button class="category-button" icon="delete" />
      <ui-button class="category-button" icon="drag" draggable="true" />
    </div>
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
      circles: Number,
      item: {
        background: String,
        border: String,
        shadow: String,
      },
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
    cursor: grab;
    cursor: -moz-grab;
    cursor: -webkit-grab;
  }

  &:first-child:active {
    cursor: grabbing;
    cursor: -moz-grabbing;
    cursor: -webkit-grabbing;
  }
}
</style>