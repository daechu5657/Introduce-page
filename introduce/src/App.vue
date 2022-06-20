<template>
  <div class="wrap">
    <div class="header">
      <div class="h-left">
        <p>Portfolio</p>
      </div>
      <div class="h-mid">
        <p>Home</p>
        <p>1</p>
        <p>2</p>
        <p>3</p>
      </div>
      <div class="h-right">
        <i class="fa-solid fa-bars" @click="sidebar_modal = 1"></i>
      </div>
    </div>
    <div class="contents">
      <div class="contents-home"></div>
      <div class="contents-1"></div>
      <div class="contents-2"></div>
      <div class="contents-3"></div>
    </div>
    <transition name="sidebar">
      <div class="sidebar" v-if="sidebar_modal == 1">
        <div class="close-btn">
          <i class="fa-solid fa-x" @click="sidebar_modal = 0"></i>
        </div>
        <div class="comments">
          <div class="comments-text">Comments</div>
        </div>
        <textarea class="comments-textarea" type="text" />
        <div class="comments-submit">Submit</div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},
  methods: {},
  data() {
    return {
      sidebar_modal: 0,
    };
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Staatliches&display=swap');
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
  overflow-y: hidden;
}
.wrap {
  width: 100vw;
  height: 400vh;
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
  opacity: 1;
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

.sidebar {
  position: fixed;
  width: 15vw;
  height: 100vh;
  background-color: #75757524;
  right: 0;
  backdrop-filter: blur(5px);
}
.sidebar-enter-active {
  animation: sidebar 0.3s ease;
}
.sidebar-leave-active {
  animation: sidebar 0.3s ease reverse;
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
.close-btn {
  font-size: 1vw;
  color: #f5f5f5;
  position: absolute;
  left: 1vw;
  top: 1vw;
}
.comments {
  position: relative;
  width: 14vw;
  height: 80vh;
  background-color: #f0f8ff26;
  top: 10vh;
  left: 0.5vw;
}
.comments-text {
  position: absolute;
  font-family: 'Staatliches', cursive;
  color: #f5f5f5;
  font-size: 1vw;
  top: -3vh;
}
.comments-textarea {
  position: absolute;
  width: 10vw;
  bottom: 5vh;
}
.comments-submit {
  position: absolute;
  position: absolute;
  font-family: 'Staatliches', cursive;
  color: #f5f5f5;
  font-size: 1vw;
  top: 93vh;
  right: 0.5vw;
}
</style>
