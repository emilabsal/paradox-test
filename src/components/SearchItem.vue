<template>
  <div class="search">
    <ui-icon class="search-icon" name="search" />
    <input
      class="search-input"
      type="text"
      placeholder="Поиск"
      @input="$emit('input', $event.target.value)"
      ref="input"
    />
    <transition name="slide">
      <div class="search-line"></div>
    </transition>
    <transition name="fade">
      <ui-button
        class="search-close"
        icon="close"
        v-show="close"
        @button-click="emptyValue"
      />
    </transition>
  </div>
</template>

<script>
import UiButton from "@/components/ui/UiButton.vue";
import UiIcon from "@/components/ui/UiIcon.vue";

export default {
  components: {
    UiButton,
    UiIcon,
  },
  props: {
    filtered: Array,
  },
  data() {
    return {
      close: false,
      filteredValue: this.filtered,
    };
  },
  methods: {
    showClose() {
      //   if (this.$refs.input.value !== "") {
      //     this.close = true;
      //   } else {
      //     this.close = false;
      //   }
      // console.log(this.$refs.input.value);
      // this.filteredValue.filter((item) => {
      //   item.title.toLowerCase().indexOf(this.$refs.input.value.toLowerCase()) >
      //     -1;
      // });
    },
    emptyValue() {
      this.$refs.input.value = "";
      this.close = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.search {
  padding-bottom: 12px;
  max-width: 564px;
  display: flex;
  align-items: center;
  position: relative;
  z-index: 1;
}

.search-line {
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  border-bottom: 1px solid #bfc9e0;
  z-index: -1;
  transition: 0.2s;
}

.search-input {
  flex-grow: 1;
}

.search-input:focus ~ .search-line {
  border-bottom: 1px solid #0066ff;
  animation: focus 0.3s linear forwards;
}

@keyframes focus {
  0% {
    width: 0;
  }
  100% {
    width: 100%;
  }
}

.search-icon {
  border: none;
}

.search-close {
  border: none;
}

.search-input {
  border: none;
  outline: none;
  padding: 0 11px;
  font-size: 15px;
  color: #000000;
  line-height: 108%;
}

.search-input::placeholder {
  font-size: 15px;
  color: #8e9cbb;
  line-height: 108%;
  font-style: italic;
}

//transition
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>