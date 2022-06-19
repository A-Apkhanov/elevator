<template>
  <div class="floor_number">
    <p>
      {{ displayFloor }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'FloorNumberComponent',
  props: {
    floorNumber: Number,
  },
  computed: {
    displayFloor() {
      if ((`${this.floorNumber}`).length === 1) {
        return `0${this.floorNumber}`;
      }
      return `${this.floorNumber}`;
    },
  },
};
</script>

<style scoped>
.floor_number {
  box-sizing: border-box;
  height: 50px;
  width: 50px;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #94d2bd;
  border: 1px solid #005f73;
  border-radius: 5px;
}

.floor_number p {
  margin: 0;
  font-size: 25px;
  color: #005f73;
}
</style>
