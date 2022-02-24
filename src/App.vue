<template>
  <div class="main-parent">
    <div class="parent">
      <div class="digits">
        <div class="Quarter nf">
          <p class="third">11</p>
          <p class="second">10</p>
          <p class="first">9</p>
        </div>
        <div class="Quarter fh">
          <p class="third">2</p>
          <p class="second">1</p>
          <p class="first">12</p>
        </div>
        <div class="Quarter fv">
          <p class="third">8</p>
          <p class="second">7</p>
          <p class="first">6</p>
        </div>
        <div class="Quarter fvh">
          <p class="third">5</p>
          <p class="second">4</p>
          <p class="first">3</p>
        </div>
      </div>
      <div class="dial" :style="{ transform: 'rotate(' + secondsDeg + 'deg)'}">
        <span class="seconds"></span>
      </div>
      <div class="dial" :style="{ transform: 'rotate(' + minutesDeg + 'deg)'}">
        <span class="minutes"></span>
      </div>
      <div class="dial" :style="{ transform: 'rotate(' + hoursDeg + 'deg)'}">
        <span class="hours"></span>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {
    
  },
  data() {
    return {
      secondsDeg: Number,
      minutesDeg: Number,
      hoursDeg: Number,
    }
  },
  methods: {
    setDate() {
      const now = new Date;
      this.secondsDeg = 6 * now.getSeconds();
      this.minutesDeg = (now.getMinutes() + ((now.getSeconds())*(100/60)/100)) * 6 ;
      const hours = (now.getHours() > 12 ? now.getHours()-12 : now.getHours());
      this.hoursDeg = (hours + ((now.getMinutes())*(100/60)/100)) * 15;
    },
  },
  created() { 
    this.setDate();
    setInterval(() => {
      this.setDate();
    }, 1000);

  }
}

</script>

<style>

body.dark {
  --backgroundColor: linear-gradient(90deg, rgba(8,0,140,1) 0%, rgba(0,0,107,1) 50%, rgba(0,0,162,1) 100%);
  --textColor: white;
  --minutesDial: white;
  --hoursDial: white;
}
body {
  --backgroundColor: white;
  --textColor: black;
  --minutesDial: black;
  --hoursDial: black;
}

body {
  background: var(--backgroundColor);
  color: var(--textColor);
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  overflow: hidden;
}
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
.main-parent {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.parent {
  width: 500px;
  height: 500px;
  position: relative;
}
.digits {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  width: 100%;
  height: 100%;
}
/*No Flip element*/
.nf {

}
/*Fliping element horizontaly*/
.fh {
  transform: rotate(90deg);
}
/*Fliping element verticaly */
.fv {
  transform: rotate(-90deg);
}
/*fliping element Vertically and horizontally */
.fvh {
  transform: rotate(180deg);
}


.Quarter {
  position: relative;
}
.Quarter > p {
  position: absolute;
  font-size: 1.7rem;
}
.nf > p {
  transform: rotate(0deg) translate(50%, 50%);
}
.fh > p {
  transform: rotate(-90deg) translate(-50%, 50%);
}
.fv > p {
  transform: rotate(90deg) translate(100%, -50%);
}
.fvh > p {
  transform: rotate(-180deg) translate(-50%, -50%);
}
.Quarter .first {
  bottom: 0%;
  right: 100%;
}
.Quarter .second {
  bottom: 50%;
  right: 86.60254%;
}
.Quarter .third {
  bottom: 86.60254%;
  right: 50%;
}



/*Dials*/

.dial {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
}
.dial span {
  width: 5px;
  border-radius: 10px;
  transform: translateY(-50%);
}
.dial .seconds {
  height: 35%;
  width: 2px;
  background: rgb(148, 0, 0);
}
.dial .minutes {
  height: 40%;
  width: 3px;
  background-color: var(--minutesDial);
}
.dial .hours {
  height: 30%;
  background-color: var(--hoursDial);
  width: 7px;
}
</style>
