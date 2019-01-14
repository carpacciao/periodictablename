<template>
  <div>
    <h1 class="text-center mt-5">Find your name in the <strong class="text-primary">periodic table</strong> !</h1>
    <div class="row">
      <div class="col-4"></div>
      <div class="col-4">
        <input type="text" v-validate="'required|alpha_dash'" name="alpha_dash_field" class="mt-5 form-control" :class="{'is-invalid': has_error}" placeholder="Your name" v-model="name">
        <div v-if="has_error" class="invalid-feedback d-block">Ce champ doit être rempli et composé de lettres uniquement.</div>
      </div>
      <div class="col-4"></div>
    </div>
    <div class="container d-flex justify-content-center flex-wrap">
      <element-x v-for="item in table" :element-name="item.name" :element-abv="item.symbol" :element-number="item.atomicNumber" :element-color="item.cpkHexColor"></element-x>
    </div>
    <div class="container d-flex justify-content-center">
      <element-x element-name="hydrogen" element-abv="H" element-number="1" element-color="00FF00"></element-x>
      <element-x element-name="caca" element-abv="C" element-number="2" element-color="00FF00"></element-x>
    </div>
  </div>
</template>

<script>
import ElementX from './Element'
export default {
  components: {ElementX},
  data () {
    return {
      table: Array,
      name: ''
    }
  },
  methods: {
    getData () {
      this.table = require('./table.json')
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
      return [{}]
    }
  },
  created () {
    this.getData()
  }
}
</script>