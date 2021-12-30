<template>
  <!-- instructions -->
  <div class="instructions">
    <h2>Instructions</h2>
    <ol>
      <li>Smash the reactionary as soon as you see him.</li>
      <li>Difficulty increases as you advance, so gear up.</li>
    </ol>
  </div>
</template>

<script>
export default {

}
</script>

<style>
/* instructions styles */
.instructions {
  perspective: 40px;
  transform-origin: 50% 20%;
  opacity: 1;
  transition: 0.1s ease-in 0.2s;
  transition-property: opacity, transform;
}
.instructions h2 {
  text-decoration: underline;
  font-size: 28px;
  margin: 20px 0;
}
.instructions ol{
  list-style-type: decimal;
  text-align: left;
  list-style-position: inside;
  display: inline-block;
}
.instructions.hide {
  opacity: 0;
  transform: translateY(-20px) rotateX(32deg);
}

</style>