<script>
  import Section from './components/Section.vue';
  import Profile from './components/Profile.vue';
  import Beer from './components/Beer.vue';

  import styles from './App.module.scss';

  export default {
    data() {
      return {
        styles,
        isInit: false,
        user: {
          data: null,
        },
        beer: {
          data: null,
        },
      };
    },
    async mounted() {
      await this.fetchData('https://random-data-api.com/api/users/random_user', this.user);
      await this.fetchData('https://random-data-api.com/api/beer/random_beer?size=6', this.beer);

      this.isInit = true;
    },
    methods: {
      async fetchData(url, obj) {
        try {
          const response = await fetch(url);

          if (response.ok) {
            obj.data = await response.json();
          }
        } catch (error) {
          console.log(error);
        }
      },
    },
    components: {
      Section,
      Profile,
      Beer,
    },
  };
</script>

<template>
  <div class="container" v-if="isInit">
    <div :class="styles.layout">
      <div :class="styles.layoutItem">
        <Profile
          :image="user.data.avatar"
          :name="user.data.first_name"
          :surname="user.data.last_name"
          :job="user.data.employment.title"
          :age="user.data.date_of_birth"
        />
      </div>
      <div :class="styles.layoutItem">
        <Section text="Recommended beer:" :items="beer.data">
          <template #item="item">
            <Beer :name="item.name" />
          </template>
        </Section>
      </div>
    </div>
  </div>
</template>
