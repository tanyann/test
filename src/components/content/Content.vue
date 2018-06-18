<template src="./Content.html"></template>

<script>
  import {mapState} from 'vuex';
  import router from '../../router';

  export default {
    name: "Content",
    computed: {
      ...mapState([
        'data',
        'city',
        'category',
      ]),
      filteredData() {
        let citySelected = parseInt(this.$route.query.city),
            categories = this.$route.query.categories,
            priceFrom = parseInt(this.$route.query.priceFrom),
            priceTo = parseInt(this.$route.query.priceTo),
            categoriesSelected = [];

        if (!citySelected && !categories && !priceFrom && !priceTo)
          return this.data;

        if (categories) {
          categories = categories.split(',');
          categories.forEach((item) => {
            categoriesSelected.push(parseInt(item));
          });
        }

        this.$store.commit('UPDATE_CATEGORIES_SELECTED', categoriesSelected);
        this.$store.commit('UPDATE_CITY_SELECTED', citySelected);

        let filtered = this.data;

        if (citySelected) {
          filtered = filtered.filter(item => {
            return citySelected === item.city;
          });
        }

        if (categoriesSelected.length) {
          filtered = filtered.filter(item => {
            return categoriesSelected.includes(item.category)
          });
        }

        filtered = filtered.filter(item => {
          return item.price >= priceFrom && item.price <= priceTo
        });

        return filtered;
      }
    },
    methods: {},
    comments: {
      router,
    }
  }
</script>

<style src="./Content.scss" lang="scss"></style>
