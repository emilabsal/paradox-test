<template>
  <div class="element">
    <div class="element-left">
      <span class="element-title">{{ element.title }}</span>
      <span class="element-circle" v-if="element.circle"></span>
      <span class="element-require" v-if="element.require">Обязательный</span>
      <span class="element-status">{{ element.status }}</span>
    </div>
    <div class="element-controls">
      <ui-button class="element-button" icon="edit" />
      <ui-button class="element-button" icon="delete" />
      <ui-button class="element-button element-button-drag" icon="drag" />
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
    element: {
      title: String,
      circle: {
        type: Boolean,
        default: false,
      },
      require: {
        type: Boolean,
        default: false,
      },
      status: String,
    },
  },
};
</script>

<style lang="scss" scoped>
.element {
  border: 1px solid #dfe4ef;
  padding: 9px 11px;
  padding-right: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  background-color: #fff;
}

.element-title {
  display: inline-block;
  font-size: 13px;
  line-height: 108%;
}

.element-circle {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  display: inline-block;
  margin-left: 20px;
  background: #00c2ff;
  flex-shrink: 0;
}

.element-require {
  font-size: 11px;
  line-height: 108%;
  color: #ff238d;
  display: inline-block;
  margin-left: 15px;
}

.element-status {
  font-size: 11px;
  line-height: 108%;
  display: inline-block;
  margin-left: 16px;
  color: #8e9cbb;
}

.element-controls {
  display: flex;
  align-items: center;
  gap: 20px;
}

.element-button {
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

.categories-category:last-child .element:last-child {
  border-bottom: 1px solid #dfe4ef;
}
</style>