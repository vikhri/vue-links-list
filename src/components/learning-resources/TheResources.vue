<template>
  <base-card>
    <base-button @click="setSelectedTab('learning-resources')" :mode="LearnResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="AddResButtonMode">Add new resource</base-button>
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>

import LearningResources from "./LearningResources.vue";
import AddResource from "./AddResource.vue";


export default {
  components: {
    LearningResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'learning-resources',
      storedResources: [
        {
          id:'official-guide',
          title: 'Official Guide',
          description: 'This is official guide',
          link: 'https://vuejs.org',
        },
        {
          id:'google',
          title: 'Google',
          description: 'This is google',
          link: 'https://google.com',
        }
      ]
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource,
      }
  },
  computed: {
    LearnResButtonMode() {
      return this.selectedTab === 'learning-resources' ? null : 'flat';
    },
    AddResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, link) {
      const newResource = {
        id:new Date().toISOString(),
        title: title,
        description: description,
        link: link
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'learning-resources';
    },
    removeResource(resId) {
      const index = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(index, 1);
    },
  }
}
</script>


<!--<learning-resources :resources="storedResources"></learning-resources>-->