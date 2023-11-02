<template>
  <ul>
    <ResourceItem
        :resources="resources"
        v-for="resource of resources"
        key="resource.id"
        :id="resource.id"
        :title="resource.title"
        :description="resource.description"
        :link="resource.link">
    </ResourceItem>
  </ul>
</template>
<script>
import ResourceItem from "./ResourceItem.vue";

export default {
  components: {
    ResourceItem: ResourceItem
  },
  inject: ["resources"]
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>