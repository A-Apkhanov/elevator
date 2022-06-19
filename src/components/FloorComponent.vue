<template>
  <div class="floor">
    <div class="floor_header">
      <slot name="floor-header" />
    </div>
    <div class="floor_content">
      <slot name="floor-content" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'FloorComponent',
};
</script>

<style scoped>
.floor {
  display: flex;
  flex-direction: column;
  gap: 10px;
  box-sizing: border-box;
  width: calc(100% - 10px);
  height: 200px;
  padding: 10px;
  margin: 5px;
  background-color: #edede9;
  border-radius: 5px;
}
.floor_content {
  display: flex;
  flex: 1 1 auto;
  align-items: center;
}
</style>
