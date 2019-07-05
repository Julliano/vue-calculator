<template>
    <button class="button" :class="{ double, triple, operation }" @click="$emit('on-calc-clicked', label)">
        {{ label }}
    </button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        label: {},
        operation: {
            type: Boolean
        },
        double: {
            type: Boolean
        },
        triple: {
            type: Boolean
        }
    }
}
</script>

<style lang="scss">
  :root {
    --bg-button: #f0f0f0;
    --border-button: solid 1px #888;
  }
  .button {
    font-size: 1.4em;
    background-color: var(--bg-button);
    border: none;
    border-right: var(--border-button);
    border-bottom: var(--border-button);
    outline: none;
    &:active {
      background-color: #ccc;
    }
    &.double {
      grid-column: span 2;
    }
    &.triple {
      grid-column: span 3;
    }
    &.operation {
      background-color: #fa8231;
      color: #fff;
      &:active {
        background-color: #fa8231cc;
      }
    }
  }
</style>
