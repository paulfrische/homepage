<script lang="ts">
import CommandLine from "./CommandLine.svelte";
</script>

<div><div class="input"><CommandLine /> whoami</div>
<p>I am Paul Frische and I am interested in everything related to linux or software development
You can find me on <a href="https://github.com/paulfrische">Github</a></p>
</div>

<style lang="sass">
div
    white-space: pre-wrap
    .input
        display: flex
        gap: 1rem
</style>
