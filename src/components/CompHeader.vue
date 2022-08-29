<template>
  <div id="comp-header">
    <p>{{ firstText }}</p>
    <p>{{ secondText }}</p>
  </div>
</template>
<script>
export default {
  name: "CompHeader",
  props: {
    firstText: String,
    secondText: String,
  },
};
</script>
<style scoped>
#comp-header {
  display: flex;
  padding: 50px 99px 50px 56px;
  width: 100%;
  height: 140px;
  background: #333333;
  align-items: center;
  justify-content: start;
  gap: 30px;
}
#comp-header p:nth-child(1) {
  font-weight: 700;
  font-size: 48px;
  line-height: 56px;
  color: #ffffff;
}
#comp-header p:nth-child(2) {
  font-weight: 300;
  font-size: 32px;
  line-height: 38px;
  color: #ffffff;
}
</style>
