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
  <component :is="selectedTabComponent"></component>
</template>

<script setup>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
import { provide, ref, computed } from 'vue';
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
provide('resources', storedResources);
</script>
