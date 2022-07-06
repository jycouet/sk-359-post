<script context="module" lang="ts">
  import type { LoadEvent } from "@sveltejs/kit";

  export async function load(event: LoadEvent) {
    // Working well
    const resultGET = await event.fetch("http://localhost:3000/api", {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
      },
    });
    const jsonGET = await resultGET.json();
    console.log(`jsonGET`, jsonGET);

    // Not working from version 359 👇
    // Error message: "Request with GET/HEAD method cannot have body."
    const resultPOST = await event.fetch("http://localhost:3000/api", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        hello: "World",
      }),
    });
    const jsonPOST = await resultPOST.json();
    console.log(`jsonPOST`, jsonPOST);

    return { props: {} };
  }
</script>

<h1>Welcome to SvelteKit</h1>
<p>
  Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation
</p>
