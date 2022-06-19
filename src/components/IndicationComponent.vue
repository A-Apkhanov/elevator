<template>
  <div class="elevator-indication">
    <div class="elevator-indication_direction direction">
      <svg
        data-v-049a135c
        viewBox="0 0 1317 1024"
        xmlns="http://www.w3.org/2000/svg"
        width="200"
        height="200"
        class="direction_up"
        :class="{ active: goingUp }"
      >
        <path
          data-v-049a135c
          d="M0 1024 1316.571429 1024 658.285714 0 0 1024Z"
          fill="#cdcdcd"
        />
      </svg>
      <svg
        data-v-049a135c
        viewBox="0 0 1317 1024"
        xmlns="http://www.w3.org/2000/svg"
        width="200"
        height="200"
        class="direction_down"
        :class="{ active: goingDown }"
      >
        <path
          data-v-049a135c
          d="M0 0 1316.571429 0 658.285714 1024 0 0Z"
          fill="#cdcdcd"
        />
      </svg>
    </div>
    <div class="elevator-indication_floor-info floor-info">
      <p class="floor-info_number">
        {{ displayFloor }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndicationComponent',
  props: {
    floor: Number,
    goingUp: Boolean,
    goingDown: Boolean,
  },
  computed: {
    displayFloor() {
      if ((`${this.floor}`).length === 1) {
        return `0${this.floor}`;
      }
      return `${this.floor}`;
    },
  },
};
</script>

<style scoped>
.elevator-indication {
  display: inline-flex;
  gap: 10px;
  padding: 5px 10px;
  margin: 5px;
  border-radius: 15px;
  background-color: #ca6702;
}
.direction {
  display: flex;
  flex-direction: column;
  gap: 2px;
}
.direction_up, .direction_down {
  height: 25px;
  width: auto;
}
.direction_up path, .direction_down path {
  fill: #e9d8a6;
}
.active path {
  fill: #ae2012;
}
.floor-info {
  display: inline-flex;
  align-items: center;
}
.floor-info_number {
  color: #005f73;
  font-size: 35px;
  margin: 0;
}
</style>
