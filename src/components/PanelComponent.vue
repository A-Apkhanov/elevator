<template>
  <div class="floor-panel">
    <svg
      data-v-049a135c
      viewBox="0 0 1317 1024"
      xmlns="http://www.w3.org/2000/svg"
      width="200"
      height="200"
      class="direction_up"
      :class="{
        active: isActiveRequest && !isDoubleRequest,
        double: isDoubleRequest,
      }"
    >
      <path
        data-v-049a135c
        d="M0 1024 1316.571429 1024 658.285714 0 0 1024Z"
        fill="#cdcdcd"
      />
    </svg>
    <button
      class="floor-panel_button call-button"
    />
    <svg
      data-v-049a135c
      viewBox="0 0 1317 1024"
      xmlns="http://www.w3.org/2000/svg"
      width="200"
      height="200"
      class="direction_down"
      :class="{
        active: isActiveRequest && !isDoubleRequest,
        double: isDoubleRequest,
      }"
    >
      <path
        data-v-049a135c
        d="M0 0 1316.571429 0 658.285714 1024 0 0Z"
        fill="#cdcdcd"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'PanelComponent',
  props: {
    isActiveRequest: Boolean,
    isDoubleRequest: Boolean,
  },
};
</script>

<style scoped>
.floor-panel {
  display: flex;
  flex-direction: column;
  width: 30px;
  padding: 10px;
  border-radius: 5px;
  gap: 5px;
  align-items: center;
  background-color: #0a9396;
}
.call-button {
  display: inline-block;
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background-color: #ca6702;
}
.call-button:hover {
  cursor: pointer;
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
.double path {
  fill: #ff0054
}
</style>
