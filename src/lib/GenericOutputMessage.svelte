<script lang="ts">
    import type { SvelteComponent } from "svelte";

export let message: string | SvelteComponent;
export let command: string;

import CommandLine from "./CommandLine.svelte";
</script>

<div><div class="input"><CommandLine /> {command}</div>{message}</div>

<style lang="sass">
div
    white-space: pre-wrap
    .input
        display: flex
        gap: 1rem
</style>
