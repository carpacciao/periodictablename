<template>
  <div>
    <a href="#" class="btn btn-primary" @click.prevent="test()">Lucas</a>
    <h1 class="text-center mt-5">Find your name in the <strong class="text-primary">periodic table</strong> !</h1>
    <div class="row">
      <div class="col-4"></div>
      <div class="col-4">
        <input type="text" v-validate="'required|alpha_dash'" name="alpha_dash_field" class="mt-5 form-control" :class="{'is-invalid': has_error}" placeholder="Your name" v-model="name">
        <div v-if="has_error" class="invalid-feedback d-block">Ce champ doit être rempli et composé de lettres uniquement.</div>
      </div>
      <div class="col-4"></div>
    </div>
    <div class="container-fluid bg-sombre mt-5">
      <div class="container d-flex justify-content-center flex-wrap">
        <element-x v-for="item in result" :key="item.atomicNumber" :element-name="item.name" :element-abv="item.symbol" :element-number="item.atomicNumber" :element-color="item.cpkHexColor"></element-x>
      </div>
    </div>
  </div>
</template>

<script>
import ElementX from './Element'

const tools = {
  isIn (el, tb) {
    for (let i = 0; i < el.length; i++) {
      for (let j = 0; j < tb.length; j++) {
        if(el[i].toUpperCase() === tb[j].symbol.toUpperCase()){
          console.log(el[i])
          console.log(tb[j].symbol)
          console.log('oui')
        }
      }
    }
  }
}

export default {
  components: {ElementX},
  data () {
    return {
      table: Array,
      name: '',
      pre : 'Lucas'
    }
  },
  methods: {
    getData () {
      this.table = require('./table.json')
    },
    test () {
      tools.isIn('lucas', this.table)
    }
  },
  computed: {
    has_error () {
      if(this.errors.items.length !== 0) {
        return true
      }
      return false
    },
    result () {
      let r = []
      r.push(this.table[0])
      return r
    }
  },
  created () {
    this.getData()
  }
}
</script>

<style lang="scss">
.bg-sombre{
  background-color: rgb(245, 245, 245);
  border-top: 1px solid rgba(0, 0, 0, 0.274);
}

</style>
