<template>
  <div id="app">
    <comp-header firstText="入力欄" secondText="Input Field" />
    <comp-input-search
      placeHolder="Nhập tên thành phố để tìm kiếm..."
      :getListCity="getListCity"
      :searchValue.sync="searchValue"
      :getPointList="getPointList"
    />
  </div>
</template>

<script>
import axios from "axios";
import CompHeader from "./components/CompHeader.vue";
import CompInputSearch from "./components/CompInputSearch.vue";
import { CITY_API } from "../src/data/constants";
export default {
  name: "App",
  components: {
    CompHeader,
    CompInputSearch,
  },
  data() {
    return {
      points: [],
      searchValue: "",
    };
  },
  methods: {
    async getListCity() {
      try {
        const res = await axios.get(CITY_API);
        this.points = res.data;
      } catch (err) {
        console.log(err);
      }
    },
  },
  computed: {
    getPointList() {
      const searchValue = this.searchValue;
      if (searchValue) {
        return this.points.filter((point) =>
          point.name.toLowerCase().match(searchValue.toLowerCase())
        );
      }
      return [];
    },
  },
  created() {
    this.getListCity();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
