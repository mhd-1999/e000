<template>
  <div id="input-search">
    <div class="input">
      <div class="select-point d-flex">
        <li
          v-for="(point, index) in pointArr"
          :key="index"
          @click="deletePoint(index)"
        >{{point}}
        </li>
      </div>
      <input :class="[active ? 'isActive' :'']" type="text" v-model="searchValue" :placeholder="placeHolder" />
    </div>
    <div class="list">
      <li
        v-for="point in getPointList"
        :key="point.code"
        @click="pointArr.push(point.name)"
      >
        {{ point.name }}
      </li>
    </div>
    </div>
</template>

<script>
import axios from "axios";
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
      active: false
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
      console.log(typeof(this.pointArr.length));
    },
    activeInput(){
      if(this.pointArr.length){
        return !this.active;
      }
      console.log(this.pointArr.length);
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
.d-flex{
  display: flex;
}
.nowrap{
  flex-wrap: nowrap;
}
#input-search {
  padding-top: 168px;
}
#input-search input {
  position: relative;
  width: 400px;
  padding: 14.5px 10px;
  border: 1px solid #dbdbdb;
  border-radius: 4px;
  font-size: 14px;
  background: rgba(230, 249, 255, 0.2);
}
#input-search input:focus {
  outline: none;
  border: 1px solid #1991d2 !important;
}
#input-search .list {
  display: flex;
  margin: 0 auto;
  justify-content: center;
  flex-wrap: wrap;
  width: 400px;
  list-style: none;
  background: #f1f5f8;
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
  color: #ffffff;
  background-color: #617d98;
}
.input .select-point{
  flex-wrap: wrap;
  width: 60%;
}
.isActive{
  border-color:red !important;
}
/* button {
  position: absolute;
} */
</style>
