<script lang="ts">
  export let title: string;
  export let vata: string;
  export let pitta: string;
  export let kapha: string;
</script>

<div class="flex flex-col gap-2">
  <p class="font-light text-3xl">{title}</p>
  <label>
    <input class="w-4 h-4" type="radio" name={title} value="vata" />
    {vata}
  </label>
  <label>
    <input class="w-4 h-4" type="radio" name={title} value="pitta" />
    {pitta}
  </label>
  <label>
    <input class="w-4 h-4" type="radio" name={title} value="kapha" />
    {kapha}
  </label>
</div>
