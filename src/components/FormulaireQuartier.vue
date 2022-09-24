<script setup lang="ts">
import { Ref, ref } from "vue";
import { useRouter } from "vue-router";
import { supabase } from "../supabase";
const router = useRouter();
const props = defineProps<{
  id?: string;
}>();
// TODO: ajout type Quartier
const quartierObject: Ref<any> = ref({});
if (props.id) {
  // On charge les données de la vue quartiercommune
  let { data, error } = await supabase
    .from("Quartier")
    .select("*")
    .eq("code_Quartier", props.id);
  if (error || !data)
    console.log("n'a pas pu charger le table Maison :", error);
  else quartierObject.value = data[0];
}
async function upsertQuartierCommune(dataForm, node) {
  const { data, error } = await supabase.from("Quartier").upsert(dataForm);
  if (error) node.setErrors([error.message]);
  else {
    node.setErrors([]);
    router.push({ name: "quartier-id", params: { id: data[0].code_Quartier } });
  }
}
const { data: listeCommune, error } = await supabase
  .from("Commune")
  .select("*");
if (error) console.log("n'a pas pu charger la table Commune :", error);
const optionsCommune = listeCommune?.map((commune) => ({
  value: commune.code_Commune,
  label: commune.libelle_Commune,
}));
</script>
<template>
  <div class="p-2">
    <RouterLink to="/quartier">Retour à la liste des quartiers</RouterLink>
    <FormKit
      @submit="upsertQuartierCommune"
      type="form"
      v-model="quartierObject"
    >
      <FormKit name="libelle_Quartier" label="Nom du quartier" />
      <FormKit
        type="select"
        name="code_Commune"
        label="Commune"
        :options="optionsCommune"
      />
    </FormKit>
  </div>
</template>
