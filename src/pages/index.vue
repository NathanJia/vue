<template>
  <div class="index-wrap">
    <div class="index-left">

      <!--left block of the web-->
      <div class="index-left-block">
        <h2>Useful links</h2>
        <template v-for="links in urlList">
          <h3>{{ links.title }}</h3>
          <ul>
            <li v-for="item in links.list">
              <a target='_blank' :href="item.url">{{ item.name }}</a>
              <span v-if="item.hot" class="hot-tag">HOT</span>
            </li>
          </ul>
          <div v-if="!links.last" class="hr"></div>
        </template>
      </div>

      <!--to do list-->
      <div class="index-left-block to-do-list">
        <h2>Todo list</h2>
        <ul>
          <li v-for="item in todoList">
            <a>{{ item.thing }} ----- {{ item.time }}</a>
          </li>
        </ul>
      </div>
    </div>

    <!--right part of the web-->
    <div class="index-right">

      <!-- display slides-->
      <slide-show :slides='slides' :inv="slidespeed">
      </slide-show>

      <!--display blocks-->
      <div class="index-board-list">
        <div class="index-board-item"
             v-for="(item,index) in boardList"
        :class="[
          {'line-last': index % 2 !== 0},// display straight line
          'index-board-' + item.id// display images
          ]"
        >
          <div class="index-board-item-inner">
            <h2>{{ item.title }}</h2>
            <p>{{ item.description }}</p>
            <div class="index-board-button">
              <button @click="">upvote</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import slideShow from '../components/slideShow'
export default{
  components:{
    slideShow
  },
  data(){
    return {

      //control slide speed(in component slideShow)
      slidespeed: 2000,

      //slides for the right part
      slides: [
        {
          src: require('../assets/slideShow/pic1.jpg'),
          title: 'picture1',
          href: 'detail/analysis'
        },
        {
          src: require('../assets/slideShow/pic2.jpg'),
          title: 'picture2',
          href: 'detail/count'
        },
        {
          src: require('../assets/slideShow/pic3.jpg'),
          title: 'picture3',
          href: 'http://xxx.xxx.com'
        },
        {
          src: require('../assets/slideShow/pic4.jpg'),
          title: 'picture4',
          href: 'detail/forecast'
        }
      ],

      //list for the right part
      boardList: [
        {
          title: 'thinking ability',
          description: 'it is important to enhance it',
          id: 'car',
          toKey: 'useless',
          saleout: false
        },
        {
          title: 'insistence',
          description: 'insistence helps you win everyday',
          id: 'loud',
          toKey: 'useful',
          saleout: false
        },
        {
          title: 'communication',
          description: 'communication is the best way to solve problems',
          id: 'earth',
          toKey: 'useful',
          saleout: true
        },
        {
          title: 'teamwork',
          description: 'working together is also important',
          id: 'hill',
          toKey: 'useless',
          saleout: false
        }
      ],

      //for left part
      todoList:[
        {
          thing :'ics test',
          time:'11.04'
        },
        {
          thing :'phy lab',
          time:'15:00'
        },
        {
          thing :'coding',
          time:'everyday'
        },
        {
          thing :'new words',
          time:'everyday'
        },
        {
          thing :'prp',
          time:'thursday night'
        }
      ],

      //for left part
      urlList:{
        uls:{
          title : 'Go to courses',
          list :[
            {
              name:'ICS',
              url:'http://ipads.se.sjtu.edu.cn/courses/ics/schedule.shtml',
              hot:true
            },
            {
              name:'physics',
              url:'http://phycai.sjtu.edu.cn/wis/student/studentcoursehostnew.aspx'
            },
            {
              name:'physics labs',
              url:'http://www.phycai.sjtu.edu.cn/PE/student/student.aspx'
            },
            {
              name:'algorithms',
              url:'https://basics.sjtu.edu.cn/~liguoqiang/teaching/Ualgo17/index.htm',
              hot :true
            }
          ]
        },
        app:{
          title : 'App links',
          last : true,
          list :[
            {
              name:'github',
              url:'https://github.com/',
              hot :true
            },
            {
              name:'bilibili',
              url:'https://www.bilibili.com/'
            },
            {
              name:'POJ',
              url:'http://poj.org/'
            },
            {
              name:'leetcode',
              url:'http://blog.csdn.net/column/details/leetcode-solution.html',
              hot :true
            }
          ]
        }
      }
    }
  },

  //upvoter from the slideshow component
  methods:{
    upOne(){
      console.log('upvoted!')
    }
  }
}
</script>

<style scoped>
  .index-wrap {
    width: 1200px;
    margin: 0 auto;
    overflow: hidden;
  }
  .index-left {
    float: left;
    width: 300px;
    text-align: left;
  }
  .index-right {
    float: left;
    width: 900px;
  }
  .index-left-block {
    margin: 15px;
    background: #fff;
    box-shadow: 0 0 1px #ddd;
  }
  .index-left-block .hr {
    margin-bottom: 20px;
  }
  .index-left-block h2 {
    background: #4fc08d;
    color: #fff;
    padding: 10px 15px;
    margin-bottom: 20px;
  }
  .index-left-block h3 {
    padding: 0 15px 5px 15px;
    font-weight: bold;
    color: #222;
  }
  .index-left-block ul {
    padding: 10px 15px;
  }
  .index-left-block li {
    padding: 5px;
  }
  .index-board-list {
    overflow: hidden;
  }
  .index-board-item {
    float: left;
    width: 400px;
    background: #fff;
    box-shadow: 0 0 1px #ddd;
    padding: 20px;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .index-board-item-inner {
    min-height: 125px;
    padding-left: 120px;
  }
  .index-board-car .index-board-item-inner{
    background: url(../assets/images/1.png) no-repeat;
  }
  .index-board-loud .index-board-item-inner{
    background: url(../assets/images/2.png) no-repeat;
  }
  .index-board-earth .index-board-item-inner{
    background: url(../assets/images/3.png) no-repeat;
  }
  .index-board-hill .index-board-item-inner{
    background: url(../assets/images/4.png) no-repeat;
  }
  .index-board-item h2 {
    font-size: 18px;
    font-weight: bold;
    color: #000;
    margin-bottom: 15px;
  }
  .line-last {
    margin-right: 0;
  }
  .index-board-button {
    margin-top: 20px;
  }
  .lastest-news {
    min-height: 512px;
  }
  .hot-tag {
    background: red;
    color: #fff;
  }
  .new-item {
    display: inline-block;
    width: 230px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
</style>
