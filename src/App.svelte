<style lang="scss">
  $-red: hsl(4, 38%, 49%);
  $-darkorange: hsl(24, 51%, 55%);
  $-lightorange: hsl(35, 61%, 56%);
  $-yellow: hsl(51, 81%, 55%);

  $-lightblue: hsl(196, 69%, 46%);
  $-blue: hsl(201, 80%, 37%);
  $-darkblue: hsl(206, 88%, 32%);
  $-deepblue: hsl(210, 97%, 27%);

  main {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    font-size: 30px;
  }

  .background {
    position: absolute;
    width: 63%;
    height: 100%;
    z-index: -2;

    &.redish {
      top: 0;
      left: 0;
      background: linear-gradient(to bottom right, $-red 10%, $-darkorange 30%, $-lightorange 60%, $-yellow 80%) no-repeat border-box;
    }

    &.blueish {
      top: 0;
      right: 0;
      background: linear-gradient(to bottom right, $-lightblue 20%, $-blue 40%, $-darkblue 70%, $-deepblue 90%) no-repeat border-box;
      clip-path: polygon(30% 0%, 100% 0%, 100% 100%, 11% 100%);
    }

    &.grid {
      width: 100%;
      z-index: -1;
      background-size: 30px 30px;
      background-image:
        linear-gradient(to right, hsl(0, 0%, 80%) 1px, transparent 1px),
        linear-gradient(to bottom, hsl(0, 0%, 80%) 1px, transparent 1px);
    }
  }

  section {
    display: grid;
    grid-template-rows: 70px 40px 70px 40px 70px;
    align-items: center;
    justify-items: center;
    width: 95%;
  }

  .circle {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 70px;
    height: 70px;
    background-color: whitesmoke;
    color: #333;
    border: none;
    border-radius: 50%;

    &.flipped {
      transform: scale(-1, -1);
    }

    &.mid {
        font-size: 60px;

      > span {
        pointer-events: none;
        background: linear-gradient(to top right, $-darkorange 40%, $-darkblue 60%);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
      }
    }

    &.active {
        position: relative;

        &:before {
          content:"";
          position:absolute;
          width: 80px;
          height: 80px;
          border-radius: 50%;
          border: 5px solid transparent;
          mask: linear-gradient(#fff 0 0) exclude;
          -webkit-mask:
              linear-gradient(#fff 0 0) padding-box, 
              linear-gradient(#fff 0 0);
          -webkit-mask-composite: xor;
          mask-composite: exclude;
          pointer-events: none;
        }

        &.previous:before {
          filter: grayscale(50);
        }

        &.mid:before {
          background: linear-gradient(105deg, $-blue 40%, $-lightorange 60%) border-box;
        }

        &.red:before {
          background: $-blue border-box;
        }

        &.blue:before {
          background: $-lightorange border-box;
        }
      }
  }

  .line {
    background-color: whitesmoke;
    height: 15px;
    width: 300%;
    z-index: -1;

    &.vertical {
      height: 300%;
      width: 15px;
    }
  }

  .empty {
    height: 100%;
    width: 100%;

    &.row-one {
      grid-row:  1 / 1;
      grid-column: 1 / 13;
    }

    &.row-two {
      grid-row: 2 / 2;
      grid-column: 1 / 21;
    }

    &.row-four {
      grid-row: 4 / 4;
      grid-column: 2 / 22;
    }
  }
</style>

<script lang="ts">
import { onMount } from "svelte";

let active: Element;
let previous: Element;

onMount(() => {
  document.querySelectorAll('main > section .active').forEach((element) => {
    if (element.classList.contains('mid')) {
      element.classList.remove('previous');
      active = element;
    } else {
      element.classList.remove('active');
    }
  });
});

const activate = ({ target }: Event) => {
  if (target === active) return;

  if (previous) {
    previous.classList.remove('previous');
    previous.classList.remove('active');
  }

  previous = active;
  previous.classList.add('previous');
  
  active = target as Element;
  active.classList.add('active');
};

</script>

<main>
  <div class="background redish"></div>
  <div class="background blueish"></div>
  <section>
    <span class="empty row-one"></span>
    <button class="circle blue flipped" on:click={activate}>10</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>9</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>8</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>7</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>6</button>
    <span class="empty row-two"></span>
    <span class="line vertical"></span>
    <button class="circle red" on:click={activate}>5</button>
    <span class="line"></span>
    <button class="circle red" on:click={activate}>4</button>
    <span class="line"></span>
    <button class="circle red" on:click={activate}>3</button>
    <span class="line"></span>
    <button class="circle red" on:click={activate}>2</button>
    <span class="line"></span>
    <button class="circle red active" on:click={activate}>1</button>
    <span class="line"></span>
    <button class="circle mid active previous" on:click={activate}><span>0</span></button>
    <span class="line"></span>
    <button class="circle blue flipped active" on:click={activate}>1</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>2</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>3</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>4</button>
    <span class="line"></span>
    <button class="circle blue flipped" on:click={activate}>5</button>
    <span class="line vertical"></span>
    <span class="empty row-four"></span>
    <button class="circle red" on:click={activate}>6</button>
    <span class="line"></span>
    <button class="circle red" on:click={activate}>7</button>
    <span class="line"></span>
    <button class="circle red" on:click={activate}>8</button>
    <span class="line"></span>
    <button class="circle red" on:click={activate}>9</button>
    <span class="line"></span>
    <button class="circle red" on:click={activate}>10</button>
  </section>
</main>

