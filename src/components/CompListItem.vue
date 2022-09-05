<template>
  <div class="list">
    <li
      v-for="point in getPointList"
      :key="point.code"
      @click="addToArray(point)"
    >
      <p v-if="point.name.includes('Tỉnh')">
        {{ point.name.replace("Tỉnh", "") }}
      </p>
      <p v-else-if="point.name.includes('Thành phố')">
        {{ point.name.replace("Thành phố ", "") }}
      </p>
    </li>
  </div>
</template>
<script>
export default {
  name: "ListItem",
  props: {
    getPointList: Array,
  },
  methods: {
    addToArray(point) {
      this.$emit("addToArray", point);
    },
  },
};
</script>

<style scoped>
.list {
  display: flex;
  margin: 0 auto;
  justify-content: center;
  flex-wrap: wrap;
  width: 400px;
  list-style: none;
  background: #f1f5f8;
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
  color: #ffffff;
  background-color: #617d98;
}
</style>
