<template>
    <div class="cell" @click="onClick">
        <template v-if="isO">{{text}}</template>
        <template v-else></template>
    </div>
</template>

<script>
  export default {
    name: 'Cell',
    props: {
      n: Number
    },
    data () {
      return {
        isO: false,
        text: ''
      };
    },
    methods: {
      onClick () {
        if (this.text != '') {
          return;
        }
        this.text = this.n % 2 == 0 ? 'X' :'O';
        this.isO = true;
        this.$emit('click', this.text);
      }
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .cell {
        border-collapse: collapse;
        width: 100px;
        height: 100px;
        border: 2px solid #000;
        font-size: 20px;
        font-weight: 800;
        margin-right: -2px;
        margin-bottom: -2px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    ul {
        list-style-type: none;
        padding: 0;
    }
    li {
        display: inline-block;
        margin: 0 10px;
    }
    a {
        color: #42b983;
    }
</style>
