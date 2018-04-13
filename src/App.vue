<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Built-In Directives</h1>
                <p v-text="'From Directive'"></p>
                <p v-html="'<strong>From Directive</strong>'"></p>
            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Custom Directives</h1>
                <p v-highlight:background.delayed="'red'">Color This</p>
                <p v-local-highlight:background.delayed.blink="{mainColor: 'red', secondColor: 'green', delay: 500}">Color This, too</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  directives: {
    "local-highlight": {
      bind(el, binding, vnode) {
        var delay = 0;
        if (binding.modifiers["delayed"]) {
          delay = 3000;
        }

        let val = binding.value;

        if (binding.modifiers["blink"]) {
          let mainColor = val.mainColor;
          let secondColor = val.secondColor;
          let currentColor = mainColor;
          setTimeout(() => {
            setInterval(() => {
              currentColor =
                currentColor == mainColor ? secondColor : mainColor;
              if (binding.arg == "background") {
                el.style.backgroundColor = currentColor;
              } else {
                el.style.color = currentColor;
              }
            }, val.delay);
          }, delay);
        } else {
          setTimeout(() => {
            if (binding.arg == "background") {
              el.style.backgroundColor = val.mainColor;
            } else {
              el.style.color = val.mainColor;
            }
          }, delay);
        }
      }
    }
  }
};
</script>

<style>

</style>
