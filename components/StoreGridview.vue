<template>
  <div class="storegrid">
    <transition-group name="items" tag="section" class="content">
      <div v-for="item in filteredprice" :key="item.id" class="item">
        <div class="img-contain">
          <NuxtLink :to="`product/${item.id}`">
            <img :src="`${item.img}`" />
          </NuxtLink>
        </div>
        <star-rating
          :rating="item.star_rating"
          active-color="#d57eeb"
          :star-size="15"
          :show-rating="false"
          style="margin: 5px 0"
        ></star-rating>
        <h3>{{ item.name }}</h3>
        <h4 class="price"> XAF {{ item.price }}</h4>
        <NuxtLink :to="`product/${item.id}`">
          <button class="view-item">View</button>
        </NuxtLink>
      </div>
    </transition-group>
    <aside>
      <h3>Special Sale</h3>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam libero iusto nemo laboriosam perferendis voluptas ullam officiis, quibusdam quas quam eveniet est fugit delectus corporis incidunt nam esse suscipit itaque?</p>
      <h3>Filter by Price:</h3>
      <p style="margin-top: 5px">
        Max Price
        <strong>XAF {{ pricerange }}</strong>
      </p>
      <input
        class="slider"
        id="pricerange"
        type="range"
        v-model="pricerange"
        :min="min"
        :max="max"
        step="0.1"
      />
      <span class="min">XAF {{ min }}</span>
      <span class="max">XAF {{ max }}</span>
    </aside>
  </div>
</template>

<script>
import StarRating from "vue-star-rating/src/star-rating.vue";

export default {
  props: {
    data: {
      required: true
    }
  },
  data() {
    return {
      min: 0,
      max: 2000,
      pricerange: 60000
    };
  },
  computed: {
    filteredprice() {
      return this.data.filter(el => el.price < this.pricerange);
    }
  },
  components: {
    StarRating
  }
};
</script>

<style lang="scss" scoped>
.content {
  height: 100%;
  width: 100%;
 
}

.img-contain {
  max-height: 200px;
  display: flex;
  align-content: center;
  align-items: center;
  img {
    width: 100%;
  }
}
.view-item{
 border: none;
  width:100px;
  padding:10px 20px;
  border-radius: 10px;
  &:hover{
    background-color: #d57eeb;
  }
}
.item {
  max-height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 20px 0;
}

aside {
  height: 100%;
  width: 100%;
}

.max {
  display: inline-block;
  float: right;
}
</style>