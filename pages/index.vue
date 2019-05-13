<template>
  <div>

  <section class="flex-container has-background-warning">

      <div class="left has-background-danger">

      <div class="field">
        <label class="label has-text-white is-large">Criteria
        </label>
        <div v-for="criterium in criteria" class="control mb-3">
          <div class="is-flex">
          <input v-model="criterium.title" class="input" type="text" placeholder="Text input">
          <div class="select">
            <select v-model="criterium.imp">
              <option>1</option>
              <option>2</option>
              <option>3</option>
              <option>4</option>
              <option>5</option>
            </select>
          </div>
          </div>
        </div>
      </div>

      <div class="buttons is-at-bottom">
        <a v-on:click="addCriterium()" class="button is-white "><strong>Add Criterium</strong></a>
        <a v-on:click="removeCriterium()" class="button is-light">Remove</a>
      </div>

      </div>

      <div class="right has-background-info">

      <div class="field">
        <label class="label has-text-white is-large">Options
        </label>
      </div>
      <div v-for="(option, key) in options" class="field is-flex mb-5">
        <div class="control">
          <input v-model="option.name" class="input" type="text" placeholder="Text input">
        </div>
        <div v-for="(criterium, key) in  criteria" class="select">
          <select v-model="option.matches[key]">
            <option>1</option>
            <option>2</option>
            <option>3</option>
            <option>4</option>
            <option>5</option>
          </select>
          <p class="has-text-white">{{criterium.title}}</p>
        </div>
      </div>

      <div class="buttons is-at-bottom">
        <a v-on:click="addOption()" class="button is-white "><strong>Add Option</strong></a>
        <a v-on:click="removeOption()" class="button is-light">Remove</a>
      </div>

      </div>

      <div class="results has-background-warning">
        <div class="field">
          <label class="label is-large">Ranking
          </label>
          <ul>
            <li v-for="(option, key) in options"><strong>{{option.name}}</strong> {{getResult(option)}}</li>
          </ul>
        </div>
      </div>

  </section>

  </div>
</template>

<script>
import Head from '~/components/Head'

export default {

  components: {
    Head
  },

  data() {
    return {
      criteria: [
        {
        title: 'Fun',
        imp: 5
        }
      ],
      options: [
        {
        name: 'Exploding Kittens',
        matches:[5]
        }
      ]
    }
  },
  methods: {
    addCriterium() {
      let x = {};
      this.criteria.push(x)
      this.options.forEach(o => {let x = {}; o.matches.push(x)});
    },
    removeCriterium() {
      this.criteria.pop()
      this.options.forEach(o => o.matches.pop())
    },
    addOption() {
      let x = {};
      let y = {
        matches:[]
      };
      for (let i = 0; i < this.options[0].matches.length; i++ ){
        y.matches.push(x)
      }
      this.options.push(y)
    },
    removeOption() {
      this.options.pop()
    },
    getResult(x) {
      let result = 0;
      let i = 0;
      x.matches.forEach(y => {
        result = result + (parseInt(y) * this.criteria[i].imp);
        i++;
      })
      return result
    }
  },
  computed: {
    // getResult() {
    //   let multiple = 1
    //   this.criteria.forEach(x => multiple = multiple * x.imp)
    //   return multiple
    // }
  }

}
</script>

<style>
.flex-container {
  display: flex;
  flex-direction: row;
  width: 100vw;
  height: 100vh;
}
.left, .right{
  flex: 2;
  height: 100vh;
  padding: 2%
}
.results {
  flex:1;
  height: 100vh;
  padding: 2%
}
.mt-5 {
  margin-top: 30px;
}
.mt-3 {
  margin-top: 10px;
}
.mb-5 {
  margin-bottom: 30px !important;
}
.mb-3 {
  margin-bottom: 10px;
}
.mb-2 {
  margin-bottom: 8px;
}
.p-5 {
  padding: 5%;
}
.is-at-bottom {
  position: absolute;
  bottom: 25px;
}

</style>
