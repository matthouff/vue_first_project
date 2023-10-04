<template>
  <div class="list-note">
    <div class="titleContent">
      <h1>Mes notes</h1>
      <el-button type="primary" primary @click="handleReset">Ajouter</el-button>
    </div>

    <el-table :data="props.listNote" style="width: 100%" @row-click="selected">
      <el-table-column prop="name" label="Name" width="180" />
      <el-table-column prop="date1" label="Créé le" align="right" />
    </el-table>
  </div>
</template>

<script setup>
const props = defineProps(["listNote"]);
const emit = defineEmits(["selected-row"]);

const selected = (value) => {
  emit("selected-row", value);
};

const handleReset = () => {
  emit("selected-row", {});
};
</script>

<style scoped>
.list-note {
  padding-top: 30px;
  border-top: 3px solid #fff;
}
.titleContent {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
