<template>
  <component :is="wrapper" :class="['field-group']">
    <label :for="id" v-if="label">{{ label }}</label>
    <textarea
      :type="type"
      :id="id"
      :disabled="disabled"
      :class="state"
      :placeholder="placeholder"
      @input="onInput($event.target.value)"
      @focus="onFocus($event.target.value)"
      v-model="value"
    />
  </component>
</template>

<script>
/**
 * Textareas are used to allow users to provide text input when the expected
 * input is long. Textarea has a range of options. For shorter input,
 * use the `Input` element.
 */
export default {
  name: "fn1-textarea",
  status: "ready",
  release: "1.0.0",
  props: {
    /**
     * The type of input field.
     * `textarea`
     */
    type: {
      type: String,
      default: "textarea",
      validator: value => {
        return value.match(/(textarea)/)
      },
    },
    /**
     * Text value of the form textarea.
     * @model
     */
    value: {
      type: String,
      default: null,
    },
    /**
     * The placeholder value for the form textarea.
     */
    placeholder: {
      type: String,
      default: null,
    },
    /**
     * The label of the form textarea.
     */
    label: {
      type: String,
      default: null,
    },
    /**
     * The html element name used for the wrapper.
     * `div, section`
     */
    wrapper: {
      type: String,
      default: "div",
      validator: value => {
        return value.match(/(div|section)/)
      },
    },
    /**
     * Unique identifier of the form textarea.
     */
    id: {
      type: String,
      default: null,
    },
    /**
     * The width of the form textarea.
     * `auto, expand`
     */
    width: {
      type: String,
      default: "expand",
      validator: value => {
        return value.match(/(auto|expand)/)
      },
    },
    /**
     * Whether the form textarea is disabled or not.
     * `true, false`
     */
    disabled: {
      type: Boolean,
      default: false,
    },
    /**
     * Manually trigger various states of the textarea.
     * `hover, active, focus`
     */
    state: {
      type: String,
      default: null,
      validator: value => {
        return value.match(/(hover|active|focus)/)
      },
    },
  },
  methods: {
    onInput(value) {
      this.$emit("change", value)
    },
    onFocus(value) {
      this.$emit("focus", value)
    },
  },
}
</script>

<style lang="scss">
// Design Tokens with local scope
$color-placeholder: tint($color-silver, 50%);

.field-group {
  @include stack-space($space-s);
  font-weight: $weight-normal;
  font-family: $font-text;
  font-size: $size-m;
  line-height: $line-height-xs;
  width: 100%;

  label {
    cursor: pointer;
    display: block;
    font-size: $size-s;
    color: tint($color-slate, 20%);
    @include stack-space($space-xs);
  }

  textarea {
    @include reset;
    @include inset-squish-space($space-s);
    transition: all 0.2s ease;
    -webkit-appearance: none;
    appearance: none;
    resize: vertical;
    min-height: $space-xxl;
    font-size: $size-m;
    font-family: $font-text;
    background: white;
    border-radius: $radius-default;
    color: set-text-color($color-slate, white);
    width: 100%;
    margin: 0;
    border: 0;
    box-shadow: inset 0 1px 0 0 rgba($color-slate, 0.07), 0 0 0 1px tint($color-slate, 80%);
    &::-webkit-input-placeholder {
      -webkit-font-smoothing: antialiased;
      color: $color-placeholder;
    }
    &:-ms-input-placeholder {
      color: $color-placeholder;
    }
    &::-moz-placeholder {
      color: $color-placeholder;
      -moz-osx-font-smoothing: grayscale;
      opacity: 1;
    }
    &:hover,
    &.hover {
      box-shadow: 0 1px 5px 0 rgba($color-slate, 0.07), 0 0 0 1px tint($color-slate, 60%);
    }
    &:focus,
    &.focus {
      transition: box-shadow 0.2s ease;
      box-shadow: inset 0 0 0 1px $color-bleu-de-france, 0 0 0 1px $color-bleu-de-france;
      outline: 0;
    }
    &[disabled] {
      -webkit-font-smoothing: antialiased;
      box-shadow: 0 0 0 1px tint($color-slate, 80%);
      background: lighten($color-placeholder, 42%);
      color: tint($color-placeholder, 20%);
      cursor: not-allowed;
      opacity: 0.7;
    }
  }
}
</style>

<docs>
  ```jsx
  <div>
    <fn1-textarea label="Default textarea" placeholder="Write your text" id="textarea-1" />
    <fn1-textarea label=":focus" state="focus" placeholder="Write your text" id="textarea-2" />
    <fn1-textarea label="[disabled]" disabled value="Write your text" id="textarea-3" />
  </div>
  ```
</docs>
