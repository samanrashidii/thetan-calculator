<template>
  <div
    class="home py-5"
  >
    <img
      alt="Thetan Arena Logo"
      src="https://thetanarena.com/c340923d536b2cd10586.png"
      width="300"
    >
    <div
      class="thetan-form mt-4 p-4 border rounded"
    >
      <b-form inline>
        <div
          class="form-item my-3 d-flex justify-content-center align-items-center"
        >
          <label
            for="hero-type"
            class="mr-2"
          >
            THC Price : 
          </label>
          <b-form-input
            v-model.number="thcPrice"
            type="text"
            class="number-input-x2"
          />
        </div>
        <div
          class="form-item my-3 d-flex justify-content-center align-items-center"
        >
          <label
            for="hero-type"
            class="mr-2"
          >
            Hero Type : 
          </label>
          <b-form-select
            v-model="heroType"
            id="hero-type"
            :options="varieties"
          />
        </div>
        <div
          class="form-item my-3 d-flex justify-content-center align-items-center"
        >
          <label
            class="mr-2"
          >
            Hero Price : 
          </label>
          <b-form-input
            v-model.number="heroPrice"
            type="text"
            class="number-input-x2"
          />
        </div>
        <div
          class="form-item my-3 d-flex justify-content-center align-items-center"
        >
          <label
            class="mr-2"
          >
            Hero Matches : 
          </label>
          <b-form-input
            v-model.number="playedMatches"
            type="text"
            class="number-input"
          />
          <span
            class="mx-2"
          >
            /
          </span>
          <b-form-input
            v-model.number="totalMatches"
            type="text"
            class="number-input"
          />
        </div>
        <b-button
          type="button"
          variant="primary"
          class="mt-3"
          @click="calcIncome"
        >
          Calculate
        </b-button>
      </b-form>
      <div class="show-result d-flex justify-content-center align-items-center mt-4">
        <h5
          class="mr-2"
        >
          Hero Cost in THC : 
        </h5>
        <h1>
          {{ heroPriceInTHC + 'THC' }}
        </h1>
      </div>
      <div class="show-result d-flex justify-content-center align-items-center mt-4">
        <h5
          class="mr-2"
        >
          Hero Cost in Dollar : 
        </h5>
        <h1>
          {{ heroPrice + '$' }}
        </h1>
      </div>
      <div class="show-result d-flex justify-content-center align-items-center mt-4">
        <h5
          class="mr-2"
        >
          income in THC : 
        </h5>
        <h1>
          {{ thcIncome + 'THC' }}
        </h1>
      </div>
      <div class="show-result d-flex justify-content-center align-items-center mt-4">
        <h5
          class="mr-2"
        >
          income in Dollar : 
        </h5>
        <h1>
          {{ dollarIncome + '$' }}
        </h1>
      </div>
      <div class="show-result d-flex justify-content-center align-items-center mt-4">
        <h5
          class="mr-2"
        >
          Profit : 
        </h5>
        <h1
          :class="{
            'text-danger': profit <= 0,
            'text-success': profit > 0
          }"
        >
          {{ profit + '$' }}
        </h1>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data () {
    return {
      thcPrice: '',
      heroType: 9.25,
      heroPrice: 0,
      dollarIncome: 0,
      thcIncome: 0,
      playedMatches: null,
      totalMatches: null,
      varieties: [
        {
          text: 'Common',
          value: 9.25
        },
        {
          text: 'Epic',
          value: 12.5
        },
        {
          text: 'Legendary',
          value: 29.55
        }
      ]
    }
  },
  computed: {
    profit () {
      let output = 0
      if (this.dollarIncome && this.heroPrice) {
        output = this.dollarIncome - this.heroPrice
      }
      return output
    },
    heroPriceInTHC () {
      let output = 0
      if (this.heroPrice && this.thcPrice) {
        output = this.heroPrice / this.thcPrice
      }
      return output.toFixed()
    }
  },
  methods: {
    calcIncome () {
      if (this.playedMatches && this.totalMatches) {
        const remainingBattle = this.totalMatches - this.playedMatches
        this.thcIncome = remainingBattle * this.heroType
        const totalIncomeInUSD = this.thcIncome * this.thcPrice
        this.dollarIncome = totalIncomeInUSD.toFixed()
      }
    }
  }
}
</script>

<style lang="scss">
  .thetan-form{
    max-width: 480px;
    margin-left: auto;
    margin-right: auto;
  }
  .mr-2{
    margin-right: 1rem;
  }
  .number-input{
    max-width: 60px;
  }
  .number-input-x2{
    max-width: 100px;
  }
</style>
