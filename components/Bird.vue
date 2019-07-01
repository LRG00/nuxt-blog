<template>
  <div class="bird">
    
  </div>
</template>
<style>
.bird {
    width: 100px; height: 58px;
    background: url('../assets/piece-bird.png') no-repeat;
    background-size: contain;
    /* 动画 */
    animation: pulse 5s linear infinite;
}
@keyframes pulse {
    from {
        filter: hue-rotate(0);
    }
    to {
        filter: hue-rotate(360deg);
    }
}

</style>