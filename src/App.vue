<template>
  <div class="sky">
    <div id="snow-container"></div>
  </div>
</template>

<script>
export default {
  name: "App",
  created() {
    document.title = "Snow Falling with Starry Sky";
  },
  mounted() {
    this.startSnowfall();
  },
  methods: {
    startSnowfall() {
      const snowContainer = document.getElementById('snow-container');

      // 눈덩이 생성 함수
      const createSnowflake = () => {
        const snowflake = document.createElement('div');
        snowflake.classList.add('snowflake');

        // 랜덤 크기
        const size = Math.random() * 5 + 2 + 'px';
        snowflake.style.width = size;
        snowflake.style.height = size;

        // 랜덤 시작 위치
        snowflake.style.left = Math.random() * window.innerWidth + 'px';

        // 랜덤 속도 (애니메이션 지속 시간)
        const duration = Math.random() * 3 + 2 + 's';
        snowflake.style.animationDuration = duration;

        snowContainer.appendChild(snowflake);

        // 눈덩이가 화면 아래로 내려가면 제거
        setTimeout(() => {
          snowflake.remove();
        }, parseFloat(duration) * 1000);
      };

      // 일정 시간마다 눈덩이 생성
      setInterval(createSnowflake, 200);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
}

body {
  margin: 0;
  background: linear-gradient(to bottom, #1c1f5a, #090c30);
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  text-align: center;
}

.sky::before {
  content: '';
  width: 100%;
  height: 100%;
  background: transparent url('https://www.transparenttextures.com/patterns/stardust.png');
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0.3;
}

#snow-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.snowflake {
  position: absolute;
  top: -10px;
  background-color: white;
  border-radius: 50%;
  opacity: 0.8;
  animation: fall linear infinite;
}

@keyframes fall {
  to {
    transform: translateY(100vh);
  }
}
</style>
