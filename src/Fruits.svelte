<script>
  export let propsFruit;
  export let reverse;
  export let slice;

  let computedFruits = [];
  if (reverse) {
    computedFruits = [...propsFruit.reverse()];
  } else if (slice) {
    // slice => '-2', '0, 3'
    // slice.split(',') => ['-2'], ['0', ' 3'];
    // ['-2'] => '-2';
    // ['0' , ' 3'] => '0', ' 3';

    computedFruits = propsFruit.slice(...slice.split(","));
  } else {
    computedFruits = propsFruit;
  }
</script>

<h2>Fruit Component</h2>

<p>App -> 변수 내려받아서 사용하기 :: props</p>
<ul>
  {#each computedFruits as fruit}
    <li>{fruit}</li>
  {/each}
</ul>
