<template>
  <div id="search">
    <div :class="[isFocused ? 'input active':'input']">
      <label for="input-search">
        <img :src="iconSearch" alt="">
      </label>
      <div class="select-point">
          <button
            v-for="(point, index) in pointArr"
            :key="index"
            @click="deletePoint(index)"
          >
          <p>{{point}}</p><img :src="iconClose">
          </button>
      </div>
      <input id="input-search" type="text" v-model="searchValue" :placeholder="placeHolder" @blur="handleBlurInput" @focus="handleFocusInput"/>
    </div>
    <div class="list">
      <li
        v-for="point in getPointList"
        :key="point.code"
        @click="pointArr.push(point.name)"
      >
        <p v-if="point.name.includes('Tỉnh')">{{point.name.replace('Tỉnh','')}}</p>
      </li>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import iconSearch from '../assets/Combined ShapeSearch.png';
import iconClose from '../assets/X.png';
export default {
  name: "InputSearch",
  props: {
    placeHolder: String,
  },
  data() {
    return {
      searchValue: "",
      points: [],
      pointArr: [],
      isFocused: null,
      iconSearch:iconSearch,
      iconClose:iconClose,
    };
  },
  created() {
    axios
      .get("https://provinces.open-api.vn/api/")
      .then((res) => {
        this.points = res.data;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    deletePoint(index) {
      this.pointArr.splice(index, 1);
    },
    handleFocusInput(){
      return this.isFocused=true;
    },
    handleBlurInput(){
      return this.isFocused=false;
    }
  },
  computed: {
    getPointList() {
      if (this.searchValue) {
        return this.points.filter((point) =>
          point.name.toLowerCase().match(this.searchValue.toLowerCase())
        );
      } else if (!this.searchValue) {
        return [];
      }
      return [];
    },
  },
};
</script>
<style scoped>
#search {
  padding-top: 168px;
}
#search input {
  max-width: 300px;
  min-width: 150px;
  padding: 14.5px 10px;
  border: none;
  font-size: 14px;
  background: rgba(230, 249, 255, 0.2);
}
#search input:focus {
  outline: none;
}
#search .list {
  display: flex;
  margin: 0 auto;
  justify-content: center;
  flex-wrap: wrap;
  width: 400px;
  list-style: none;
  background: #F1F5F8;
  filter: drop-shadow(0px 1px 8px rgba(102, 102, 102, 0.25));
  border-radius: 4px;
}
.list li {
  width: 100%;
  padding: 8px 0 8px 10px;
  font-size: 16px;
  line-height: 23px;
  color: #486581;
  text-align: start;
}
.list li:hover {
  color: #FFFFFF;
  background-color: #617D98;
}
.input{
  width: 400px;
  height: 100%;
  border: 1px solid #DBDBDB;
  border-radius: 4px;
  display: flex;
  flex-wrap:wrap;
  align-items: center;
  margin: 0 auto;
}
.input label{
  padding: 15.5px 13px;
}
.select-point{
  max-width: 354px;
  display: flex;
  flex-wrap:wrap;
}
.select-point button{
  display: flex;
  flex-wrap:nowrap;
  justify-content: center;
  align-items: center;
  padding: 4px 8px;
  margin: 5px;
  gap: 8px;
  background: #F0F4F8;
  border: 1px solid #DCDCDC;
  color: #627D98;
  border-radius: 4px;
  height: 32px;
}
.select-point button img{
  width: 14px;
  height: 14px;
}
.active{
  border:1px solid #1991D2;
}
</style>