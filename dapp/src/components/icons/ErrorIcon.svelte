<script lang="ts">
  let clazz: string = '';
  export { clazz as class };
  export let color: string = 'red';
</script>

<svg
  enable-background="new 0 0 128 128"
  height="128px"
  id="Layer_1"
  version="1.1"
  viewBox="0 0 128 128"
  xml:space="preserve"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink"
  class={clazz}
>
  <g>
    <g>
      <path
        d="M64,0C28.656,0,0,28.656,0,64s28.656,64,64,64s64-28.656,64-64S99.344,0,64,0z M64,120    C33.125,120,8,94.875,8,64S33.125,8,64,8s56,25.125,56,56S94.875,120,64,120z"
        fill={color}
      />
    </g>
  </g>
  <g>
    <g>
      <path
        d="M75.313,64l16.969-16.969c3.125-3.125,3.125-8.195,0-11.313c-3.117-3.125-8.188-3.125-11.313,0L64,52.688    L47.031,35.719c-3.125-3.125-8.195-3.125-11.313,0c-3.125,3.117-3.125,8.188,0,11.313L52.688,64L35.719,80.969    c-3.125,3.125-3.125,8.195,0,11.313c3.117,3.125,8.188,3.125,11.313,0L64,75.313l16.969,16.969c3.125,3.125,8.195,3.125,11.313,0    c3.125-3.117,3.125-8.188,0-11.313L75.313,64z"
        fill={color}
      />
    </g>
  </g>
</svg>
