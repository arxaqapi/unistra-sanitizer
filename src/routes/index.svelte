<!-- src/routes/index.svelte -->
<svelte:head>
    <title>Unistra Sanitizer</title>
</svelte:head>

<script>
    import { goto } from '$app/navigation';

    let calendar_link = ''

</script>

<h1>Bienvenue sur Unistra Sanitizer !</h1>

<div class="calendar-link">
    <input type="text" bind:value={calendar_link}>
    <button on:click={goto(`/calendar/${calendar_link.split('/')[5]}`)} >Afficher le calendrier</button>
</div>

<br>
<hr>
<footer>
    Ce projet est largement inspiré par <a href="https://git.pa1ch.fr/alban/celcatsanitizer.git/" target="_blank" referrerpolicy="no-referrer">calcat-sanitizer</a> réalisé par <a href="https://pa1ch.fr/" target="_blank" referrerpolicy="no-referrer">Alban Gruin</a>
</footer>

<style>
    input {
        border: 1px solid black;
        padding: 10px;
    }
    button {
        display: block;
    }
</style>