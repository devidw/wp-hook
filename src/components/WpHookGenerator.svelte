<script>
  import copy from "copy-to-clipboard"
  import { NotificationDisplay, notifier } from "@beyonk/svelte-notifications"

  let actionOrFilter = "action"
  let hookName = ""

  $: code = `/**
 * 
 */
add_${actionOrFilter}(
    hook_name: "${hookName}",
    priority: PHP_INT_MAX,
    accepted_args: 1,
    callback: function() {
        // ...
    }
);`

  function copyToClipboard(e) {
    if (e.charCode == 13) {
      copy(code)
      notifier.success(`${actionOrFilter} copied to clipboard`)
    }
  }
</script>

<NotificationDisplay />

<main class="min-h-screen flex justify-center items-center">
  <div class="bg-stone-700 rounded-3xl p-10">
    <section class="mb-10">
      <div class="space-x-4 mb-5">
        <label>
          <input type="radio" value="action" bind:group={actionOrFilter} />
          action
        </label>
        <label>
          <input type="radio" value="filter" bind:group={actionOrFilter} />
          filter
        </label>
      </div>

      <input
        type="text"
        autofocus
        bind:value={hookName}
        on:keypress={copyToClipboard}
        placeholder="Paste name and hit enter to copy"
        class="block bg-stone-800 rounded-lg p-2 w-full"
      />
    </section>
    <section class="bg-stone-800 p-5 rounded-xl">
      <pre><code>{code}</code></pre>
    </section>
  </div>
</main>
