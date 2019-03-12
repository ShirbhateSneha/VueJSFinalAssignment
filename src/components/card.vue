<template>
  <div class="card">
    <div class="card-image">
      <img v-bind:src="imgSrc" class="img-responsive" />
    </div>
    <div class="card-header">
      <div class="card-title h5">{{ title }}</div>
      <div class="card-subtitle text-gray">{{ subtitle }}</div>
    </div>
    <div class="card-body">{{ description }}</div>
    <div class="card-footer">
      <!-- <button class="btn btn-primary">...</button> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "gbc-card",
  props: ["title", "title2", "subtitle", "description", "imgSrc"]
};
</script>
