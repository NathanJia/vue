<template>
  <div class="slide-show"
       @mouseover="clearInv"
       @mouseout="runInv">
    <!--when mouse is above, stop changing
       when mouse leaves, continue changing-->

    <!--images-->
    <div class="slide-img">
      <a>
        <!--animation effect-->
        <transition name="slide-trans">
          <img v-if='isShow' :src="slides[nowIndex].src">
        </transition>
        <transition name="slide-trans-old">
          <img v-if="!isShow" :src="slides[nowIndex].src">
        </transition>
      </a>
    </div>

    <!--image title-->
    <h2>{{ slides[nowIndex].title }}</h2>

    <!--select bar-->
    <ul class="slide-pages">
      <li @click="goto(PrevIndex)"><</li>
      <li v-for="(item,index) in slides"
          @click="goto(index)">
        <a :class="{on: index === nowIndex}"><!--high light-->
          {{ index + 1}}
        </a>
      </li>
      <li @click="goto(NextIndex)">></li>
    </ul>

  </div>
</template>

<script>
  export default {

    //data from parent components
    props: {
      slides: {
        type: Array,
        default: []
      },
      inv: {
        type: Number,
        dafault: 1000
      }
    },

    //data of this components-->
    data() {
      return {
        //index of image
        nowIndex: 0,
        //whether the image has been shown
        isShow : true
      }
    },

    //computed attributes-->
    computed: {
      PrevIndex() {
        if (this.nowIndex === 0) {
          return this.slides.length - 1
        }
        else {
          return this.nowIndex - 1
        }
      },
      NextIndex() {
        if (this.nowIndex === this.slides.length - 1) {
          return 0
        }
        else {
          return this.nowIndex + 1
        }
      },
    },
    methods: {

      //when arrow is clicked, go to next page-->
      goto(index) {
        this.isShow = false
        setTimeout(() => {this.isShow = true
          this.nowIndex = index
        }, 10)//after 10ms, change the index and isShow
      },

      //automatically change images-->
      runInv() {
        this.invId = setInterval(() => {
          this.goto(this.NextIndex)
        }, this.inv)//after this.inv, call goto
      },

      //when mouse is above the select bar, stop automatic changing
      clearInv(){
        clearInterval(this.invId)
      }
    },

    //run runInv()
    mounted(){
      this.runInv()
    }
  }
</script>

<!--style written by the teacher-->
<style scoped>
  .slide-trans-enter-active {
    transition: all .5s;
  }
  .slide-trans-enter {
    transform: translateX(900px);
  }
  .slide-trans-old-leave-active {
    transition: all .5s;
    transform: translateX(-900px);
  }
  .slide-show {
    position: relative;
    margin: 15px 15px 15px 0;
    width: 900px;
    height: 500px;
    overflow: hidden;
  }
  .slide-show h2 {
    position: absolute;
    width: 100%;
    height: 100%;
    color: #fff;
    background: #000;
    opacity: .5;
    bottom: 0;
    height: 30px;
    text-align: left;
    padding-left: 15px;
  }
  .slide-img {
    width: 100%;
  }
  .slide-img img {
    width: 100%;
    position: absolute;
    top: 0;
  }
  .slide-pages {
    position: absolute;
    bottom: 10px;
    right: 15px;
  }
  .slide-pages li {
    display: inline-block;
    padding: 0 10px;
    cursor: pointer;
    color: #fff;
  }
  .slide-pages li .on {
    text-decoration: underline;
  }
</style>
