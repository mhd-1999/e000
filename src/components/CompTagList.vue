<template>
  <div class="select-point">
    <button
      v-for="point in pointArr"
      :key="point.code"
      @click="deletePoint(point.code)"
    >
      <p>{{ point }}</p>
      <img :src="iconClose" />
    </button>
  </div>
</template>

<script>
import iconClose from "../assets/X.png";
export default {
  name: "TagList",
  props: {
    pointArr: Array,
  },
  data() {
    return {
      iconClose: iconClose,
    };
  },
  methods: {
    deletePoint(index) {
      this.$emit("deletePoint", { index });
    },
  },
};
</script>

<style scoped>
.select-point {
  max-width: 354px;
  display: flex;
  flex-wrap: wrap;
}
.select-point button {
  display: flex;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  padding: 4px 8px;
  margin: 5px;
  gap: 8px;
  background: #f0f4f8;
  border: 1px solid #dcdcdc;
  color: #627d98;
  border-radius: 4px;
  height: 32px;
}
.select-point button img {
  width: 14px;
  height: 14px;
}
</style>
