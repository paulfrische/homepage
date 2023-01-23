<script lang="ts">
import CommandLine from "./CommandLine.svelte";
</script>

<div>
<div class="input"><CommandLine /> software</div>
<ul>
<li><a href="https://archlinux.org">I use Arch btw</a></li>
<li><a href="https://github.com/baskerville/bspwm">BSPWM</a></li>
<li><a href="https://github.com/alacritty/alacritty">Alacritty</a></li>
<li><a href="https://neovim.io">NeoVim</a></li>
</ul>
</div>

<style lang="sass">
div
    white-space: pre-wrap
    li
        margin-left: 1rem
        list-style: circle
    .input
        display: flex
</style>
