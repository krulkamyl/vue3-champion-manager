<template>
  <div class="card text-white bg-primary mb-3">
    <div class="card-header">
      Dodawanie championa
    </div>
    <div class="card-body">
      <form id="add-champion">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="champion-name">Imię postaci</span>
          </div>
          <input type="text" class="form-control" v-model="name" placeholder="imię" aria-label="imię" aria-describedby="champion-name">
        </div>
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="champion-nick">Przedrostek postaci</span>
          </div>
          <input type="text" class="form-control" v-model="nick" placeholder="przedrostek" aria-label="nick"
            aria-describedby="champion-nick">
        </div>
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="champion-hp">Max HP</span>
          </div>
          <input type="number" min="1" max="100" class="form-control" v-model="maxHp" placeholder="Maksymalna ilość HP" aria-label="hp"
            aria-describedby="champion-hp">
          &nbsp;
          <div class="input-group-prepend">
            <span class="input-group-text" id="champion-mp">Max MP</span>
          </div>
          <input type="number" min="1" max="100" class="form-control" v-model="maxMp" placeholder="Maksymalna ilość MP" aria-label="mp"
            aria-describedby="champion-mp">
        </div>
        <button type="button" class="btn btn-danger" @click="clearForm()">Resetuj</button>
        &nbsp;
        <button type="button" class="btn btn-success" :class="{disabled: isReserved}" @click="addChampion()">Dodaj</button>
      </form>
    </div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      champions: [],
      isReserved: false,
      name: '',
      nick: '',
      maxHp: '',
      maxMp: ''
    }),
    methods: {
      clearForm: function() {
        this.name = '';
        this.nick = '';
        this.maxHp = '';
        this.maxMp = '';
      },
      addChampion: function() {
        this.champions.push({name: this.name, pseudo: this.nick, hp: this.maxHp, mp: this.maxMp});
        this.emitter.emit("champions-data", this.champions);
        this.clearForm();
      }
    },
    watch: {
      name(value) {
        this.isReserved = false;
        this.champions.forEach((item) => {
          if (item.name.toLowerCase() === value.toLowerCase()) {
            this.isReserved = true;
          }
        });
        
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