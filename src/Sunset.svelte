<script>
  export let props, isVisible;
  let { img, text, textColor, bgColor, bgImage, screenTime } = props;

  // Defaults if not in props
  if (!img) img = 'bart_yellow.png';
  if (!text) text = 'This page intentionally sunsetting.';
  if (!textColor) textColor = '#000';
  if (!bgColor) bgColor = '#fff';

  $: if (isVisible && bgColor)  {
    document.body.style.backgroundColor = bgColor;
  }

  let screenTimeS = 0;
  $: screenTimeS = (screenTime / 1000).toFixed(3) + 's';

  let display = 'none';
  $: display = isVisible ? 'block' : 'none';
</script>

<div style="display: {display}">
  {#if img}<img src={img} alt="Bartley Gillan">{/if}
  {#if text}<h2 class="text-color" style="--text-color: {textColor}">{text}</h2>{/if}
  {#if bgImage}<div class="tiled-image" style="--bgImage: url({bgImage})"/>{/if}
  <div class="sunset-gradient"/>
  <div class="sun move-down" style="--screenTimeS: {screenTimeS}"/>
</div>

<style>
  img {
    max-width: 35%;
  }
  .text-color {
    color: var(--text-color);
  }
  .tiled-image {
    position: fixed;
    top: 0;
		left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    background-image: var(--bgImage);
    background-repeat: repeat;
    background-position: center center;
  }
  .sunset-gradient {
    position: fixed;
    top: 0;
		left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    background: linear-gradient(180deg, rgba(71,129,236,1) 0%, rgba(224,106,157,1) 70%, rgba(255,199,73,1) 100%);
  }
  .sun {
    position: fixed;
    left: 0;
    width: 100%;
    height: calc(100vw);
    background: #ffef49;
    border-radius: 50%;
    z-index: -1;
  }
  .move-down {
    animation: movedown var(--screenTimeS) infinite;
  }
  @keyframes movedown {
    0% {
      top: calc(80vh);
    }
    100% {
      top: calc(100vh);
    }
  }

</style>
