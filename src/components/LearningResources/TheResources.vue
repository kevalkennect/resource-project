<template>
  <base-card>
    <base-button @click="selectTab('stored-resources')" :mode="activeButtonRes">
      Stored Resources</base-button
    >
    <base-button @click="selectTab('add-resources')" :mode="activeButtonAdd">
      Add Resources
    </base-button>
    <keep-alive>
      <component :is="selectedTab"> </component>
    </keep-alive>
  </base-card>
</template>

<script>
import AddResources from './AddResources.vue';
import StoredResources from './StoredResources.vue';

export default {
  components: {
    StoredResources,
    AddResources,
  },
  computed: {
    activeButtonRes() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    activeButtonAdd() {
      return this.selectedTab === 'add-resources' ? null : 'flat';
    },
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'officialguide',
          title: 'Official Guide',
          description: 'ldskljnfdjskf',
          link: 'https://google.com',
        },
        {
          id: 'asdfdasfsdf',
          title: 'Official Guide',
          description: 'ldskljnfdjskf',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResourcesDB: this.addResourcesToDB,
      deleteResource: this.removeResource,
    };
  },
  methods: {
    selectTab(tab) {
      this.selectedTab = tab;
    },
    addResourcesToDB(title, description, url) {
      const addNew = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(addNew);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>

<style>
</style>