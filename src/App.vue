<template>
    <div id="app">
        <div>{{result}}</div>
        <div class="row">
            <Cell @click="onClick(1,$event)" :n="n"/>
            <Cell @click="onClick(2,$event)" :n="n"/>
            <Cell @click="onClick(3,$event)" :n="n"/>
            <Cell @click="onClick(4,$event)" :n="n"/>
        </div>
        <div class="row">
            <Cell @click="onClick(5,$event)" :n="n"/>
            <Cell @click="onClick(6,$event)" :n="n"/>
            <Cell @click="onClick(7,$event)" :n="n"/>
            <Cell @click="onClick(8,$event)" :n="n"/>

        </div>
        <div class="row">
            <Cell @click="onClick(9,$event)" :n="n"/>
            <Cell @click="onClick(10,$event)" :n="n"/>
            <Cell @click="onClick(11,$event)" :n="n"/>
            <Cell @click="onClick(12,$event)" :n="n"/>
        </div>
        <div class="row">
            <Cell @click="onClick(13,$event)" :n="n"/>
            <Cell @click="onClick(14,$event)" :n="n"/>
            <Cell @click="onClick(15,$event)" :n="n"/>
            <Cell @click="onClick(16,$event)" :n="n"/>
        </div>
    </div>
</template>

<script>
  import Cell from './components/cell.vue';

  export default {
    name: 'app',
    data () {
      return {
        n: 0,
        result: false,
        map: []
      };
    },
    components: {
      Cell
    },
    beforeMount () {
      const m = 3;
      const n = 3;
      this.map = Array.from({length: m + 1}, x => Array.from({length: n + 1}, y => ''));
    },
    methods: {
      onClick (n, v) {
        this.n = this.n + 1;
        const index = n - 1;
        const y = Math.floor(index / 4);
        const x = index % 4;
        this.map[y][x] = v;
        this.tell();
      },
      tell () {
        const mapp = this.map;
        for (let n = 0; n < mapp.length; n++) {
          const item = mapp[n];
          for (let i = 0; i < mapp[n].length; i++) {
            if (item[i] != '') {
              if (i == 0) {
                if (item[i] == item[i + 1] && item[i] == item[i + 2]) {
                  console.log(item);
                  this.result = true;
                } else if (i > 0 && i < item.length - 1 && item[i] == item[i - 1] && item[i] == item[i + 1]) {
                  this.result = true;
                }
              } else if (i > 0 && i < item.length - 1 && item[i] == item[i - 1] && item[i] == item[i + 1]) {
                this.result = true;
              } else if (i == item.length - 1 && item[i] == item[i - 1] && item[i] == item[i - 2]) {
                this.result = true;
              }

              if (n == 0) {
                if (mapp[n][i] && mapp[n][i] == mapp[n + 1][i] && mapp[n][i] == mapp[n + 2][i]) {
                  this.result = true;
                }
              } else if (n > i && n < mapp.length - 1) {
                if (mapp[n][i] && mapp[n][i] == mapp[n - 1][i] && mapp[n][i] == mapp[n + 1][i]) {
                  this.result = true;
                }
              } else if (n == mapp.length - 1) {
                if (mapp[n][i] && mapp[n][i] == mapp[n - 1][i] && mapp[n][i] == mapp[n - 2][i]) {
                  this.result = true;
                }
              }

              if (item.length - i - 3 >= 0 && mapp.length - n - 3 >= 0) {
                if (mapp[n][i] == mapp[n + 1][i + 1] && mapp[n][i] == mapp[n + 2][i + 2]) {
                  this.result = true;
                }
              } else if (item.length - i - 3 < 0 && mapp.length - n - 3 > 0) {
                console.log('sdsd');
                console.log(i, n);

                if (mapp[n][i] == mapp[n - 1][i - 1] && mapp[n][i] == mapp[n - 2][i - 2]) {
                  this.result = true;
                }
              }

            }


          }
        }
        console.log(this.result);
      }
      ,
      xie () {

      }
    }
  }
  ;
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
    .row {
        display: flex;
    }
</style>
