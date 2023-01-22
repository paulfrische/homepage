<script lang="ts">
    import "./terminal.sass";
    import { onMount } from "svelte";

    let input: HTMLInputElement;
    let output: HTMLParagraphElement;


    onMount(async () => {
        input = document.getElementById("cmd") as HTMLInputElement;
        output = document.getElementById("output") as HTMLParagraphElement;
        console.log(input);
    });

    function handleCommand(command: string) {
        let result: string;
        switch (command) {
            case "clear":
                output.innerText = "";
                result = "";
                break;
            default:
                result = `Error: command '${command}' not found`;
        }
        output.innerText += `${result}\n`;
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
    <p id="output" />
    <form id="prompt" on:submit={enterCommandListener}>
        <span class="purple">paul@archlinux</span>
        <span class="blue">~</span>
        <span class="white">$</span>
        <input type="text" id="cmd" />
    </form>
</div>
