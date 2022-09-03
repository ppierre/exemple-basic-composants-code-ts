<template>
  <ul>
    <li>
      <routerLink to="/">Accueil</routerLink>
    </li>
    <li>
      <routerLink to="/simple"
        >Deux composants recevant "simplement" les valeurs</routerLink
      >
    </li>
    <li>
      <routerLink to="/liste">listing depuis import</routerLink>
    </li>
    <li>
      <routerLink to="/liste-fetch">listing "dynamique" avec fetch</routerLink>
    </li>
  </ul>
  <div class="p-2">
    <!-- <Suspense> -->
    <routerView />
    <!-- <template #fallback> Chargement... depuis "RouterView..." </template> -->
    <!-- </Suspense> -->
  </div>
</template>
<script setup lang="ts"></script>
