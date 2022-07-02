<script setup>
  const { data, pending, error } = await useFetch(
    'https://api.adviceslip.com/advice'
  );

  const slip = ref(JSON.parse(data.value).slip);
</script>

<template>
  <div
    class="bg-dark-grayish-blue text-center pt-10 pb-16 px-8 rounded-xl relative md:px-12 md:pt-12 md:pb-20"
  >
    <h1 class="text-neon-green text-sm font-semibold tracking-widest">
      Advice #{{ data ? slip.id : '##' }}
    </h1>
    <blockquote class="text-[28px] text-light-cyan font-extrabold mt-6">
      "{{ slip.advice }}"
    </blockquote>
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
