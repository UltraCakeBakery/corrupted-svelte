<div class="outer">
  <slot></slot>
  <div class="inner">
    <slot></slot>
  </div>
  <div class="inner">
    <slot></slot>
  </div>
</div>


<style>
  .outer {
    position: relative;
  }

  .inner {
    position: absolute;
    top: 0px;
    left: 0px;
    animation: filter 1s;
    filter: sepia(100%) hue-rotate(90deg) saturate(400%);
  }

</style>