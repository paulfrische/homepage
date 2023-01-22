<script lang="ts">
    import "./terminal.sass";
    import { onMount } from "svelte";
    import OutputMessage from "./OutputMessage.svelte";
    import CommandLine from "./CommandLine.svelte";

    let input: HTMLInputElement;
    let output: HTMLParagraphElement;

    let outputs: Array<[string, string]> = [];

    const help =
        "Type one of the following commands and press <Enter>:\n help    - show this message\n clear   - clears the screen\n whoami  - shows information about me\n";

    onMount(async () => {
        input = document.getElementById("cmd") as HTMLInputElement;
        input.focus()
        output = document.getElementById("output") as HTMLParagraphElement;
        output.innerText = help
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
                outputs.push(["whoami", "I am paul!"]);
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
            <OutputMessage message={out[1]} command={out[0]} />
        {/each}
    </div>
    <form id="prompt" on:submit={enterCommandListener}>
        <CommandLine />
        <input type="text" id="cmd" />
    </form>
</div>
