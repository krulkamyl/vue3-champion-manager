<template>
  <div class="col">
    <div class="card">
      <div class="card-body">
        <h4 class="card-header d-flex justify-content-between align-items-center">
          {{ champion.name }}
          <button type="button" class="btn btn-sm btn-danger" @click="deleteItem()">Usuń</button>
          </h4>
        <p class="card-text">{{ champion.pseudo }} </p>
        <div class="progress">
          <div class="progress-bar bg-success" role="progressbar" style="width: 100%;" aria-valuenow="25" aria-valuemin="0"
            aria-valuemax="100">{{ champion.hp }} HP</div>
        </div>
        <p></p>
        <div class="progress">
          <div class="progress-bar" role="progressbar" style="width: 100%;" aria-valuenow="25" aria-valuemin="0"
            aria-valuemax="100">{{ champion.mp }} MP</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      champions: []
    }),
    props: {
      champion: Object
    },
    methods: {
      deleteItem: function() {
        this.$parent.deleteItem(this.champion.name);
      }
    },
    mounted() {
        this.emitter.on("champions-data", champions => {
          this.champions = champions;
        });
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>