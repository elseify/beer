<script>
  import styles from './Profile.module.scss';

  export default {
    props: [
      'image',
      'name',
      'surname',
      'job',
      'age',
    ],
    data() {
      return {
        styles,
      };
    },
    methods: {
      getYears(value) {
        try {
          return new Date().getFullYear() - new Date(value).getFullYear();
        } catch {
          return 'Unknown';
        }
      },
      srcReplace({ target }) {
        target.src = '/images/placeholder.png';
      },
    },
  };
</script>

<template>
  <div :class="styles.profile">
    <div :class="styles.side">
      <img
        :class="styles.image"
        :width="64"
        :height="64"
        :src="image"
        :alt="image"
        @error="srcReplace($event)"
      >
    </div>
    <div :class="styles.side">
      <div :class="styles.sideItem">
        <div :class="styles.info">
          <span :class="styles.infoText">{{ `${name} ${surname}` }}</span>
        </div>
      </div>
      <div :class="styles.sideItem">
        <div :class="styles.group">
          <div :class="styles.groupItem">
            <div :class="styles.detail">
              <span :class="styles.detailTitle">Age:</span>
              <span :class="styles.detailText">{{ `${getYears(age)} years old` }}</span>
            </div>
          </div>
          <div :class="styles.groupItem">
            <div :class="styles.detail">
              <span :class="styles.detailTitle">Job:</span>
              <span :class="styles.detailText">{{ job }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
