<template>
  <div
    @click="onFocused"
    :class="{'border-blue-500': focused}"
    class="p-2 border border-solid rounded flex items-center justify-center"
  >
    <!-- Search icon -->
    <search-icon class="h-4 mx-2" />

    <!-- Placeholder -->
    <span
      v-show="!focused"
      class="text-gray-400"
    >
      Название или автор
    </span>

    <!-- Input field -->
    <input
      ref="input"
      v-show="focused"
      v-model.trim="value"
      @input="onValueChanged"
      @blur="onBlur"
      class="w-full mx-2"
    >
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'

@Component
class BookshelfFilter extends Vue {
  private value:string = '';
  private focused:boolean = false;

  private onValueChanged() {
    this.$emit('input', this.value)
  }

  private onFocused() {
    this.focused = true
    this.$nextTick(function () {
      (this.$refs.input as HTMLInputElement).focus()
    })
  }

  private onBlur() {
    this.focused = (this.value !== '')
  }
}

export default BookshelfFilter
</script>
