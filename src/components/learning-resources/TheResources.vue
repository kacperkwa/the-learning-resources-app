<template>
  <BaseCard>
    <BaseButton
      @click="setSelectedTab('StoredResources')"
      :mode="storedResButtonMode"
      >Stored Resources</BaseButton
    >
    <BaseButton @click="setSelectedTab('AddResource')" :mode="AddResButtonMode"
      >Add Resource</BaseButton
    >
  </BaseCard>
  <KeepAlive>
    <component :is="selectedTabComponent"></component>
  </KeepAlive>
</template>

<script setup>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
import { provide, ref, computed, onMounted } from 'vue';
let selectedTab = ref('StoredResources');
const setSelectedTab = (tab) => {
  selectedTab.value = tab;
};

const storedResources = ref([
  {
    id: 'official-guide',
    title: 'Official Guide',
    description: 'The official Vue.js documentation',
    link: 'https://vuejs.org',
  },
  {
    id: 'google',
    title: 'Google',
    description: 'Learn to google..',
    link: 'https://google.com',
  },
]);
const storedResButtonMode = computed(() => {
  return selectedTab.value === 'StoredResources' ? null : 'flat';
});
const AddResButtonMode = computed(() => {
  return selectedTab.value === 'AddResource' ? null : 'flat';
});
const selectedTabComponent = computed(() => {
  return selectedTab.value === 'StoredResources'
    ? StoredResources
    : AddResource;
});

const addResource = (title, description, url) => {
  if (storedResources.value) {
    const newResource = {
      id: new Date().toISOString(),
      title: title,
      description: description,
      link: url,
    };
    storedResources.value.unshift(newResource);
    selectedTab.value = 'StoredResources';
  }
};
const removeResource = (resId) => {
  storedResources.value = storedResources.value.filter(
    (res) => res.id !== resId
  );
};
onMounted(() => {
  provide('addResource', addResource);
});
provide('resources', storedResources);
provide('removeResource', removeResource);
</script>
