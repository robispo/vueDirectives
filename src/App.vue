<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Build-in Directives</h1>

        <p v-text="'text directive'"></p>
        <p v-html="'<strong>html directive</strong>'"></p>
      </div>
    </div>
    <hr />
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Custom Directives</h1>
        <p v-highlight="'red'">highlight directive</p>
        <p v-highlight:background="'red'">highlight directive</p>
        <p v-highlight.delayed="'blue'">highlight directive</p>
        <p v-highlight:background.delayed="'blue'">highlight directive</p>
        <p
          v-local-highlight:background.delayed.blink="{
            mainColor: 'red',
            secondColor: 'blue',
            delay: 300
          }"
        >
          local-highlight directive
        </p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    directives: {
      'local-highlight': {
        bind(el, binding, vnode) {
          let { mainColor, secondColor, delay } = binding.value;

          if (binding.modifiers['blink']) {
            let currentColor = secondColor;

            setTimeout(() => {
              setInterval(() => {
                currentColor =
                  currentColor == mainColor ? secondColor : mainColor;

                if (binding.arg == 'background') {
                  el.style.backgroundColor = currentColor;
                } else {
                  el.style.color = currentColor;
                }
              }, 1000);
            }, delay);
          } else {
            setTimeout(() => {
              if (binding.arg == 'background') {
                el.style.backgroundColor = mainColor || binding.value;
              } else {
                el.style.color = mainColor || binding.value;
              }
            }, delay);
          }
        }
      }
    }
  };
</script>

<style></style>
