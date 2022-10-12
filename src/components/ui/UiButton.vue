<template>
  <button class="button" @click="$emit('buttonClick')">
    <ui-icon :name="icon" :width="width" :height="height" :fill="fill" />
    {{ name }}
  </button>
</template>

<script>
import UiIcon from "@/components/ui/UiIcon.vue";

export default {
  components: {
    UiIcon,
  },
  props: {
    name: String,
    icon: String,
    width: Number,
    height: Number,
    fill: String,
  },
};
</script>

<style lang="scss" scoped>
.button {
  background: transparent;
  outline: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  flex-shrink: 0;
}
</style>