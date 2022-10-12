<template>
  <div class="element">
    <span class="element-title">{{ element.title }}</span>
    <span class="element-circle" v-if="element.circle"></span>
    <span class="element-require" v-if="element.require">Обязательный</span>
    <span class="element-status">{{ element.status }}</span>
  </div>
</template>

<script>
export default {
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
</style>