<style lang="scss">
  @use 'assets/colors';

  main {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    font-size: 30px;

    section {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: center;

      &.portrait-detected {
        flex-flow: column;
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: #333;
        z-index: 10;
        text-align: center;

        visibility: visible;
        opacity: 1;
        transition: opacity .5s linear;

        &.hidden {
          visibility: hidden;
          opacity: 0;
          transition: visibility .5s, opacity .5s linear;
        }
      }
    }
  }

  .background {
      position: absolute;
      width: 63%;
      height: 100%;
      z-index: -2;
  
      &.redish {
        top: 0;
        left: 0;
        background: linear-gradient(to bottom right, colors.$red 10%, colors.$darkorange 30%, colors.$lightorange 60%, colors.$yellow 80%) no-repeat border-box;
      }
  
      &.blueish {
        top: 0;
        right: 0;
        background: linear-gradient(to bottom right, colors.$lightblue 20%, colors.$blue 40%, colors.$darkblue 70%, colors.$deepblue 90%) no-repeat border-box;
        clip-path: polygon(30% 0%, 100% 0%, 100% 100%, 11% 100%);
      }
    }
</style>

<script lang="ts">
import Gauge from "./lib/Gauge.svelte";

let orientation: string = screen.orientation.type;

screen.orientation.onchange = (e) => {
  orientation = screen.orientation.type;
};
</script>

<main>
  <section
    class="portrait-detected"
    class:hidden={!orientation.includes('portrait')}
  >
    <p>Portrait mode detected.</p>
    <p>Please put your device in landscape mode.</p>
  </section>

  <section>
    <div class="background redish"></div>
    <div class="background blueish"></div>
    <Gauge />
  </section>
</main>

