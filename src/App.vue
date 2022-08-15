<script>
export default {
  data() {
    return {
      header: "Login Page",
      showPass: false,
      passVal: null,
      // warn letter uppercase
      showWarnLetterUpper: false,
      warnLetterUpperText: null,
      // warn letter lowercase
      showWarnLetterLower: false,
      warnLetterLowerText: null,
      // warn number
      showWarnNum: false,
      warnNumText: null,
      // warn length
      showWarnLength: false,
      warnLengthText: null,
      // warn special
      showWarnSpecial: false,
      warnSpecialText: null,
    };
  },

  watch: {
    passVal(val) {
      let numVal = /[0-9]/g;
      let letterValLower = /[a-z]/g;
      let letterValUpper = /[A-Z]/g;
      let specialVal = /[^a-zA-Z0-9_]/g;

      // if pass val is less than 8
      if (val.length <= 8) {
        this.showWarnLength = true;
        this.warnLengthText = "Password must be 8 characters or more.";
      } else {
        this.showWarnLength = false;
        this.warnLengthText = null;
      }

      // if pass val has no number
      if (!val.match(numVal)) {
        this.showWarnNum = true;
        this.warnNumText = "Password at least have 1 number.";
      } else {
        this.showWarnNum = false;
        this.warnNumText = null;
      }

      // if pass val has no letter (UPPER)
      if (!val.match(letterValUpper)) {
        this.showWarnLetterUpper = true;
        this.warnLetterUpperText = "Password at least have 1 uppercase letter.";
      } else {
        this.showWarnLetterUpper = false;
        this.warnLetterUpperText = null;
      }

      // if pass val has no letter (LOWER)
      if (!val.match(letterValLower)) {
        this.showWarnLetterLower = true;
        this.warnLetterLowerText = "Password at least have 1 lowercase letter.";
      } else {
        this.showWarnLetterLower = false;
        this.warnLetterLowerText = null;
      }

      // if pass val has no special char
      if (!val.match(specialVal)) {
        this.showWarnSpecial = true;
        this.warnSpecialText = "Password at least have 1 special character.";
      } else {
        this.showWarnSpecial = false;
        this.warnSpecialText = null;
      }
    },
  },

  methods: {
    showPassMethod() {
      this.showPass = !this.showPass;
    },
  },
};
</script>

<template>
  <div id="app" class="container">
    <h2>{{ header }}</h2>

    <form>
      <div class="form-container">
        <div class="input-container">
          <input
            type="email"
            name="email"
            id="email"
            placeholder="email address"
            required
          />
        </div>

        <div class="input-container pass-container">
          <!-- if showPass is true then type input is text -->
          <input
            v-if="showPass"
            type="text"
            name="password"
            id="password"
            placeholder="your password"
            v-model="passVal"
            pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}"
            title="Password must be chars"
            required
          />

          <!-- if showPass is false then type input is password -->
          <input
            v-else
            type="password"
            name="password"
            id="password"
            placeholder="your password"
            v-model="passVal"
            pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}"
            required
          />
          <span @click="showPassMethod()">{{ showPass ? "H" : "S" }}</span>
        </div>

        <div id="warning-pass">
          <p v-show="showWarnLetterUpper" id="warn-letter" class="invalid-pass">
            {{ warnLetterUpperText }}
          </p>
          <p v-show="showWarnLetterLower" id="warn-letter" class="invalid-pass">
            {{ warnLetterLowerText }}
          </p>
          <p v-show="showWarnNum" id="warn-number" class="invalid-pass">
            {{ warnNumText }}
          </p>
          <p v-show="showWarnLength" id="warn-length" class="invalid-pass">
            {{ warnLengthText }}
          </p>
          <p v-show="showWarnSpecial" id="warn-length" class="invalid-pass">
            {{ warnSpecialText }}
          </p>
        </div>
        <button type="submit">Login</button>
      </div>
    </form>
  </div>
</template>

<style>
@import "./assets/base.css";
</style>
