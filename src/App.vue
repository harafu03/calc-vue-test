<template>
  <div>
    <div>
      <button v-for="i in 3" :key="i" @click="bindValue(i + 6)">
        {{ i + 6 }}
      </button>
      <button @click="setType('/')">/</button>
    </div>
    <div>
      <button v-for="i in 3" :key="i" @click="bindValue(i + 3)">
        {{ i + 3 }}
      </button>
      <button @click="setType('*')">*</button>
    </div>
    <div>
      <button v-for="i in 3" :key="i" @click="bindValue(i)">{{ i }}</button>
      <button @click="setType('-')">-</button>
    </div>
    <div>
      <button>&nbsp;</button>
      <button @click="bindValue(0)">0</button>
      <button>&nbsp;</button>
      <button @click="setType('+')">+</button>
    </div>
    <button @click="calcResult()">=</button>
    <button @click="resetCalc()">C</button>
  </div>
  <div>
    <span>{{ first }}</span>
    <span>{{ type }}</span>
    <span>{{ second }}</span>
    <h5>{{ res }}</h5>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      first: "",
      type: "",
      second: "",
      res: "",
    };
  },
  methods: {
    resetCalc() {
      this.first = "";
      this.type = "";
      this.second = "";
      this.res = "";
    },
    bindValue(i) {
      if (this.type) {
        this.second = parseInt(String(this.second) + String(i));
      } else {
        this.first = parseInt(String(this.first) + String(i));
      }
    },
    setType(type) {
      if (!this.first) return;
      if (this.second) {
        this.calcResult();
        this.second = "";
        this.first = this.res;
        this.res = "";
        this.type = type;
        return;
      }
      if (String(this.res).length > 0) {
        this.second = "";
        this.first = this.res;
      }
      this.type = type;
    },
    calcResult() {
      switch (this.type) {
        case "+":
          this.res = this.first + this.second;
          break;
        case "-":
          this.res = this.first - this.second;
          break;
        case "*":
          this.res = this.first * this.second;
          break;
        case "/":
          this.res = this.first / this.second;
          break;
      }
    },
  },
};
</script>

<style>
button {
  margin-right: 2px;
  padding: 0.5rem;
}
</style>
