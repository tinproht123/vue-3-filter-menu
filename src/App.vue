<template>
  <div id="app" class="container">
    <h1 class="text-center mt-5 mb-3">Our Menu</h1>
    <div class="mx-auto d-block text-center mb-5">
      <button
        v-for="(link, index) in links"
        :key="index"
        class="btn btn-outline-warning border-3 mx-2"
        @click="filteredMenu(link)"
      >
        {{ link }}
      </button>
    </div>
    <section class="row">
      <article
        v-for="item in currentMenu"
        class="row col-lg-6 g-0 border my-2"
        :key="item.id"
      >
        <img :src="item.img" :alt="item.title" class="col-md-6" />
        <div class="row col-md-6 g-0 p-2">
          <div class="d-flex justify-content-between">
            <h5>{{ item.title }}</h5>
            <p>${{ item.price }}</p>
          </div>
          <p>{{ item.desc }}</p>
        </div>
      </article>
    </section>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import data from './data';

export default {
  name: 'App',
  setup() {
    //original array
    const menu = ref(data);
    //links (or category)
    const links = ref(['all', 'breakfast', 'lunch', 'shakes']);

    //make a copy of original menu array. so filter array will not mutating the origianl
    const currentMenu = ref([]);

    //Declare current menu
    currentMenu.value = menu.value;

    //filter menu on click
    function filteredMenu(category) {
      if (category === 'all') {
        return (currentMenu.value = menu.value);
      }
      return (currentMenu.value = menu.value.filter((item) =>
        item.category.match(category)
      ));
    }

    return {
      menu,
      links,
      filteredMenu,
      currentMenu,
    };
  },
};
</script>
