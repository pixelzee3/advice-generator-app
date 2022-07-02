<script setup>
  const { data, pending, error } = await useFetch(
    'https://api.adviceslip.com/advice'
  );

  const id = ref('##');
  const advice = ref('');

  if (!error.value) {
    const slip = JSON.parse(data.value).slip;
    id.value = slip.id;
    advice.value = slip.advice;
  }
</script>

<template>
  <div
    class="bg-dark-grayish-blue text-center pt-10 pb-16 px-8 rounded-xl relative md:px-12 md:pt-12 md:pb-20"
  >
    <h1 class="text-neon-green text-sm font-semibold tracking-widest">
      Advice #{{ id }}
    </h1>
    <div class="mt-6">
      <p v-if="pending" class="text-[28px] text-light-cyan font-extrabold">
        Loading...
      </p>
      <p v-else-if="error" class="text-[28px] text-red-200 font-extrabold">
        Error loading advice!
      </p>
      <blockquote v-else class="text-[28px] text-light-cyan font-extrabold">
        "{{ advice }}"
      </blockquote>
    </div>
    <picture>
      <source
        srcSet="/images/pattern-divider-mobile.svg"
        media="(max-width: 400px)"
      />
      <source srcSet="/images/pattern-divider-desktop.svg" />
      <img
        class="mt-6 md:mt-8 w-full"
        src="/images/pattern-divider-desktop.svg"
        alt=""
      />
    </picture>
    <div class="absolute -bottom-8 left-1/2 -translate-x-1/2">
      <Button />
    </div>
  </div>
</template>
