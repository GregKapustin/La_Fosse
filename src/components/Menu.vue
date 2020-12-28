<template>
  <div id="menu">
    <div class="item">
      <div class="menu_icon">
        <font-awesome-icon icon="cogs" />
      </div>
      <div class="menu_stuff" id="params">
        <h1>{{ texts[lang].params }}</h1>

        <div class="columns is-vcentered">
          <div class="column align-left">
            <h2>{{ texts[lang].language }} :</h2>
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

        <div class="columns is-vcentered">
          <div class="column align-left">
            <h2>{{ texts[lang].article.title }} :</h2>
          </div>
          <div class="column align-right">
            <b-field>
              <b-radio-button v-model="articleCopy" @click="articleChange" native-value="interactive" size="is-small" type="is-dark">
                <span>{{ texts[lang].article.interactive }}</span>
              </b-radio-button>
              <b-radio-button v-model="articleCopy" @click="articleChange" native-value="read" size="is-small" type="is-dark">
                <span>{{ texts[lang].article.read }}</span>
              </b-radio-button>
            </b-field>
          </div>
        </div>

        <div class="columns is-vcentered">
          <div class="column align-left">
            <h2>{{ texts[lang].graph }} :</h2>
          </div>
          <div class="column align-right">
            <b-field>
              <b-radio-button v-model="graphTypeCopy" @click="graphChange" native-value="bar" size="is-small" type="is-dark">
                <span>{{ texts[lang].bars }}</span>
              </b-radio-button>
              <b-radio-button v-model="graphTypeCopy" @click="graphChange" native-value="radar" size="is-small" type="is-dark">
                <span>{{ texts[lang].radar }}</span>
              </b-radio-button>
              <b-radio-button v-model="graphTypeCopy" @click="graphChange" native-value="none" size="is-small" type="is-dark">
                <span>X</span>
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
      <div class="menu_stuff align-left" id="about">
        <h1>{{ texts[lang].about.title }}</h1>
        <div class="menu_stuff_content" v-for="(content, i) in texts[lang].about.content" v-html="content" :key="'content_' + i" />
      </div>
    </div>
    <div class="item">
      <div class="menu_icon">
        <font-awesome-icon icon="copyright" />
      </div>
      <div class="menu_stuff align-left" id="copyright">
        <h1>{{ texts[lang].copyright.title }}</h1>
        <div class="menu_stuff_content" v-for="(content, i) in texts[lang].copyright.content" v-html="content" :key="'copyright_' + i" />
      </div>
    </div>
    <div class="item">
      <div class="menu_icon">
        <font-awesome-icon icon="comments" />
      </div>
      <div class="menu_stuff align-left" id="contact">
        <h1>{{ texts[lang].contact.title }}</h1>
        <div class="menu_stuff_content" v-for="(content, i) in texts[lang].contact.content" v-html="content" :key="'contact_' + i" />
      </div>
    </div>
  </div>
</template>

<script>
import texts from '../assets/menu.json'

export default {
  name: 'Menu',
  components: {},
  props: {
    graphChange: Function,
    graphType: String,
    langChange: Function,
    lang: String,
    articleChange: Function,
    articleType: String
  },
  data: () => {
    return {
      texts
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
    },
    articleCopy: {
      get() {
        return this.articleType
      },
      set(value) {
        this.articleChange(value)
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
  color: #34495e;
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
  transition: 0.5s all ease;
}
#menu .item .menu_stuff {
  width: 0;
  height: 0;
  overflow: hidden;
  transition: 0.5s all ease;
  font-family: 'Roboto';
}
#menu .item:hover .menu_stuff {
  width: 460px;
  height: auto;
  padding: 20px;
  overflow: auto;
}
#menu .item:hover .menu_icon {
  opacity: 0
}
h1 {
  font-family: 'Anton';
  font-style: italic;
  color: #34495e;
  font-size: 50px;
  line-height: 50px;
  padding: 0px 15px 15px 15px;
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
<style>
.menu_stuff .img {
  display: inline;
  height: 20px;
  width: auto;
}
.menu_stuff#contact .img {
  display: inline;
  height: 60px;
  width: auto;
}
a {
  color: white!important;
  background: #34495e;
  padding: 1px 3px;
  border-radius: 2px;
  transition: 0.5s all ease;
}
a:hover {
  background-color: rgb(180, 180, 255);
  color: black!important;
}
#contact a {
  background: transparent;
}
</style>
