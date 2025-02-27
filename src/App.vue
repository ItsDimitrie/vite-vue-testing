<template>
  <div class="min-h-screen flex flex-col">
    <!-- Header with blue background -->
    <header class="bg-blue-600 text-white py-16 px-6 text-center">
      <h1 class="text-5xl font-bold mb-2">Table.One Widget</h1>
      <p class="text-xl">This widget is in test production.</p>
    </header>
    
    <!-- Dark section with embed code -->
    <main class="flex-grow bg-gray-900 text-white py-12 px-6">
      <div class="max-w-3xl mx-auto">
        <h2 class="text-4xl font-bold mb-8">Embed code</h2>
        
        <p class="mb-6 text-gray-300">Paste this code inside the <span class="text-white font-mono">&lt;body&gt;</span> tag of your website.</p>
        
        <!-- Editable fields -->
        <div class="mb-8 grid grid-cols-1 md:grid-cols-2 gap-6">
          <div>
            <label class="block text-gray-300 mb-2" for="restoIdInput">Restaurant ID:</label>
            <input 
              id="restoIdInput" 
              v-model="restoId" 
              class="w-full bg-gray-800 border border-gray-700 rounded px-4 py-2 text-white"
              placeholder="Enter restaurant ID"
            />
          </div>
          <div>
            <label class="block text-gray-300 mb-2" for="colorSelect">Color:</label>
            <select 
              id="colorSelect" 
              v-model="color" 
              class="w-full bg-gray-800 border border-gray-700 rounded px-4 py-2 text-white"
            >
              <option value="blue">Blue</option>
              <option value="green">Green</option>
              <option value="red">Red</option>
              <option value="orange">Orange</option>
            </select>
          </div>
        </div>
        
        <p class="text-gray-300 mb-6">
          You can edit the 
          <span class="text-white font-mono">&lt;restoId&gt;</span> and change the color to either blue, green, red or orange in
          <span class="text-white font-mono">&lt;color&gt;</span>
        </p>
        <p class="text-gray-300">Note that this only changes on your own application where you import the code, not on this page.</p>
        
        <div class="bg-gray-800 rounded-md overflow-hidden relative">
          <pre class="p-4 overflow-x-auto text-sm text-gray-300">
<span class="text-gray-500">1.</span> <span class="text-blue-400">&lt;script&gt;</span>
<span class="text-gray-500">2.</span>     document.addEventListener<span class="text-white">(</span><span class="text-green-400">"DOMContentLoaded"</span><span class="text-white">, </span><span class="text-yellow-400">function</span><span class="text-white"> () {</span>
<span class="text-gray-500">3.</span>         <span class="text-white">(</span><span class="text-yellow-400">function</span><span class="text-white"> (document, script, scriptId) {</span>
<span class="text-gray-500">4.</span>             <span class="text-purple-400">const</span> firstScript = document.getElementsByTagName<span class="text-white">(script)[</span><span class="text-red-400">0</span><span class="text-white">];</span>
<span class="text-gray-500">5.</span>             <span class="text-purple-400">if</span><span class="text-white"> (document.getElementById(scriptId)) </span><span class="text-purple-400">return</span><span class="text-white">;</span>
<span class="text-gray-500">6.</span> 
<span class="text-gray-500">7.</span>             <span class="text-purple-400">const</span> scriptElement = document.createElement<span class="text-white">(script);</span>
<span class="text-gray-500">8.</span>             scriptElement.src = <span class="text-green-400">"https://itsdimitrie.github.io/table.one-widget-test/embed.js"</span><span class="text-white">;</span>
<span class="text-gray-500">9.</span>             <span class="text-gray-500">// scriptElement.src = "http://localhost:5173/table.one-widget-test/embed.js";</span>
<span class="text-gray-500">10.</span> 
<span class="text-gray-500">11.</span>            firstScript.parentNode?.insertBefore<span class="text-white">(scriptElement, firstScript);</span>
<span class="text-gray-500">12.</span>        <span class="text-white">})(document, </span><span class="text-green-400">"script"</span><span class="text-white">, </span><span class="text-green-400">"reservationWidgetScript"</span><span class="text-white">);</span>
<span class="text-gray-500">13.</span>    <span class="text-white">});</span>
<span class="text-gray-500">14.</span> <span class="text-blue-400">&lt;/script&gt;</span>
<span class="text-gray-500">15.</span> <span class="text-blue-400">&lt;div</span> class=<span class="text-green-400">"widget-data"</span> restoId=<span class="text-green-400">"{{ restoId }}"</span> color=<span class="text-green-400">"{{ color }}"</span><span class="text-blue-400">&gt;&lt;/div&gt;</span></pre>
        </div>
        
        <button 
          @click="copyCode" 
          class="flex ml-auto mr-auto mt-2 bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 text-xl font-medium rounded"
        >
          {{ copyButtonText }}
        </button>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue';

export default defineComponent({
  name: 'App',
  setup() {
    const copyButtonText = ref('COPY');
    const restoId = ref('Bistro Van Dimi');
    const color = ref('red');

    const codeSnippet = computed(() => {
      return `<script>
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
<\/script>
<div class="widget-data" restoId="${restoId.value}" color="${color.value}"><\/div>`;
    });

    const copyCode = () => {
      navigator.clipboard.writeText(codeSnippet.value);
      copyButtonText.value = 'COPIED!';
      setTimeout(() => {
        copyButtonText.value = 'COPY';
      }, 2000);
    };

    return {
      copyButtonText,
      restoId,
      color,
      copyCode
    };
  }
});
</script>