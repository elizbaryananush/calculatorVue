<script setup>
import { ref } from "vue";

const answer = ref("");
const expression = ref("");

const appendValue = (value) => {
  if (answer.value === "") {
    expression.value += value;
  } else {
    expression.value = answer.value;
    answer.value = "";
  }
};

const deleteAll = () => {
  expression.value = "";
  answer.value = "";
};

const deleteOnly = () => {
  expression.value = answer.value;
  answer.value = "";
};

const solve = () => {
  answer.value = eval(expression.value);
};

const plusMinus = () => {
  if (answer.value === "") {
    if (expression[0] === "-") {
      expression.value = expression.value + expression.value * 2;
    } else {
      expression.value = expression.value - expression.value * 2;
    }
  } else {
    expression.value = answer.value;
    answer.value = "";

    if (expression[0] === "-") {
      expression.value = expression.value + expression.value * 2;
    } else {
      expression.value = expression.value - expression.value * 2;
    }
  }
};

const deleteLastSymbol = () => {
  if (answer.value === "") {
    expression.value = expression.value.slice(0 , -1);
  } else {
      expression.value = answer.value.toString();
      expression.value = expression.value.slice(0 , -1)
    answer.value = "";
  }
};
</script>

<template>
  <main class="main">
    <div class="calculator">
      <div class="top">
        <div v-if="answer !== ''" class="answer">{{ answer }}</div>
        <div class="expression">{{ expression }}</div>
      </div>
      <div class="bottom">
        <button @click="solve()" class="equal">=</button>
        <button @click="deleteAll()">CE</button>
        <button @click="deleteOnly()">C</button>
        <button @click="deleteLastSymbol()">&#x2716;</button>
        <button @click="appendValue('7')">7</button>
        <button @click="appendValue('8')">8</button>
        <button @click="appendValue('9')">9</button>
        <button @click="appendValue('/')">&#xF7;</button>
        <button @click="appendValue('4')">4</button>
        <button @click="appendValue('5')">5</button>
        <button @click="appendValue('6')">6</button>
        <button @click="appendValue('*')">*</button>
        <button @click="appendValue('1')">1</button>
        <button @click="appendValue('2')">2</button>
        <button @click="appendValue('3')">3</button>
        <button @click="appendValue('-')">-</button>
        <button @click="plusMinus()">&plusmn;</button>
        <button @click="appendValue('0')">0</button>
        <button @click="appendValue('.')">.</button>
        <button @click="appendValue('+')">+</button>
      </div>
    </div>
  </main>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Roboto;
}

#app {
  height: 100vh;
  width: 100%;
  background: url("@/assets/background.jpg");
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main {
  height: 80vh;
  width: 470px;
  background-color: rgb(255, 255, 255);
  border-radius: 40px;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;

  .calculator {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: stretch;
    align-items: center;

    .top {
      height: 25vh;
      width: 410px;
      background-color: rgb(236, 236, 236);
      border-radius: 20px;
      margin: 30px;
      margin-bottom: 0;
      box-shadow: rgba(0, 0, 0, 0.05) 0px 6px 24px 0px,
        rgba(0, 0, 0, 0.08) 0px 0px 0px 1px;
      padding: 20px;
      display: flex;
      flex-direction: column-reverse;

      .answer {
        font-size: 36px;
        font-weight: 800;
      }

      .expression {
        font-size: 24px;
      }
    }

    .bottom {
      width: 98%;
      height: 100%;
      padding: 30px;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;

      button {
        height: 100%;
        width: 100%;
        border: 0;
        background-color: rgb(236, 236, 236);
        border-radius: 5px;
        font-size: 1.3rem;
        cursor: pointer;
        box-shadow: rgba(0, 0, 0, 0.02) 0px 1px 3px 0px,
          rgba(27, 31, 35, 0.15) 0px 0px 0px 1px;

        &:hover {
          background-color: rgb(224, 224, 224);
        }

        &:active {
          background-color: rgb(185, 185, 185);
        }
      }

      .equal {
        background-color: rgb(255, 144, 103);
        font-size: 1.5rem;
        color: white;
        box-shadow: none;

        &:hover {
          background-color: rgb(255, 123, 75);
        }

        &:active {
          background-color: #ff662f;
        }
      }
    }
  }
}
</style>
