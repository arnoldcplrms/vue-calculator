<template>
	<div class="calculator">
		<div class="display">{{current || 0}}</div>
		<div class="btn"
		     @click="clear">C</div>
		<div class="btn"
		     @click="sign">+/-</div>
		<div class="btn"
		     @click="percent">%</div>
		<div class="btn operator"
		     @click="divide">/</div>
		<div class="btn"
		     @click="append(7)">7</div>
		<div class="btn"
		     @click="append(8)">8</div>
		<div class="btn"
		     @click="append(9)">9</div>
		<div class="btn operator"
		     @click="multiply">x</div>
		<div class="btn"
		     @click="append(4)">4</div>
		<div class="btn"
		     @click="append(5)">5</div>
		<div class="btn"
		     @click="append(6)">6</div>
		<div class="btn operator"
		     @click="subtract">-</div>
		<div class="btn"
		     @click="append(1)">1</div>
		<div class="btn"
		     @click="append(2)">2</div>
		<div class="btn"
		     @click="append(3)">3</div>
		<div class="btn operator"
		     @click="add">+</div>
		<div class="zero btn"
		     @click="append(0)">0</div>
		<div class="btn"
		     @click="dot">.</div>
		<div @click="equal"
		     class="btn operator">=</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			current: '',
			operator: null,
			operatorClicked: false,
			previous: null
		}
	},
	methods: {
		setPrevious() {
			this.previous = this.current;
			this.operatorClicked = true;
		},
		clear() {
			this.current = '';
		},
		sign() {
			this.current = this.current.charAt(0) === '-' ?
				this.current.slice(1) : this.current = `-${this.current}`;
		},
		percent() {
			this.current = `${parseFloat(this.current) / 100}`;
		},
		append(number) {
			if (this.operatorClicked) {
				this.current = '';
				this.operatorClicked = false;
			}
			this.current = `${this.current}${number.toString()}`;
		},
		dot() {
			if (this.current.indexOf('.') === -1) {
				this.append('.')
			}
		},
		add() {
			this.operator = (a, b) => a + b;
			this.setPrevious();
		},
		subtract() {
			this.operator = (a, b) => a - b;
			this.setPrevious();
		},
		multiply() {
			this.operator = (a, b) => a * b;
			this.setPrevious();
		},
		divide() {
			this.operator = (a, b) => a / b;
			this.setPrevious();
		},
		equal() {
			this.current = `${this.operator(
				parseFloat(this.current), parseFloat(this.previous)
			)}`
			this.previous = null;
		}
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #eee;
  border: 1px solid #999;
  cursor: pointer;
}

.operator {
  background-color: orange;
  color: white;
}

.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
}
</style>
