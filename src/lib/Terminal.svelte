<script lang="ts">
    import "./terminal.sass";
    import { onMount, SvelteComponent } from "svelte";
    import GenericOutputMessage from "./GenericOutputMessage.svelte";
    import CommandLine from "./CommandLine.svelte";
    import About from "./About.svelte";

    let input: HTMLInputElement;
    let output: HTMLParagraphElement;

    let outputs: Array<[string, string | SvelteComponent]> = [];

    const help = `Type one of the following commands and press <Enter>:
         help    - show this message
         clear   - clears the screen
         whoami  - shows information about me
         
         `;

    onMount(async () => {
        input = document.getElementById("cmd") as HTMLInputElement;
        input.focus();
        output = document.getElementById("output") as HTMLParagraphElement;
        output.innerText = help;
    });

    function handleCommand(command: string) {
        switch (command) {
            case "clear":
                output.innerText = "";
                break;
            case "help":
                outputs.push(["help", help]);
                break;
            case "whoami":
                outputs.push(["whoami", ""]);
                break;
            default:
                outputs.push([
                    command,
                    `Error: command '${command}' not found`,
                ]);
        }

        // to rerender the data
        outputs = outputs;
    }

    function enterCommandListener(event: SubmitEvent) {
        event.preventDefault();
        input.focus();
        const command = input.value;
        handleCommand(command);
        input.value = "";
    }
</script>

<div class="terminal">
    <div id="output">
        {#each outputs as out}
            {#if out[0] == "whoami"}
                <About />
            {/if}
            {#if out[0] != "whoami"}
                <GenericOutputMessage message={out[1]} command={out[0]} />
            {/if}
        {/each}
    </div>
    <form id="prompt" on:submit={enterCommandListener}>
        <CommandLine />
        <input type="text" id="cmd" />
    </form>
</div>
