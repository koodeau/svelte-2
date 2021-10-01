<script>
  let password = ""
  $: id = 0
  let passwords = []
  let error = null

  function addPassword() {
    if (password.trim().length == 0) {
      error = "empty"
    } else if (password.trim().length > 0 && password.trim().length < 5) {
      error = "short"
    } else if (password.trim().length > 10) {
      error = "long"
    } else if (password.trim().length >= 5 && password.trim().length <= 10) {
	  id ++
	  error = null
      passwords = [
        ...passwords,
        {
		  id: id,
          value: password,
        },
      ]
	}else {
      error = "other"
    }
  }

  function remove() {
	  passwords = passwords.slice(id - id + 1)
  }
</script>

<h1>Input your password</h1>
<input type="password" bind:value={password} />
<p>Must be between 5 to 10 symbols</p>
<button on:click={addPassword}>Save</button>

<h2>Saved passwords</h2>

{#if error == null}
  <br />
{:else if error == "empty"}
  <strong>Password cannot be {error}</strong>
{:else if error == "short"}
  <strong>Too {error}</strong>
{:else if error == "long"}
  <strong>Too {error}</strong>
{:else if error == "other"}
  <strong>Some error occured</strong>
{/if}

<ul>
  {#each passwords as show}
    <li>
      <a 
	  on:click={remove}
	  >
	  {show.value} {show.id}
	</a>
    </li>
  {/each}
</ul>
