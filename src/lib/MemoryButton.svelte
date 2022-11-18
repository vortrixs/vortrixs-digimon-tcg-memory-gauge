<style lang="scss">
  @use '../assets/colors';
  
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

      > :global(span) {
        pointer-events: none;
        background: linear-gradient(to top right, colors.$darkorange 40%, colors.$darkblue 60%);
        background-clip: text;
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
          background: linear-gradient(105deg, colors.$blue 40%, colors.$lightorange 60%) border-box;
        }

        &.red:before {
          background: colors.$blue border-box;
        }

        &.blue:before {
          background: colors.$lightorange border-box;
        }
      }
  }
</style>

<script context="module">
    let current;
    let previous;
</script>

<script lang="ts">
    import { onMount } from "svelte";

    export let styles: string;

    let button;

    onMount(() => {
        if (styles.includes('active')) current = button;

        if ($$slots.mid) $$slots.mid
    });

    const activate = () => {
        if (button === current) return;

        if (previous) {
            previous.classList.remove('previous');
            previous.classList.remove('active');
        }

        previous = current;
        previous.classList.add('previous');
        
        current = button;
        current.classList.add('active');
    };

    
</script>

<button class={styles} bind:this={button} on:click={activate}>
    <slot></slot>
</button>