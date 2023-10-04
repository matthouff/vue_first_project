<template>
  <div class="content">
    <NoteForm :form="form" @update-form="updateForm" />
    <ListNotes :listNote="listNote" @selected-row="selectedRow" />
  </div>
</template>

<script setup>
import { reactive } from "vue";
import { ElMessage } from "element-plus";
import ListNotes from "./ListNotes.vue";
import NoteForm from "./NoteForm.vue";

const form = reactive({
  name: "",
  type: [],
  desc: "",
});

const listNote = reactive([
  {
    id: Math.floor(Math.random() * (1000000 - 1 + 1)) + 1,
    name: "Ma première note",
    date1: new Date().toLocaleDateString(),
    type: ["Online activities"],
    desc: "Ceci est un petit texte juste pour rien dire",
  },
]);

const updateForm = (updatedForm) => {
  // Mettre à jour l'utilisateur avec les données du formulaire
  if (!updatedForm.id && updatedForm.name) {
    const newValue = {
      ...updatedForm,
      id: Math.floor(Math.random() * (1000000 - 1 + 1)) + 1,
      date1: new Date().toLocaleDateString(),
    };
    form.id = newValue.id;
    form.name = newValue.name;
    form.type = newValue.type;
    form.desc = newValue.desc;

    ElMessage({
      message: `La note a bien été ajouté`,
      type: "success",
    });
    return listNote.push(newValue);
  }

  ElMessage({
    message: `La note a bien été modifié`,
    type: "success",
  });
  listNote.forEach((item, index) => {
    if (item.id === updatedForm.id) {
      // Mettre à jour les propriétés de l'objet
      listNote[index] = { ...listNote[index], ...updatedForm };
    }
  });
};

const selectedRow = (row) => {
  form.id = row.id;
  form.name = row.name;
  form.type = row.type;
  form.desc = row.desc;
};
</script>

<style scoped>
.content {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-top: 100px;
}
</style>
