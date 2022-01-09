<script lang="ts">
  import { slide } from 'svelte/transition';
  import Question from '$lib/Question.svelte';
  import questions from '../questions.json';

  let showResult = false;
  let result: {
    vata?: number;
    pitta?: number;
    kapha?: number;
  };
  let dosha: string;

  function handleSubmit(e: Event) {
    const formData = new FormData(e.target as HTMLFormElement);
    const data = Object.fromEntries(formData);
    const values = Object.values(data);

    result = values.reduce(
      (obj, answer: string) => {
        ++obj[answer];
        return obj;
      },
      {
        vata: 0,
        pitta: 0,
        kapha: 0
      }
    );
    dosha = Object.entries(result)
      .sort((a, b) => b[1] - a[1])
      .map(([key]) => key)
      .slice(0, 2)
      .join('-');
    showResult = true;
  }
</script>

<main w-dark="bg-cool-gray-800 text-true-gray-400">
  <div class="flex flex-col gap-7 p-9 max-w-5xl mx-auto">
    <h1 class="font-light text-3xl">Ayurveda | Dosha Prakriti Quiz</h1>

    <h3 class="font-light">
      Please answer the questions as objectively as you can. Try to answer with the idea in mind
      that you are assessing yourself based on general tendencies that you have held since around
      the age of 17 years until now. Also, base your answers on people with your genetic/cultural
      background. If you have trouble with some questions, ask someone who has known you for a while
      for an objective answer.
    </h3>

    <a
      class="text-indigo-800 underline"
      href="https://drive.google.com/file/d/168m-yX2vdUoj6_DaDp1j3aSHdsA-wIhU/view">Source</a
    >

    <form class="grid grid-cols-1 gap-9 sm:grid-cols-2" on:submit|preventDefault={handleSubmit}>
      {#each questions as fields}
        <Question {...fields} />
      {/each}
      <button
        class="p-4 rounded-xl bg-indigo-700 text-white font-bold text-2xl transition duration-300"
        w-hover="bg-white border border-black text-black"
        w-active="bg-indigo-700 text-white"
        type="submit"
      >
        Get your result
      </button>
    </form>

    {#if showResult}
      <div class="flex flex-col items-center p-10" transition:slide>
        <p class="font-light text-4xl">Your dosha is:</p>
        <p class="font-light text-4xl">{dosha}</p>
        <div class="flex justify-between w-64">
          <p class="font-light text-xl">Vata: {result.vata}</p>
          <p class="font-light text-xl">Pitta: {result.pitta}</p>
          <p class="font-light text-xl">Kapha: {result.kapha}</p>
        </div>
      </div>
    {/if}
  </div>
</main>
