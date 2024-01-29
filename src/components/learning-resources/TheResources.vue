<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storeResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official guide to Vue.js',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'The place to find everything',
          link: 'https://google.com',
        },
        {
          id: 'stack-overflow',
          title: 'Stack Overflow',
          description: 'The place to ask and answer questions',
          link: 'https://stackoverflow.com',
        },
        {
          id: 'github',
          title: 'Github',
          description: 'The place to share code',
          link: 'https://github.com',
        },
        {
          id: 'vue-forum',
          title: 'Vue Forum',
          description: 'The place to ask and answer Vue questions',
          link: 'https://forum.vuejs.org',
        },
        {
          id: 'vue-land',
          title: 'Vue Land',
          description: 'The place to chat about Vue',
          link: 'https://vue-land.js.org',
        },
        {
          id: 'frc-forum',
          title: 'FRC Forum',
          description: 'The place to ask and answer FRC questions',
          link: 'https://www.chiefdelphi.com/c/technical',
        },
        {
          id: 'frc-blog',
          title: 'FRC Blog',
          description: 'The place to find FRC updates',
          link: 'https://www.firstinspires.org/robotics/frc/blog',
        },
        {
          id: 'frc-docs',
          title: 'FRC Docs',
          description: 'The place to find FRC documentation',
          link: 'https://docs.wpilib.org/en/stable/',
        },
        {
          id: 'frc-discord',
          title: 'FRC Discord',
          description: 'The place to chat about FRC',
          link: 'https://discord.gg/first',
        },
        {
          id: 'apple',
          title: 'Apple',
          description: 'The place to find Apple products',
          link: 'https://apple.com',
        },
        {
          id: 'microsoft',
          title: 'Microsoft',
          description: 'The place to find Microsoft products',
          link: 'https://microsoft.com',
        }
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
    };
  },
  computed: {
    storeResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, decription, link) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: decription,
        link: link,
      };
      this.storedResources.unshift(newResource);
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