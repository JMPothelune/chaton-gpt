<script lang="ts">
  import { fly } from 'svelte/transition';




  const ITEMS = [
      " miaou",
      " miaou",
      " miaou",
      " miaou",
      " miaou",
      " miaou",
      " miaou",
      " miaou",
      " miaou",
      " meow",
      " meow",
      " meow",
      " mia",
      " mia",
      " mia",
      " meow",
      ", miaou",
      ". Miaou",
      ".<br/> Miaou",
      "? Miaou",
    ]

    let messages = [] as any

  let message:string = "";

  function generateResponse(){

    let response = "Miaou"

    let wordCount = Math.floor(Math.random() * 100) + 20
    for (let i = 0; i < wordCount; i++) {
      response += ITEMS[Math.floor(Math.random() * ITEMS.length)]
    }

    response += "."
    
    return response
  }



  function simulateChaton(){

    let response = generateResponse()

    let responseItem = { text: "...", author: "Chaton" }
    setTimeout(() => {
      messages = [...messages, responseItem ];

      let end = 0;
      let token = setInterval(() => {
        if (end < response.length) {
          end += Math.floor(Math.random() * 10) + 1;
          responseItem.text = response.substring(0, end)
          messages = messages
        }
        else {
          clearInterval(token)
        }
      }, 150);
    }, 1000);


  }





  function addMessage(){
    messages = [...messages, { text: message, author: "user" }];
    message = "";

    simulateChaton();
  };
</script>



<main class=" flex flex-col mx-auto items-stretch text-center text-gray-200 min-h-screen ">
  <h1 class="text-4xl my-5">🐱 Chaton GPT</h1>

  <div class="flex flex-col items-stretch ">
    {#each messages as { text, author }}
      <div class="flex flex-row items-center border-b border-gray-500 py-5"
        transition:fly={{y: 20, duration: 300}}
        class:bg-gray-600={author === "Chaton"}
      >
        <div class="container flex flex-row items-start space-x-4 mx-auto px-4">
          {#if author === "Chaton"}
            <img src="https://placekitten.com/50/50" class="w-10 h-10 rounded-full" alt={author}/>
          {:else}
            <img src="https://placekitten.com/50/50?rand=2" class="w-10 h-10 rounded-full" alt={author}/>
          {/if}
          <div class="text-left">{@html text}</div>
        </div>
      </div>
    {:else}

    <div class="flex flex-row items-center justify-center text-center  py-6 opacity-50">
        Pour commencer une conversation, posez une question à Chaton GPT.
    </div>
    {/each}
  </div>


</main>


<footer class="flex flex-col items-center justify-center text-gray-200 sticky bottom-0 w-full py-4 bg-gray-700 ">

  <form 
    class="container flex items-center justify-center"
    on:submit|preventDefault={addMessage}
    >

    <input 
      class="w-full bg-gray-600 border-gray-200  p-4 mx-2 shadow-xl rounded"
      placeholder="Votre question..."
      type="text" bind:value={message} />
    <button type="submit">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
        <path d="M3.478 2.405a.75.75 0 00-.926.94l2.432 7.905H13.5a.75.75 0 010 1.5H4.984l-2.432 7.905a.75.75 0 00.926.94 60.519 60.519 0 0018.445-8.986.75.75 0 000-1.218A60.517 60.517 0 003.478 2.405z" />
      </svg>
    </button>

  </form>

  <div class="container mx-auto flex items-center justify-center opacity-50 space-x-4">
    
    <a href="https://github.com/JMPothelune/chaton-gpt" class="flex flex-row items-center">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" fill="currentColor" class="w-4 h-4 mx-2">
        <path fill-rule="evenodd" clip-rule="evenodd" d="M48.854 0C21.839 0 0 22 0 49.217c0 21.756 13.993 40.172 33.405 46.69 2.427.49 3.316-1.059 3.316-2.362 0-1.141-.08-5.052-.08-9.127-13.59 2.934-16.42-5.867-16.42-5.867-2.184-5.704-5.42-7.17-5.42-7.17-4.448-3.015.324-3.015.324-3.015 4.934.326 7.523 5.052 7.523 5.052 4.367 7.496 11.404 5.378 14.235 4.074.404-3.178 1.699-5.378 3.074-6.6-10.839-1.141-22.243-5.378-22.243-24.283 0-5.378 1.94-9.778 5.014-13.2-.485-1.222-2.184-6.275.486-13.038 0 0 4.125-1.304 13.426 5.052a46.97 46.97 0 0 1 12.214-1.63c4.125 0 8.33.571 12.213 1.63 9.302-6.356 13.427-5.052 13.427-5.052 2.67 6.763.97 11.816.485 13.038 3.155 3.422 5.015 7.822 5.015 13.2 0 18.905-11.404 23.06-22.324 24.283 1.78 1.548 3.316 4.481 3.316 9.126 0 6.6-.08 11.897-.08 13.526 0 1.304.89 2.853 3.316 2.364 19.412-6.52 33.405-24.935 33.405-46.691C97.707 22 75.788 0 48.854 0z"/>
      </svg>
      Sources
    </a>
  </div>

</footer>