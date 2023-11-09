<template>
  <div class="dropdown-wrapper" ref="dropDown">
    <div class="dropdown-selected-option" @click="isDropDownVisible = true">
      {{ mappedSelectedOption }}
    </div>
    <div class="options-wrapper" v-if="isDropDownVisible">
      <div
        class="option"
        v-for="(option, index) in props.options"
        :key="index"
        @click="toggleOptionSelect(option)"
      >
        {{ option.name || option }}
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  computed,
  defineProps,
  defineEmits,
  ref,
  onMounted,
  onBeforeUnmount,
} from "vue";

const dropDown = ref(null);

const props = defineProps({
  options: {
    type: Array,
    required: true,
  },
  modelValue: {
    default: null,
  },
});

const emit = defineEmits(["update:modelValue"]);

const selectedOption = ref(null);

const isDropDownVisible = ref(false);

const mappedSelectedOption = computed(() => {
  return selectedOption.value?.name || selectedOption.value || "Choose author";
});

const toggleOptionSelect = (option) => {
  selectedOption.value = option;
  emit("update:modelValue", option);
  isDropDownVisible.value = false;
};

const closeDropDown = (element) => {
  if (!dropDown.value.contains(element.target)) {
    isDropDownVisible.value = false;
  }
};

onMounted(() => {
  window.addEventListener("click", closeDropDown);
});

onBeforeUnmount(() => {
  window.removeEventListener("click", closeDropDown);
});
</script>

<style>
.dropdown-wrapper {
  padding: 16px;
  cursor: pointer;
  max-width: 200px;
  margin: 0 auto;
}

.dropdown-selected-option {
  padding: 16px;
  border: solid 1px #313131;
  border-radius: 8px;
  box-sizing: border-box;
  margin-bottom: 4px;
}

.option:hover {
  background: #c5c5c5;
}

.option {
  padding: 16px;
  border: solid 1px #313131;
  box-sizing: border-box;
}

.option:last-of-type {
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
}
</style>
