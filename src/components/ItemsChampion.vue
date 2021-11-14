<template>
  <div class="row row-cols-1 row-cols-md-2 g-4">
    <ItemChampion v-for="champion in champions" :key="champion.name" :champion="champion" />
  </div>
</template>

<script>
  import ItemChampion from './ItemChampion';
  export default {
    components: {
      ItemChampion
    },
    data: () => ({
      champions: []
    }),
    mounted() {
      this.emitter.on("champions-data", champions => {
        this.champions = champions;
      });
    },
    methods: {
      deleteItem: function (name) {
        
        let newChampionArr = this.champions.filter(function (champion) {
          return name.toLowerCase() !== champion.name.toLowerCase()
        })

        this.emitter.emit("champions-data", newChampionArr);
      }
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>