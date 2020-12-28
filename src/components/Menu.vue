<template>
  <div id="menu">
    <div class="item">
      <div class="menu_icon">
        <font-awesome-icon icon="cogs" />
      </div>
      <div class="menu_stuff" id="params">
        <h1>Params</h1>

        <div class="columns is-vcentered">
          <div class="column align-left">
            <h2>Graph :</h2>
          </div>
          <div class="column align-right">
            <b-field>
              <b-radio-button v-model="graphTypeCopy" @click="graphChange" native-value="bar" size="is-small" type="is-dark">
                <span>Bars</span>
              </b-radio-button>
              <b-radio-button v-model="graphTypeCopy" @click="graphChange" native-value="radar" size="is-small" type="is-dark">
                <span>Radar</span>
              </b-radio-button>
              <b-radio-button v-model="graphTypeCopy" @click="graphChange" native-value="none" size="is-small" type="is-dark">
                <span>X</span>
              </b-radio-button>
            </b-field>
          </div>
        </div>
        <div class="columns is-vcentered">
          <div class="column align-left">
            <h2>Language :</h2>
          </div>
          <div class="column align-right">
            <b-field>
              <b-radio-button v-model="langCopy" @click="langChange" native-value="en" size="is-small" type="is-dark">
                <span>English</span>
              </b-radio-button>
              <b-radio-button v-model="langCopy" @click="langChange" native-value="fr" size="is-small" type="is-dark">
                <span>Français</span>
              </b-radio-button>
            </b-field>
          </div>
        </div>
      </div>
    </div>
    <div class="item">
      <div class="menu_icon">
        <font-awesome-icon icon="question-circle" />
      </div>
      <div class="menu_stuff" id="about">
        <h1>What is this ?!</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  components: {},
  props: {
    graphChange: Function,
    graphType: String,
    langChange: Function,
    lang: String,
  },
  data: () => {
    return {
    }
  },
  computed: {
    graphTypeCopy: {
      get() {
        return this.graphType
      },
      set(value) {
        this.graphChange(value)
      }
    },
    langCopy: {
      get() {
        return this.lang
      },
      set(value) {
        this.langChange(value)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#menu {
  position: fixed;
  z-index: 120;
  top: 0;
  right: 0;
}
#menu .item {
  display: block;
  float: left;
  min-width: 50px;
  min-height: 50px;
  margin-top: 0px;
  background: white;
  margin-right: 30px;
  transition: 0.5s all ease;
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  box-shadow: 5px 3px 3px black;
}
#menu .item:hover {
  margin-top: 0
}
#menu .item .menu_icon {
  margin-top: 7px;
  width: 100%;
  text-align: center;
  font-size: 25px;
}
#menu .item .menu_stuff {
  width: 0;
  height: 0;
  overflow: hidden;
  transition: 0.5s all ease;
}
#menu .item:hover .menu_stuff {
  width: 460px;
  height: 460px;
  padding: 20px;
}
h1 {
  font-family: 'Anton';
  font-style: italic;
  color: #34495e;
  font-size: 50px;
  line-height: 50px;
  padding: 15px;
  margin-bottom: 35px;
  border-bottom: solid 1px silver;
}
h2 {
  font-family: 'Teko';
  color: #34495e;
  font-size: 30px;
  line-height: 30px;
  padding: 10px;
}
.align-left {
  text-align: left;
}
.align-right {
  text-align: right;
}
</style>
