<template>
    <h1 data-title="POSTSAPP" class="text">
        POSTSAPP
    </h1>
</template>

<style scoped>
  .text{
    color: transparent;
    font-size: 3vw;
    margin-top: 10px;
    display: inline-block;
    border-radius: 3px;
    background-color: #1d3557;
    position: relative;
    -webkit-background-clip: text;
    background-clip: text;
    &:before{
      content: attr(data-title);
      background: linear-gradient(90deg, rgb(3, 159, 13) 0%, rgb(238, 176, 94) 51%, rgb(31, 61, 103) 100%);
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      width: 0;
      background-clip: text;
      -webkit-background-clip: text;
      transition: all 1s ease-in-out;
      animation: text-animation 3s infinite;
    }
  }


@keyframes text-animation{
  0%{
    width: 0;
  }
  50%{
    width: 100%;
  }
  100%{
    width: 0;
  }
}

</style>