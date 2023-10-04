<template>
  <el-form :model="form" label-width="120px">
    <el-form-item label="Activity name">
      <el-input v-model="form.name" />
    </el-form-item>
    <el-form-item label="Activity type">
      <el-checkbox-group v-model="form.type">
        <el-checkbox label="Online activities" name="type" />
        <el-checkbox label="Promotion activities" name="type" />
        <el-checkbox label="Offline activities" name="type" />
        <el-checkbox label="Simple brand exposure" name="type" />
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="Activity form">
      <el-input v-model="form.desc" type="textarea" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="handleInput" v-if="!form.id"
        >Ajouter</el-button
      >
      <el-button type="primary" @click="handleInput" v-else>Modifier</el-button>
    </el-form-item>
  </el-form>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const { form } = defineProps(["form"]);
const emit = defineEmits(["update-form"]);

const handleInput = () => {
  // Émettre l'événement pour mettre à jour l'utilisateur
  emit("update-form", { ...form, form });
};
</script>

<style scoped></style>
