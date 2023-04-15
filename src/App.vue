<template>
  <div class="main">
    <div class="header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>    

    <RoundOne
      :cards="cards"
    />

  </div>
</template>
<script>
import RoundOne from './views/RoundOne.vue';

export default {
  name: 'App',
  components: {
    RoundOne
  },
  data() {
    return {
      cards: [
        {
          word: 'Accountability',
          important: true
        },
        {
          word: 'Achievement',
          important: true
        },
        {
          word: 'Teamwork',
          important: true
        },
        {
          word: 'Thrift',
          important: true
        },
        {
          word: 'Time',
          important: true
        }
      ]
    }
  }
}
</script>
<style lang="scss">
body {
  font-family: 'Nunito', sans-serif;
  background-color: #D6D6D6;
}

.main {
  width: 400px;
  margin: 0 auto;
}
.header {
  h1, p {
    margin: 0;
    padding: 0;
    text-align: center;
  }
}

.title {
  h2 {
    margin: 0;
    padding: 0;
    text-align: center;
  }
}

.number {
  padding-top: 2rem;
  text-align: center;
  line-height: 26px;
  span {
    display: inline-block;
    background-color: #fff;
    border-radius: 100px;
    width: 24px;
    height: 24px;
    color: red;
    font-weight: bold;
  }
}
.controls {
  display: flex;
  flex-direction: row;
  column-gap: 16px;
  padding: 24px;
  justify-content: center;
  margin-top: 2rem;
}

button,
.btn {
  position: relative;
  display: inline-flex;
  text-decoration: none;
  font-weight: bold;
  align-items: center;
  justify-content: center;
  //
  background-color: #fff;
  border: none;
  outline: none;
  height: 120px;
  cursor: pointer;
  border-radius: 160px;
  width: 80px;
  height: 80px;
  transition: all 60ms linear;

  &:hover {
    background-color: #333333;
    color: #fff;
  }
}

.btn--reset {
  width: auto;
  background-color: transparent;
  border: none;
  text-decoration: underline;
  display: inline;
  height: auto;
  padding: 1rem 0;
}

.hide-this, .hidden {
  visibility: hidden;
  opacity: 0;
}

.card {
  border-radius: 8px;
  background-color: #F4F4F4;
  color: #454545;
  border: 16px solid #FCFCFC;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 210px;
  justify-content: center;
  align-content: center;
  box-shadow:
    0px 2.8px 2.2px rgba(0, 0, 0, 0.02),
    0px 6.7px 5.3px rgba(0, 0, 0, 0.028),
    0px 12.5px 10px rgba(0, 0, 0, 0.035);

  h3 {
    font-size: 36px;
  }
  &--deck-starter {
    cursor: pointer;
    h3 {
      font-size: 1rem;
      color: salmon;
      font-weight: bold;
    }
    &:hover {
      background-color:#ececec;
    }

  }
}
</style>