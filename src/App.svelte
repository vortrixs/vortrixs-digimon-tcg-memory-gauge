<style lang="scss">
  @use 'assets/colors';

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
      background: linear-gradient(to bottom right, colors.$red 10%, colors.$darkorange 30%, colors.$lightorange 60%, colors.$yellow 80%) no-repeat border-box;
    }

    &.blueish {
      top: 0;
      right: 0;
      background: linear-gradient(to bottom right, colors.$lightblue 20%, colors.$blue 40%, colors.$darkblue 70%, colors.$deepblue 90%) no-repeat border-box;
      clip-path: polygon(30% 0%, 100% 0%, 100% 100%, 11% 100%);
    }
  }

  section {
    display: grid;
    grid-template-rows: 70px 40px 70px 40px 70px;
    align-items: center;
    justify-items: center;
    width: 95%;
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
import MemoryButton from "./lib/MemoryButton.svelte";
</script>

<main>
  <div class="background redish"></div>
  <div class="background blueish"></div>
  <section>
    <span class="empty row-one"></span>
    <MemoryButton styles="circle blue flipped">10</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">9</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">8</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">7</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">6</MemoryButton>
    <span class="empty row-two"></span>
    <span class="line vertical"></span>
    <MemoryButton styles="circle red">5</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">4</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">3</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">2</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">1</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle mid active"><span>0</span></MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">1</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">2</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">3</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">4</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle blue flipped">5</MemoryButton>
    <span class="line vertical"></span>
    <span class="empty row-four"></span>
    <MemoryButton styles="circle red">6</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">7</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">8</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">9</MemoryButton>
    <span class="line"></span>
    <MemoryButton styles="circle red">10</MemoryButton>
  </section>
</main>

