<script>
  import styles from './Section.module.scss';

  export default {
    props: [
      'text',
      'items',
    ],
    data() {
      return {
        styles,
      };
    },
  };
</script>

<template>
  <div :class="styles.section">
    <div :class="styles.info">
      <span :class="styles.infoText">{{ text }}</span>
    </div>
    <div :class="styles.list">
      <div :class="styles.listItem" v-for="item in items">
        <slot name="item" v-bind="item" />
      </div>
    </div>
  </div>
</template>
