<template>
  <label :class="classes">
    <slot></slot>
    <input type="checkbox" :checked="status" :value="value" @change="_change" :disabled="disabled"/>
    <span></span>
  </label>
</template>
<style>
  label {
    -moz-user-select:none;
    -webkit-user-select:none;
    user-select:none;
  }
</style>
<script>
  export default {
    name: 'Checkbox',
    data () {
      return {
        status: false
      }
    },
    props: {
      value: null,
      checked: {type: Boolean, default: false},
      disabled: {type: Boolean},
      outline: {type: Boolean}
    },
    model: {
      prop: 'checked',
      event: 'check'
    },
    computed: {
      classes () {
        return [
          {'mt-checkbox': true},
          {'mt-checkbox-outline': !!this.outline}
        ]
      }
    },
    watch: {
      checked () {
        this.status = this.checked
      }
    },
    created () {
      this.status = this.checked
    },
    methods: {
      _change (e) {
        this.status = e.target.checked
        this.$emit('check', e.target.checked)
      }
    }
  }
</script>
