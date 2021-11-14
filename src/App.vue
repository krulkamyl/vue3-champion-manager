<template>
  <div id="app">
    <NewChampion />
    <ItemsChampion />
  </div>
</template>

<script>
  import NewChampion from './components/NewChampion';
  import ItemsChampion from './components/ItemsChampion';

  export default {
    name: 'app',
    components: {
      NewChampion,
      ItemsChampion
    },
    data: () => ({
      champions: [{
          name: 'Lux',
          pseudo: 'the Light',
          hp: 120,
          mp: 890
        },
        {
          name: 'Macho',
          pseudo: 'the Strong',
          hp: 690,
          mp: 80
        }
      ]
    }),
    mounted: function () {
      this.emitter.emit("champions-data", this.champions);
    },
  }
</script>

<style scope>
  #app {
    padding: 20px;
  }
</style>