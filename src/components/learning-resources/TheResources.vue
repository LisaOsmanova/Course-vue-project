<template>
    <base-card>
    <the-button @click="setselectedTad('stored-resources')" :mode="storedResButtonMode">Stored Resources</the-button>
    <the-button @click="setselectedTad('add-resources')" :mode="addResButtonMode">Add Resources</the-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResources from './AddResource.vue';
export default {
    components:{StoredResources, AddResources},
    data() {
        return {
            selectedTab:'stored-resources',
            storedResources:[
                {
                    id: 'official-guide', 
                    title: 'Official Guide', 
                    description: 'The Official Vue JS Documentation.',
                    link:'https://vuejs.org/'
                },
                {
                    id: 'google', 
                    title: 'Google', 
                    description: 'Learn to Google',
                    link:'https://google.org/'
                }
            ]
    }
    },
    provide() {
        return {
            resources: this.storedResources,
            addRes: this.addNewResource,
            deleteResource: this.removeResource
        }
    },
    computed: {
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
    },
    methods: {
        setselectedTad(tab){
            this.selectedTab = tab;
        },
        addNewResource(title,description,link){
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: link
            }
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(resId){
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1)
        }
    }
}
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #270041;
  border-color: #270041;
}

.flat {
  background-color: transparent;
  color: #3a0061;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #edd2ff;
}
</style>