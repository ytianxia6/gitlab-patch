<script>
  import { s__ } from '../../locale';
  import icon from './icon.vue';

  const ICON_ON = 'status_success_borderless';
  const ICON_OFF = 'status_failed_borderless';
  const LABEL_ON = s__('ToggleButton|Toggle Status: ON');
  const LABEL_OFF = s__('ToggleButton|Toggle Status: OFF');

  export default {
    components: {
      icon,
    },

    model: {
      prop: 'value',
      event: 'change',
    },

    props: {
      name: {
        type: String,
        required: false,
        default: null,
      },
      value: {
        type: Boolean,
        required: false,
        default: null,
      },
      disabledInput: {
        type: Boolean,
        required: false,
        default: false,
      },
      isLoading: {
        type: Boolean,
        required: false,
        default: false,
      },
    },

    computed: {
      toggleIcon() {
        return this.value ? ICON_ON : ICON_OFF;
      },
      ariaLabel() {
        return this.value ? LABEL_ON : LABEL_OFF;
      },
    },

    methods: {
      toggleFeature() {
        if (!this.disabledInput) this.$emit('change', !this.value);
      },
    },
  };
</script>

<template>
  <label class="toggle-wrapper">
    <input
      v-if="name"
      :name="name"
      :value="value"
      type="hidden"
    />
    <button
      :aria-label="ariaLabel"
      :class="{
        'is-checked': value,
        'is-disabled': disabledInput,
        'is-loading': isLoading
      }"
      type="button"
      class="project-feature-toggle"
      @click="toggleFeature"
    >
      <gl-loading-icon class="loading-icon" />
      <span class="toggle-icon">
        <icon
          :name="toggleIcon"
          css-classes="toggle-icon-svg"/>
      </span>
    </button>
  </label>
</template>
