<template>
  <v-main class="bg-slate-950 text-slate-100">
    <main class="mt-10 w-[100%] h-[90vh]">
      <section class="w-[100%] h-[100%] flex flex-col items-center justify-center">
        <v-card width="240px" class="bg-transparent" elevation="0">
          <v-img
              :src="require('@/assets/img/logo.png')"
              alt="logo-ícone barbosa catalisador" cover
          ></v-img>
        </v-card>

        <p class="text-2xl mt-7 text-center font-bold text-amber">
          OPPS! Essa página não foi encontrada!
        </p>
        <p class="mt-4 md:text-lg text-center">
          Volte para a página inicial e descubra como
          <span class="font-bold text-[#00C94F]">Barbosa Catalisador</span>
          pode <br> ajudar você a economizar e proteger o meio ambiente.
        </p>
        <v-btn to="/" class="mt-7 w-[130px] text-none" variant="flat" color="amber">Voltar</v-btn>
      </section>
    </main>
  </v-main>
</template>

<script setup>

</script>
