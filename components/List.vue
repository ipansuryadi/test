<template>
  <div>
    <div class="item" v-for="(item,index) in list" :key="index" :style="{background:item.color}">
      <div class="item-content">
        <div class="image-container">
          <div class="image-frame">
            <img class="photo" :src="item.picture.thumbnail" />
          </div>
        </div>
        <div class="desc-container">
          <div class="item-title">{{displayName(item)}}</div>
          <div class="item-age">{{item.dob.age}}</div>
          <div class="item-address">{{displayAddress(item)}}</div>
          <div class="item-email-mobile-only">{{item.email}}</div>
        </div>
      </div>
      <div class="item-address-mobile-only">{{displayAddress(item)}}</div>
      <div class="item-email">{{item.email}}</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      currentPage: 1,
      perPage: 10,
      totalData: 100
    };
  },
  name: "List",
  props: ["list"],
  methods: {
    displayName(item) {
      const { title, first, last } = item.name;
      return `${title}, ${first}, ${last}`;
    },
    displayAddress(item) {
      const { city, state, postcode } = item.location;
      return `${city}, ${state}, ${postcode}`;
    }
  },
  mounted() {}
};
</script>