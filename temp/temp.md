The Blueprint for Later (Save This!)

When you are ready to start vibe-coding or properly learning Go with this project, here is the architectural plan you can look back on:

1. **The Core Loop**: Instead of spawing heavy shell commands (`bash -c "while true..."`) which spawn hundreds of tiny sub-processes every second, your Go app will natively open and read files like `/proc/stat` (for CPU) and `/proc/meminfo` (for RAM) directly into memory. This will drop your status bar's CPU usage to basically 0%.
2. **The Output**: Your Go app will continuously calculate these stats and print them to standard output (`fmt.Println()`) as a single, clean string (e.g., `cpu|mem|swap|disk|net`).
3. **The Quickshell Bridge**: Your Quickshell config will use its `Process` component to run `goqsproch`. It will sit and listen to that standard output, splitting the string up to update your UI instantly.

It is lean, it keeps your system fast, and it is an amazing first project for learning how Go interacts with the Linux kernel!

When you are ready to kick off the project or start setting up the initial Go file structure, how would you like to handle the communication—should we stick to **printing clean strings to standard output**, or do you want to eventually explore **JSON formatting** for easier expanding later?