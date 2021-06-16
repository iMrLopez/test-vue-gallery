<template>
  <div class="gallery">
    <!-- 3 per row + title + dsc + page title-->
    <div class="container">
      <div v-for="item in items" :key="item.id" class="item">
        <img :src="item.thumbnailUrl" />
        <b-button :v-b-modal="'modal-' + item.id">{{ item.title }}</b-button>
        <b-modal :id="'modal-' + item.id" title="BootstrapVue">
          <img :src="item.url" />
        </b-modal>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Gallery",
  data() {
    return { items: [] };
  },
  beforeCreate() {
    axios
      .get("https://jsonplaceholder.typicode.com/photos")
      .then((response) => {
        if (response.status === 200) {
          this.items = response.data;
        }
      });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gallery {
  padding: 2px;
}

img {
  padding: 5px;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.item {
  width: 32%;
  padding-bottom: 32%; /* Same as width, sets height */
  margin-bottom: 2%; /* (100-32*3)/2 */
  position: relative;
}
</style>
