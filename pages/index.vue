<template>
  <div>
    <!-- Main Menu Component -->
    <MainMenu />

    <!-- Gradient Background -->
    <div class="gradient-background" />
    <!-- Main content area -->
    <main class="flex-grow-1">
      <div class="contents">
        <div class="con1">Section 1</div>
        <div class="con2">Section 2</div>
        <div class="con3">Section 3</div>
        <div class="con4">Section 4</div>
        <div class="con5">Section 5</div>
      </div>
    </main>

    <!-- Footer Component -->
    <Footer />
  </div>
</template>

<script>
export default {
    mounted() {
      this.updateGradient();
      this.setupScrollBehavior();
    },
    methods: {
      updateGradient() {
        const colors = [
          [198, 255, 221],
          [251, 215, 134],
          [247, 121, 125],
          [232, 203, 192],
          [99, 111, 164],
          [237, 66, 100]
        ];

        let step = 0;
        const colorIndices = [0, 1, 2, 3];
        const gradientSpeed = 0.002;

        const update = () => {
          const c00Color = colors[colorIndices[0]];
          const c01Color = colors[colorIndices[1]];
          const c10Color = colors[colorIndices[2]];
          const c11Color = colors[colorIndices[3]];

          const istep = 1 - step;
          const r1 = Math.round(istep * c00Color[0] + step * c01Color[0]);
          const g1 = Math.round(istep * c00Color[1] + step * c01Color[1]);
          const b1 = Math.round(istep * c00Color[2] + step * c01Color[2]);
          const color1 = `rgb(${r1},${g1},${b1})`;

          const r2 = Math.round(istep * c10Color[0] + step * c11Color[0]);
          const g2 = Math.round(istep * c10Color[1] + step * c11Color[1]);
          const b2 = Math.round(istep * c10Color[2] + step * c11Color[2]);
          const color2 = `rgb(${r2},${g2},${b2})`;

          // Apply background gradient to the .gradient-background div
          document.querySelector('.gradient-background').style.background = `linear-gradient(to right, ${color1}, ${color2})`;

          step += gradientSpeed;
          if (step >= 1) {
            step %= 1;
            colorIndices[0] = colorIndices[1];
            colorIndices[2] = colorIndices[3];
            colorIndices[1] = (colorIndices[1] + Math.floor(1 + Math.random() * (colors.length - 1))) % colors.length;
            colorIndices[3] = (colorIndices[3] + Math.floor(1 + Math.random() * (colors.length - 1))) % colors.length;
          }

          requestAnimationFrame(update);
        };

        update();
      },

      setupScrollBehavior() {
        document.querySelector('.contents').addEventListener('wheel', (event) => {
          let k = parseInt(event.currentTarget.getAttribute("data-n")) - Math.sign(event.deltaY);

          if (k < 1) k = 1;
          if (k > 5) k = 5;

          const target = document.querySelector(`.con${k}`).offsetTop;
          window.scrollTo({ top: target, behavior: 'smooth' });

          event.preventDefault();
        });

        window.addEventListener('scroll', () => {
          const sections = document.querySelectorAll('.con1, .con2, .con3, .con4, .con5');
          const scroll = window.scrollY;

          sections.forEach((section, index) => {
            if (scroll >= section.offsetTop) {
              document.querySelectorAll("#main_menu ul li a")[index].classList.add('on');
              document.querySelectorAll('.btn')[index].classList.add('sel');
            } else {
              document.querySelectorAll("#main_menu ul li a")[index].classList.remove('on');
              document.querySelectorAll('.btn')[index].classList.remove('sel');
            }
          });
        });
      }
    }
};
</script>

<style scoped>
.gradient-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.contents {
  /*padding-top: 50px; */
}

.con1, .con2, .con3, .con4, .con5 {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}
/*
.con1 { background-color: rgba(0, 0, 0, 0.5); }
.con2 { background-color: rgba(0, 0, 0, 0.6); }
.con3 { background-color: rgba(0, 0, 0, 0.7); }
.con4 { background-color: rgba(0, 0, 0, 0.8); }
.con5 { background-color: rgba(0, 0, 0, 0.9); }
*/

#main_menu ul li a.on {
  color: #ff0; /* Highlight active menu items */
}

.btn.sel {
  background-color: #ff0; /* Style active buttons */
}
</style>
