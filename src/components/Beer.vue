<script>
  import styles from './Beer.module.scss';

  export default {
    props: [
      'name',
    ],
    data() {
      return {
        styles,
      };
    },
  };
</script>

<template>
  <div :class="styles.beer">
    <span :class="styles.text">{{ name }}</span>
  </div>
</template>
