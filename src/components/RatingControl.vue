<template>
  <ul>
    <li
      v-for="item in ratingButtons"
      :key="item"
      :class="{ active: modelValue.includes(item) }"
    >
      <button
        @click="activate(item)"
        type="button"
      >{{ item }}</button>
    </li>
  </ul>
</template>

<script>
  export default {
    name: 'RatingControl',
    props: ['modelValue'],
    emits: ['update:modelValue'],

    data() {
      return {
        optionsArray: this.modelValue,
        ratingButtons: ['Extra bed', 'Animals', 'Child'],
      }
    },

    methods: {
      activate(option) {
        if (!this.optionsArray.includes(option)) {
          this.optionsArray.push(option);
        } else {
          const index = this.optionsArray.findIndex(el => option === el );
          this.optionsArray.splice(index, 1);
        }

        this.$emit('update:modelValue', this.optionsArray);
      },
    },
  }
</script>

<style scoped>
  .active {
    border-color: #d127d1;
  }

  .active button {
    color: #d127d1;
  }

  ul {
    display: flex;
    list-style: none;
    margin: 0.5rem 0;
    padding: 0;
  }

  li {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 1rem;
    border: 1px solid #ccc;
    padding: 1rem;
  }

  button {
    font: inherit;
    border: none;
    background-color: transparent;
    cursor: pointer;
  }
</style>
