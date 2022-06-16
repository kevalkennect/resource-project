<template>
  <ul>
    <resource-item
      v-for="res in resources"
      :key="res.id"
      :id="res.id"
      :description="res.description"
      :title="res.title"
      :link="res.link"
    >
    </resource-item>
  </ul>
</template>

<script>
import ResourceItem from './ResourceItem.vue';

export default {
  inject: ['resources'],
  components: {
    ResourceItem,
  },
};
</script>

<style>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>