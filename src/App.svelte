<script>

let pass = '';
let passState = '';

let passList = [];

$: if (pass.trim().length < 5) {
        passState = 'Too short';
    } else if (pass.trim().length > 10) {
        passState = 'Too long';
    } else {
        passState = 'ok';
    }

function addPass() {
    if (passState === 'ok') {
        passList = [...passList, pass];
    }
}

function removePass(index) {
    const value = passList[index];
    passList = passList.filter(function(item) {
        return item !== value;
    });
}

</script>

<h1>Assignment</h1>
<p>Solve these tasks.</p>
<ol>
	<li>&#10003; - Add a password input field and save the user input in a variable.</li>
	<li>&#10003; - Output "Too short" if the password is shorter than 5 characters and "Too long" if it's longer than 10.</li>
	<li>&#10003; - Output the password in a paragraph tag if it's between these boundaries.</li>
	<li>&#10003; - Add a button and let the user add the passwords to an array.</li>
	<li>&#10003; - Output the array values (= passwords) in a unordered list (ul tag).</li>
	<li>&#10003; - Bonus: If a password is clicked, remove it from the list.</li>
</ol>
<hr>
<label>Password:</label>
<input type="password" bind:value={pass} id="pass"/>
<button on:click={addPass}>Add Pass</button>

{#if passState === 'Too short'}
    <p>Too short</p>
{:else if passState === 'Too long'}
    <p>Too long</p>
{:else}
    <p>Pass: {pass}</p>
{/if}

<h2>Pass List</h2>
<ul>
{#each passList as pw, i (pw)}
    <li on:click="{() => removePass(i)}">{pw}</li>
{/each}
</ul>
