<template>
    <div class="about container">
      <h2>About</h2>
      <aticle>
        Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。
      </aticle>
      <div id="image"></div>
    </div>
</template>

<script>
    export default {
        name: 'about',
        data() {
            return {}
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
article{
  font-style: italic;
}
  #image{
    background: url("../assets/logo.png");
    width: 400px;
    height: 400px;
    margin: 0 auto;
  }
</style>
