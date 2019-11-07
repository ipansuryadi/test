<template>
  <div>
    <Header @sort-by-color="sortByColor" @sort-by-city="sortByCity" />
    <Container :position="lastPosition">
      <List :list="peoples" />
    </Container>
  </div>
</template>

<script>
import Header from "~/components/Header";
import Container from "~/components/Container";
import List from "~/components/List";

export default {
  data() {
    return {
      peoples: [],
      lastPosition: 0
    };
  },
  components: {
    Header,
    Container,
    List
  },
  methods: {
    async fetchPeoples() {
      const res = await this.$axios.$get("?results=100");
      this.peoples = await res.results;
      await this.addColorToPeople(this.peoples);
      await this.scrollToPosition();
    },
    addColorToPeople(peoples) {
      peoples.forEach(people => {
        const { age } = people.dob;
        if (age < 21) {
          people.color = "red";
        } else if (age >= 21 && age < 56) {
          people.color = "green";
        } else {
          people.color = "blue";
        }
      });
    },
    sortByCity() {
      this.peoples.sort((a, b) => {
        const cityA = a.location.city.toUpperCase();
        const cityB = b.location.city.toUpperCase();
        return cityA < cityB ? -1 : cityA > cityB ? 1 : 0;
      });
    },
    sortByColor() {
      const order = ["green", "blue", "red"];
      this.peoples.sort((a, b) => {
        return order.indexOf(a.color) - order.indexOf(b.color);
      });
    },
    scrollToPosition() {
      this.lastPosition = localStorage.getItem("scrollPosition");
    }
  },
  mounted() {
    this.fetchPeoples();
  }
};
</script>