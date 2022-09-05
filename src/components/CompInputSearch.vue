<template>
  <div id="search">
    <div :class="[isFocused ? 'input active' : 'input']">
      <label for="input-search">
        <img :src="iconSearch" alt="" />
      </label>
      <TagList
        :pointArr="pointArr"
        @deletePoint="deletePoint($event)"
      ></TagList>
      <input
        id="input-search"
        type="text"
        :value="searchValue"
        :placeholder="placeHolder"
        @blur="handleBlurInput"
        @focus="handleFocusInput"
        @input="onInputSearchValue"
      />
    </div>
    <ListItem
      :getPointList="getPointList"
      @addToArray="addToArray($event)"
    ></ListItem>
  </div>
</template>
<script>
import ListItem from "./CompListItem.vue";
import TagList from "./CompTagList.vue";
import iconSearch from "../assets/Combined ShapeSearch.png";

export default {
  name: "InputSearch",
  props: {
    placeHolder: String,
    getPointList: Array,
    searchValue: String,
  },
  components: {
    ListItem,
    TagList,
  },
  data() {
    return {
      searchText: "",
      pointArr: [],
      isFocused: null,
      iconSearch: iconSearch,
    };
  },
  methods: {
    onInputSearchValue(e) {
      const searchText = e.target.value;
      this.$emit("update:searchValue", searchText);
    },
    deletePoint(index) {
      this.pointArr.splice(index, 1);
    },
    handleFocusInput() {
      this.isFocused = true;
    },
    handleBlurInput() {
      this.isFocused = false;
    },
    addToArray(point) {
      this.pointArr.push(point.name);
    },
    getListCity() {
      this.$emit("getListCity");
    },
  },
};
</script>
<style scoped>
#search {
  padding-top: 168px;
}
#search input {
  max-width: 100%;
  min-width: 30%;
  flex: 70%;
  padding: 14.5px 10px;
  border: none;
  font-size: 14px;
  background: rgba(230, 249, 255, 0.2);
}
#search input:focus {
  outline: none;
}
.input {
  width: 400px;
  height: 100%;
  border: 1px solid #dbdbdb;
  border-radius: 4px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  margin: 0 auto;
}
.input label {
  padding: 15.5px 13px;
}
.active {
  border: 1px solid #1991d2;
}
</style>
