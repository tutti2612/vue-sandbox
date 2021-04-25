<template>
  <div class="status-select">
    <button class="status-select-btn" @click="isOpen = !isOpen">
      {{ seletedOptionLabel || placeholder }}
    </button>
    <ul class="status-select-list" :class="{ open: isOpen }">
      <li
        v-for="option in options"
        :key="option.label"
        @click="handleClick(option)"
      >
        {{ option.label }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue, { PropType } from "vue";

interface option {
  label: string;
  value: string;
  isSelected: boolean;
}

export default Vue.extend({
  props: {
    options: {
      type: Array as PropType<option[]>,
      required: true
    },
    placeholder: {
      type: String,
      default: "選択してください"
    }
  },
  data() {
    return {
      isOpen: false,
      seletedOptionLabel: ""
    };
  },
  created() {
    const selectedOption = this.options.find((option) => option.isSelected);
    this.seletedOptionLabel = selectedOption ? selectedOption.label : "";
  },
  mounted() {
    document.addEventListener("click", (event) => {
      if (!(event.target as Element).closest(".status-select")) {
        this.isOpen = false;
      }
    });
  },
  methods: {
    handleClick(option: option) {
      this.isOpen = false;
      this.seletedOptionLabel = option.label;
    }
  }
});
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

.status-select {
  position: relative;
  width: 200px;

  &-btn {
    border: 1px solid black;
    background-color: white;
    cursor: pointer;
    width: 200px;
    height: 50px;
    outline: none;
    font-size: inherit;
  }

  &-list {
    display: none;
    list-style: none;
    padding: 0;
    width: 200px;
    position: absolute;
    top: 50px;
    margin: 0;

    li {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 50px;
      cursor: pointer;
      border: 1px solid black;
      border-top: none;
    }
  }

  .open {
    display: block;
  }
}
</style>
