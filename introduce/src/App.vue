<template>
  <div class="wrap">
    <div class="header">
      <div class="h-left">
        <p>Portfolio</p>
      </div>
      <div class="h-mid">
        <p>HOME</p>
        <p>ABOUT ME</p>
        <p>CREATIVES</p>
        <p>CONTACT</p>
      </div>
      <div class="h-right">
        <div
          class="menu"
          :class="{ active: sidebar_modal == 1 }"
          @click="sidebar_mOnOff"
        >
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </div>
    <div class="contents">
      <div class="contents-home" id="home">
        <div class="home-title">
          Daeho Kim <br />
          <p>Front-end Developer/ Aiming for growth</p>
          <div class="home-title-bar"></div>
        </div>
        <img class="profileimg" src="./assets/man.png" alt="" />
        <div class="home-view">
          <div class="home-view-bar"></div>
          View
          <span class="home-view-arrow updown">↓</span>
        </div>
      </div>
      <div class="contents-about" id="about">
        <img class="about-img" src="./assets/man.png" alt="" />
        <div class="about-name">Daeho KIm(1998)</div>
        <div class="about-introduce1">좌절에서 열정으로 , 변곡점의 필요.</div>
        <div class="about-introduce2">
          스스로 발전하는 단단한 인물이되야겠다는 다짐.
        </div>
        <div class="about-introduce3">
          즉각적인 결과 도출 , 표현의 다양성 , 창의성 , 짜임새
        </div>
        <div class="about-introduce4">
          프로젝트를 진행하면서 <br />
          나도 할수있다는 자신감과 성취감이 제자신을 열정으로 가득차게
          해준것같습니다
        </div>
        <div class="about-introduce5">
          열정넘치는 신입 프론트엔드 김대호입니다.
        </div>
        <div class="about-education">백석문화대 졸업 (4.2)</div>
        <div class="about-certificate">GTQ 1급</div>
      </div>
      <div class="contents-creative" id="creative"></div>
      <div class="contents-contact" id="contact"></div>
    </div>
    <transition name="sidebar">
      <div class="sidebar" v-if="sidebar_modal == 1">
        <div class="comments">
          <div class="comments-text">Comments</div>
        </div>
        <div class="sidebar-bottom">
          <textarea class="comments-textarea" type="text" spellcheck="false" />
          <div class="comments-submit">Submit</div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},
  methods: {
    sidebar_mOnOff() {
      if (this.sidebar_modal == 0) {
        this.sidebar_modal = 1;
      } else {
        this.sidebar_modal = 0;
      }
    },
    scroll() {
      var Element = document.documentElement.scrollTop;
      this.scrollv = Element;
      let vh = window.innerHeight;
      this.vh = vh;
      const target = document.getElementById('home');
      const clientRect = target.getBoundingClientRect();
      const home_relativeTop = clientRect.top;
      // console.log(home_relativeTop);

      const scrolledTopLength = window.pageYOffset;
      console.log(scrolledTopLength);
      const home_absoluteTop = scrolledTopLength + home_relativeTop;
      // console.log(home_absoluteTop);

      const target_about = document.getElementById('about');
      const clientRect_about = target_about.getBoundingClientRect();
      const about_relativeTop = clientRect_about.top;

      // const scrolledTopLength = window.pageYOffset;
      const about_absoluteTop = scrolledTopLength + about_relativeTop;
      console.log(about_absoluteTop);

      const home = document.querySelector('#home');
      if (home_relativeTop / this.vh >= 0) {
        home.style.opacity = `${1 - home_absoluteTop / this.vh}`;
      } else if (home_relativeTop / this.vh <= 0) {
        home.style.opacity = `${1 + home_absoluteTop / this.vh}`;
      }
      const about = document.querySelector('#about');
      if (scrolledTopLength > 2 * this.vh) {
        console.log('지금');
        about.style.opacity = `${scrolledTopLength / this.vh}`;
      } else if (about_relativeTop / this.vh <= 0) {
        about.style.opacity = `${1 + about_absoluteTop / this.vh}`;
      }
    },
  },
  data() {
    return {
      sidebar_modal: 0,
      scrollv: 0,
      vh: 0,
      page: 0,
    };
  },
  computed: {
    ing() {
      return `
       top: ${this.page * 8}vh`;
    },
  },
  watch: {
    scrollv() {
      // if (val < this.vh) {
      //   // this.page = 0;
      // } else if (val > this.vh / 2) {
      //   // this.page = 1;
      //   window.scrollTo({ behavior: 'smooth', left: 0, top: this.vh * 2 });
      // }
    },
  },
  mounted() {
    window.addEventListener('scroll', this.scroll);
    setTimeout(() => {
      document.getElementById('home').classList.add('fadein');
    }, 1000);
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Staatliches&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Questrial&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@500&display=swap');
* {
  margin: 0;
  padding: 0;
}
div {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  overflow-x: hidden;
}
body::-webkit-scrollbar {
  display: none;
}
.wrap {
  width: 100vw;
  height: 1000vh;
  background-color: #161616;
  max-width: 100%;
}
.header {
  position: fixed;
  width: 100vw;
  height: 7vh;
  font-family: 'Staatliches', cursive;
  color: #f5f5f5;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background-color: transparent;
  z-index: 100;
}
.h-left {
  position: relative;
  width: 10vw;
  font-size: 2vw;
  text-align: left;
  padding-left: 1vw;
}
.h-mid {
  width: 20vw;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  font-size: 1vw;
}
.h-mid > p {
  position: relative;
}
.h-mid > p:after {
  left: -20%;
  content: '';
  position: absolute;
  bottom: 0.5vh;
  width: 0px;
  height: 1vh;
  transition: all 0.2s ease;
  transition-duration: 0.2s;
  opacity: 0.5;
  background-color: #f5f5f566;
  border-radius: 5px;
}
.h-mid > p:hover:after {
  width: 140%;
  opacity: 1;
  left: -20%;
}
.h-right {
  position: relative;
  width: 10vw;
  text-align: right;
  font-size: 1.2vw;
  color: #f5f5f5;
  padding-right: 1vw;
}
.menu {
  position: relative;
  width: 1.5vw;
  height: 2vh;
  left: 7.5vw;
  transition: all 0.3s cubic-bezier(0.455, 0.03, 0.515, 0.955);
}
.menu span {
  position: absolute;
  left: 0;
  width: 100%;
  height: 4px;
  background-color: #fff;
  border-radius: 2px;
  transition: all 0.3s cubic-bezier(0.455, 0.03, 0.515, 0.955);
}
.menu span:nth-of-type(1) {
  top: 0;
}

.menu span:nth-of-type(2) {
  top: 1vh;
}

.menu span:nth-of-type(3) {
  top: 2vh;
}
.menu.active span:nth-of-type(1) {
  -webkit-transform: translateY (1vh) rotate (-45deg);
  transform: translateY(1vh) rotate(-45deg);
}

.menu.active span:nth-of-type(2) {
  opacity: 0;
}

.menu.active span:nth-of-type(3) {
  -webkit-transform: translateY(-1vh) rotate(45deg);
  transform: translateY(-1vh) rotate(45deg);
}
.sidebar {
  position: fixed;
  width: 15vw;
  height: 100vh;
  background-color: #75757524;
  right: 0;
  top: 0;
  backdrop-filter: blur(5px);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  z-index: 10;
}
.sidebar-enter-active {
  animation: sidebar 0.3s cubic-bezier(0.455, 0.03, 0.515, 0.955);
}
.sidebar-leave-active {
  animation: sidebar 0.3s cubic-bezier(0.455, 0.03, 0.515, 0.955) reverse;
}
@keyframes sidebar {
  0% {
    opacity: 0;
    transform: translatex(15vw);
  }
  100% {
    opacity: 1;
    transform: translatex(0vw);
  }
}
.comments {
  position: relative;
  width: 14vw;
  height: 80vh;
  background-color: #ffffff0f;
  left: 0.5vw;
  top: 9vh;
}
.comments-text {
  position: absolute;
  font-family: 'Staatliches', cursive;
  color: #f5f5f5;
  font-size: 1vw;
  top: -3vh;
}
.sidebar-bottom {
  position: relative;
  width: 14vw;
  height: 10vh;
  left: 0.5vw;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.comments-textarea {
  position: relative;
  width: 12vw;
  height: 4vh;
  text-align: left;
  background-color: #ffffff0f;
  resize: none;
  font-family: 'Staatliches', cursive;
  font-family: 'Do Hyeon', sans-serif;
  border: none;
  outline: none;
  color: #f5f5f5;
  font-size: 0.6vw;
  overflow-y: hidden;
  padding: 0.1vh 1vw;
}
.comments-submit {
  position: relative;
  font-family: 'Staatliches', cursive;
  color: #f5f5f5;
  font-size: 1vw;
}
.comments-submit:after {
  left: -20%;
  content: '';
  position: absolute;
  bottom: 0.5vh;
  width: 0px;
  height: 1vh;
  transition: all 0.2s ease;
  transition-duration: 0.2s;
  opacity: 0.5;
  background-color: #f5f5f566;
  border-radius: 5px;
}
.comments-submit:hover:after {
  width: 140%;
  opacity: 1;
  left: -20%;
}
.contents {
  position: relative;
  width: 100vw;
  height: 400vh;
  background-color: transparent;
  font-family: 'Questrial', sans-serif;
}
.contents-home {
  position: fixed;
  width: 100vw;
  height: 200vh;
  background-attachment: fixed;
  transition: 1s ease;
}
.home-title {
  position: absolute;
  color: #f5f5f5;
  font-size: 3vw;
  top: 46vh;
  left: 15vw;
  line-height: 6.5vh;
}
.home-title > p {
  font-size: 1.5vw;
}
.home-title-bar {
  position: absolute;
  width: 0.1vw;
  height: -webkit-fill-available;
  background-color: #f5f5f5;
  top: 0;
  left: -1.3vw;
  border-radius: 10px;
}
.profileimg {
  position: absolute;
  width: 45vw;
  height: 64vh;
  left: 45vw;
  top: 36vh;
  filter: grayscale(100%);
}
.home-view {
  color: #f5f5f5;
  font-size: 1.5vw;
  position: absolute;
  top: 91vh;
  left: 15vw;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.home-view-bar {
  position: relative;
  width: 4vw;
  height: 0.1vw;
  top: 0;
  left: -1.3vw;
  border-top: 0.2vw dotted;
}
.home-view-arrow {
  position: relative;
  left: 1vw;
}
.contents-about {
  position: absolute;
  width: 100vw;
  height: 200vh;
  top: 200vh;
  background-attachment: fixed;
  font-family: 'Noto Sans KR', sans-serif;
  opacity: 0;
}
.about-img {
  position: relative;
  width: 10vw;
  height: 10vw;
  border-radius: 50%;
  top: 20vh;
  left: 30vw;
}
.contents-about > div {
  position: absolute;
  color: #f5f5f5;
  font-size: 1.5vw;
}
.about-name {
  left: 53vw;
}
.about-certificate {
  left: 20vw;
  top: 60vh;
}
.about-education {
  left: 16vw;
  top: 40vh;
}
.about-introduce1 {
  top: 51vh;
}
.about-introduce2 {
  top: 55vh;
}
.about-introduce3 {
  top: 59vh;
}
.about-introduce4 {
  top: 63vh;
}
.about-introduce5 {
  top: 68vh;
}
.updown {
  animation: updown 1s infinite ease-out;
}
@keyframes updown {
  0% {
    transform: translatey(0vh);
  }
  50% {
    transform: translatey(0.8vh);
  }
  100% {
    transform: translatey(0vh);
  }
}
.fadein {
  animation: fadein 1.5s ease;
}
@keyframes fadein {
  0% {
    opacity: 0;
    transform: translatey(5vh);
  }
  100% {
    opacity: 1;
    transform: translatey(0vh);
  }
}

.contents-creative {
  position: relative;
  width: 100vw;
  height: 100vh;
  background-attachment: fixed;
}
.contents-contact {
  position: relative;
  width: 100vw;
  height: 100vh;

  background-attachment: fixed;
}
</style>
