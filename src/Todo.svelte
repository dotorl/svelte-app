<script>
  export let todo;
  export let todos;

  let isEdit = false;
  let title = "";

  function onEdit() {
    isEdit = true;
    title = todo.title;
  }

  function offEdit() {
    isEdit = false;
  }

  function deleteTodo() {
    // 이런식으로 App에서 내려준 todos는 변경할수 없으므로 Store로 바꿔야하므로 $ 붙여줌
    $todos = $todos.filter((t) => t.id !== todo.id);
    console.log($todos);
  }

  function onSave() {
    isEdit = false;
    todo.title = title;
    offEdit();
  }
</script>

{#if isEdit}
  <div>
    <input
      type="text"
      bind:value="{title}"
      on:keydown="{(e) => e.key === 'Enter' && onSave()}"
    />
    <button on:click="{onSave}">Save</button>
    <button on:click="{offEdit}">Cancel</button>
  </div>
{:else}
  <div>
    {todo.title}
    <button on:click="{onEdit}">Edit</button>
    <button on:click="{deleteTodo}">Delete</button>
  </div>
{/if}
