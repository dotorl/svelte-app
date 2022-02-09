<script>
  import { storeName } from "./store.js";
  import Todo from "./Todo.svelte";

  // console.log(storeName);
  // console.log($storeName);

  // storeName.set("aaaaa");
  // console.log($storeName);

  // $storeName = "tttttt";
  // console.log($storeName);

  // storeName.update(function (value) {
  //   return value + "bbbbb";
  // });
  // console.log($storeName);

  // import { onMount } from 'svelte';
  import Component1 from "./Component1.svelte";
  import Fruits from "./Fruits.svelte";
  import Parent from "./parent.svelte";
  import { writable } from "svelte/store";

  export let name;
  name = "choks";

  // store 변수에 다른 변수 대입
  $storeName = name;

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

  let title = "";
  let todos = writable([]);
  function createTodo() {
    $todos.push({
      id: $todos.length + 1,
      title: title,
    });

    title = "";
    $todos = $todos;
  }
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

<br />
<hr />

<Component1 />

<br />
<hr />

<Fruits propsFruit="{fruits}" />

<Fruits propsFruit="{fruits}" reverse />

<Fruits propsFruit="{fruits}" slice="-2" />

<Fruits propsFruit="{fruits}" slice="0, 2" />
<!-- 
	// Props와 데이터 이름이 같다면 생각가능한데 프리티어가 자동으로 써버리네..?
	<Fruits fruits="{fruits}" /> 
	<Fruits {fruits} /> 
-->

<br />
<hr />

<Parent />
<br />
<hr />

<input
  type="text"
  bind:value="{title}"
  on:keydown="{(e) => e.key === 'Enter' && createTodo()}"
/>

<button on:click="{createTodo}">Create Todo</button>

{#each $todos as todo}
  <Todo todos="{todos}" todo="{todo}" />
{/each}
