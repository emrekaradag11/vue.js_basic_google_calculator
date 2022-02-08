<template>
  <div class="hello">
    <h1 class="mt-4">{{ msg }}</h1>
    <div class="container">
      <div class="col-lg-8 mx-auto">
        <div class="calculator mt-5">
          <table class="table">
            <thead>
              <tr>
                <th colspan="8">
                  <div class="screen">
                    {{ number1 }} {{ trans }} {{ number2 }} {{ result }}
                  </div>
                </th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><button class="btn notSuccess">Rad</button></td>
                <td><button class="btn notSuccess">Deg</button></td>
                <td>
                  <button class="btn success" @click="setTransaction('!')">
                    !
                  </button>
                </td>
                <td><button class="btn notSuccess">(</button></td>
                <td><button class="btn notSuccess">)</button></td>
                <td>
                  <button class="btn success" @click="setTransaction('%')">
                    %
                  </button>
                </td>
                <td>
                  <button class="btn success" @click="deleteScreen()">
                    AC
                  </button>
                </td>
              </tr>
              <tr>
                <td><button class="btn notSuccess">Inv</button></td>
                <td><button class="btn notSuccess">sin</button></td>
                <td><button class="btn notSuccess">ln</button></td>
                <td>
                  <button class="btn bgDark" @click="setNumber('7')">7</button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('8')">8</button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('9')">9</button>
                </td>
                <td>
                  <button class="btn success" @click="setTransaction('/')">
                    ÷
                  </button>
                </td>
              </tr>
              <tr>
                <td><button class="btn notSuccess">π</button></td>
                <td><button class="btn notSuccess">cos</button></td>
                <td><button class="btn notSuccess">log</button></td>
                <td>
                  <button class="btn bgDark" @click="setNumber('4')">4</button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('5')">5</button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('6')">6</button>
                </td>
                <td>
                  <button class="btn success" @click="setTransaction('*')">
                    ×
                  </button>
                </td>
              </tr>
              <tr>
                <td><button class="btn notSuccess">e</button></td>
                <td><button class="btn notSuccess">tan</button></td>
                <td><button class="btn notSuccess">√</button></td>
                <td>
                  <button class="btn bgDark" @click="setNumber('1')">1</button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('2')">2</button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('3')">3</button>
                </td>
                <td>
                  <button class="btn success" @click="setTransaction('-')">
                    −
                  </button>
                </td>
              </tr>
              <tr>
                <td><button class="btn notSuccess">Ans</button></td>
                <td><button class="btn notSuccess">EXP</button></td>
                <td>
                  <button class="btn notSuccess">x<sup>y</sup></button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('0')">0</button>
                </td>
                <td>
                  <button class="btn bgDark" @click="setNumber('.')">.</button>
                </td>
                <td>
                  <button
                    class="btn bg-success text-white"
                    @click="resultTrans()"
                  >
                    =
                  </button>
                </td>
                <td>
                  <button class="btn success" @click="setTransaction('+')">+</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  @Prop({ default: "Calculator App" })
  private msg!: string;

  @Prop({ default: "" })
  private number1!: string;

  @Prop({ default: "" })
  private number2!: string;

  @Prop({ default: "" })
  private result!: number;

  @Prop({ default: "" })
  private trans!: any;

  private setNumber(x: string): void {
    this.result = null;
    if (this.trans != "") {
      if (this.trans == "!") this.trans = "!×";
      this.number2 = this.number2 + x;
    } else this.number1 = this.number1 + x;
  }

  private setTransaction(trans: string): void {
    if (this.number2 != "") this.trans = "!×";
    else this.trans = trans;
  }

  private resultTrans() {
    var number1 = parseFloat(this.number1);
    var number2 = parseFloat(this.number2);
    var factorial = 1;
    var i = 1;

    if (this.trans == "+") this.result = number1 + number2;
    else if (this.trans == "-") this.result = number1 - number2;
    else if (this.trans == "*") this.result = number1 * number2;
    else if (this.trans == "/") this.result = number1 / number2;
    else if (this.trans == "%") this.result = number1 % number2;
    else if (this.trans == "!") {
      if (number1 > 0) {
        for (i = 1; i <= number1; i++) {
          factorial = factorial * i;
        }
        this.result = factorial;
      }
    } else if (this.trans == "!×") {
      if (number1 > 0) {
        for (i = 1; i <= number1; i++) {
          factorial = factorial * i;
        }
        this.result = factorial * number2;
      }
    }

    this.number1 = "";
    this.number2 = "";
    this.trans = "";
  }

  private deleteScreen() {
    if (this.number2 != "")
      this.number2 = this.number2.slice(0, this.number2.length - 1);
    else if (this.trans != "") this.trans = "";
    else if (this.number1 != "")
      this.number1 = this.number1.slice(0, this.number1.length - 1);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.calculator {
  background: rgba(0, 0, 0, 0.11);
  padding: 20px;
  border-radius: 5px;
  .table {
    margin: 0;
  }
  &:not(caption) > * > * {
    border: 0 !important;
    box-shadow: none !important;
  }
  td {
    width: calc(100% / 7);
  }
  .screen {
    background: #cecfac;
    color: #3b3b32;
    margin: 0;
    text-align: right;
    line-height: 50px;
    height: 50px;
    padding-right: 10px;
    font-size: 35px;
    box-shadow: inset 0 0px 8px rgba(0, 0, 0, 0.5), inset 0px 2px 0 #a1a1a1;
  }
  .btn {
    background: #efefef;
    padding: 10px 0;
    border-radius: 5px;
    color: #737373;
    font-size: 18px;
    box-shadow: 0 5px 0 #a1a1a1, 0 2px 5px rgba(0, 0, 0, 0.75);
    width: 100%;
    font-weight: bold;
    position: relative;
    &:active {
      position: relative;
      top: 5px;
      box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.4);
    }
    &:is(.bgDark) {
      background: rgba(0, 0, 0, 0.2);
      color: white;
    }
    &:is(.success, .notSuccess) {
      &:before {
        content: "✓";
        position: absolute;
        left: 5px;
        top: 5px;
        background: rgb(58, 255, 0);
        width: 15px;
        height: 15px;
        font-size: 10px;
        display: flex;
        align-items: center;
        align-content: center;
        border-radius: 50%;
        text-align: center;
        padding: 4px 0 0 2px;
      }
    }
    &:is(.notSuccess) {
      &:before {
        content: "×";
        background: #ff0000;
        padding: 0 3px;
        color: white;
      }
    }
  }
}
.table > :not(:first-child) {
  border-top: 2px solid currentColor;
  border: 0 !important;
}
tbody,
td,
tfoot,
th,
thead,
tr {
  border: 0;
}
</style>
