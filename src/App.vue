<template>
  <div class="min-h-screen flex flex-col">
    <!-- Header with pink background -->
    <header class="bg-blue-600 text-white py-16 px-6 text-center">
      <h1 class="text-5xl font-bold mb-2">Table.One Widget</h1>
      <p class="text-xl">This widget is in test production.</p>
    </header>
    
    <!-- Dark section with embed code -->
    <main class="flex-grow bg-gray-900 text-white py-12 px-6">
      <div class="max-w-3xl mx-auto">
        <h2 class="text-4xl font-bold mb-8">Embed code</h2>
        
        <p class="mb-6 text-gray-300">Paste this code inside the <span class="text-white font-mono">&lt;body&gt;</span> tag of your website.</p>
        
        <div class="bg-gray-800 rounded-md overflow-hidden relative">
            <span>
            &lt;script&gt;
            document.addEventListener("DOMContentLoaded", function () {
              (function (document, script, scriptId) {
                const firstScript = document.getElementsByTagName(script)[0];
                if (document.getElementById(scriptId)) return;

                const scriptElement = document.createElement(script);
                scriptElement.src = "https://itsdimitrie.github.io/table.one-widget-test/embed.js";
                // scriptElement.src = "http://localhost:5173/table.one-widget-test/embed.js";

                firstScript.parentNode?.insertBefore(scriptElement, firstScript);
              })(document, "script", "reservationWidgetScript");
            });
            &lt;/script&gt;
            &lt;div class="widget-data" restoId="Bistro Van Dimi" color="red"&gt;&lt;/div&gt;
            </span>
        </div>  
          <button 
            @click="copyCode" 
            class="flex ml-auto mr-auto mt-20  bg-blue-600 hover:bg-blue-200 text-white p-20 py-10 text-xl font-medium rounded"
          >
            {{ copyButtonText }}
          </button>
      </div>
      
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'App',
  setup() {
    const copyButtonText = ref('COPY');
    const codeSnippet = ''
  

    const copyCode = () => {
      navigator.clipboard.writeText(codeSnippet);
      copyButtonText.value = 'COPIED!';
      setTimeout(() => {
        copyButtonText.value = 'COPY';
      }, 2000);
    };

    return {
      copyButtonText,
      copyCode
    };
  }
});
</script>