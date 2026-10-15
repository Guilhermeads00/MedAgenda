
<script setup>
defineProps(['nome', 'especialidade', 'iniciais'])
</script>

<template>
  <div class="card">
    <div class="avatar">
      {{ iniciais }}
    </div>

    <h3>{{ nome }}</h3>

    <p class="especialidade">
      {{ especialidade }}
    </p>

    <div class="informacao">
      <span>Atendimento com agendamento</span>
    </div>
  </div>
</template>

<style scoped>
.card {
  background-color: white;
  border: 1px solid #dfe8e7;
  border-radius: 14px;
  padding: 28px 20px;
 
width: 100%;
box-sizing: border-box;

  text-align: center;
}

.avatar {
  background-color: #e9f7f3;
  color: #096f69;
width: 75px;
height: 75px;
font-size: 24px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  font-weight: bold;
  margin: 0 auto 18px;
}

h3 {
  color: #12344a;
  margin: 10px 0;
  font-size: 20px;
}

.especialidade {
  color: #64748b;
  font-size: 14px;
  margin-bottom: 20px;
}

.informacao {
  background-color: #f4f8f7;
  border-radius: 8px;
  padding: 10px;
  color: #096f69;
  font-size: 12px;
}
</style>
