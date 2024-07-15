<script lang="ts">
    import "fluent-svelte/theme.css";
</script>

<h2>Hi!</h2>

<ul>
    <li><a href="/names">Name picker</a></li>
    <li><a href="/progress">Progressbar in the browser</a></li>
</ul>

<style lang="scss">
    :global(body) {
        padding: 2em;
    }
    ul {
        padding: 0;
        li {
            list-style-type: none;
        }
    }
</style>