<template>
  <div class="pho-switch-wrapper">
    <div v-if="label && !inline">
      <label :for="id.unique" class="pho-label">
        {{ label }}
      </label>
    </div>
    <div class="pho-switch-container">
      <div class="pho-switch">
        <input
          type="checkbox"
          :id="id.unique"
          :checked="modelValue"
          :value="modelValue"
          @input="onInput"
          :name="name"
          :cy="id.family" />
        <label :for="id.unique" class="pho-switch-circle"></label>
      </div>
      <label v-if="label && inline" :for="id.unique" class="pho-switch-text">{{ label }}</label>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import { useId, componentProps } from '~/src/vue/components/shared';
import { getFormProps } from '~/src/vue/components/ui/forms/forms';

export default defineComponent({

  props: {
    ...componentProps,
    ...getFormProps(Boolean),
    inline: {
      type: Boolean,
      default: () => false,
    },
  },

  setup(props, context) {
    const onInput = ($event: InputEvent) => {
      const target = $event.target as HTMLInputElement;

      return context.emit('update:modelValue', target.checked);
    };

    return {
      id: useId('field', props),
      onInput,
    };
  },

});
</script>
