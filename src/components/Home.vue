<template>
  <div>
    <h1 class="text-center mt-5">Find your name in the <strong class="text-primary">periodic table</strong> !</h1>
    <div class="row">
      <div class="col-4"></div>
      <div class="col-4">
        <input type="text" v-validate="'required|alpha_dash'" name="alpha_dash_field" class="mt-5 form-control" :class="{'is-invalid': has_error}"
          placeholder="Your name" v-model="name">
        <div v-if="has_error" class="invalid-feedback d-block">Ce champ doit être rempli et composé de lettres
          uniquement.</div>
      </div>
      <div class="col-4"></div>
    </div>
    <div class="container-fluid bg-sombre mt-5">
      <div class="container d-flex justify-content-center flex-wrap">
        <element-x v-for="item in result" :key="item.atomicNumber" :element-name="item.name" :element-abv="item.symbol"
          :element-number="item.atomicNumber" :element-color="item.cpkHexColor"></element-x>
      </div>
    </div>
  </div>
</template>

<script>
  import ElementX from './Element'

  export default {
    components: {
      ElementX
    },
    data() {
      return {
        table: Array,
        name: '',
        pre: 'Lucas'
      }
    },
    methods: {
      getData() {
        this.table = require('./table.json')
      },
      test() {
        tools.isIn('lucas', this.table)
      }
    },
    computed: {
      has_error() {
        if (this.errors.items.length !== 0) {
          return true
        }
        return false
      },
      result() {
        let s = this.name
        let t = this.table 
        let f = []
        for (let i = 0; i < s.length; i++) {
          if (i !== s.length - 1) {
            let r = t.filter((v) => {
              return v.symbol.toUpperCase() === s[i].toUpperCase()
            })
            if (r.length > 0) {
              console.log(r[0].symbol)
              f.push(r[0])
            } else {
              let e = t.filter((v) => {
                return v.symbol.toUpperCase() === (s[i].toUpperCase() + s[i + 1].toUpperCase())
              })
              if (e.length > 0) {
                console.log(e[0].symbol)
                f.push(e[0])
                i++
              }
            }
          }else {
            let a = t.filter((v) => {
              return v.symbol.toUpperCase() === s[i].toUpperCase()
            })
            if(a.length > 0) {
              f.push(a[0])
            }
          }
        }
        console.table(f)
        return f
      }
    },
    created() {
      this.getData()
    }
  }

</script>

<style lang="scss">
  .bg-sombre {
    background-color: rgb(245, 245, 245);
    border-top: 1px solid rgba(0, 0, 0, 0.274);
  }

</style>
