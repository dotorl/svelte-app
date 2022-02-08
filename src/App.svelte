<script>
  // import { onMount } from 'svelte';

  export let name;
  name = "choks";

  function assign() {
    name = "asdfasfd";
  }

  let toggle = false;

  let fruits = ["apple", "banana", "orange"];

  let isRed = false;

  // onMount(() => {
  // 	console.log('mounted');
  // 	const box = document.querySelector('.box');
  // 	box.addEventListener('click' , () => { isRed = !isRed });
  // });
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  .blue {
    color: blue;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .box {
    width: 300px;
    height: 150px;
    background-color: #ff3e00;
  }
</style>

<main>
  <h1 class="{name === 'choks' ? 'blue' : ''}">Hello {name}!</h1>
  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>
</main>

<button on:click="{assign}">assign</button>

<!-- 단방향 바인딩 -->
<!-- <input type="text" value={name} on:input={e => (name = e.target.value)} /> -->

<!-- 양방향 바인딩 -->
<input type="text" bind:value="{name}" />

<br />
<hr />

<button
  on:click="{() => {
    toggle = !toggle;
  }}">toggle</button
>

{#if toggle}
  <h1>toogle = true! 보여지는 조건부 영역</h1>
{:else}
  <h1>toggle = fale!</h1>
{/if}

<br />
<hr />

<ul>
  {#each fruits as fruit}
    <li>{fruit}</li>
  {/each}
</ul>

<br />
<hr />

<div
  class="box"
  style="background-color:{isRed ? 'red' : 'blue'}"
  on:click="{() => (isRed = !isRed)}"
  on:mouseenter="{() => {
    name = 'enter';
  }}"
  on:mouseleave="{() => {
    name = 'leave';
  }}"
>
  {name}
</div>
