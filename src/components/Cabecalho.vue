
<
  <script setup>
  defineProps([
    'nome',
    'descricao',
    'fecharFormulario',
    'abrirFormulario'
  ])
  </script>
  

<template>
  <header class="cabecalho">

    <div class="marca">
      <div class="logo">+</div>

      <div class="nome-sistema">
        <h1>{{ nome }}</h1>
        <p>{{ descricao }}</p>
      </div>
    </div>

    
<nav class="menu">

<a href="#inicio" @click="fecharFormulario">
Início
</a>

<a href="#medicos">Médicos</a>
<a
href="#inicio"
class="destaque"
@click="abrirFormulario"
>
Agendar
</a>
</nav>


  </header>
</template>

<style scoped>

.menu a {
  color: #12344a;
  text-decoration: none;
  font-size: 14px;
  font-weight: bold;
}

.menu a:hover {
  color: #096f69;
  cursor: pointer;
}

.cabecalho {
  background-color: white;
  padding: 22px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  border-bottom: 1px solid #e4edeb;
  flex-wrap: wrap;
}

.marca {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo {
  background-color: #e9f7f3;
  color: #096f69;
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 30px;
  font-weight: bold;
}

.nome-sistema h1 {
  color: #12344a;
  font-size: 24px;
  margin: 0;
  line-height: 1.3;
}

.nome-sistema p {
  color: #64748b;
  font-size: 12px;
  margin: 4px 0 0;
}

.menu {
  display: flex;
  align-items: center;
  gap: 25px;
}

.menu span {
  color: #12344a;
  font-size: 14px;
  font-weight: bold;
}

.menu .destaque {
  background-color: #096f69;
  color: white;
  padding: 12px 20px;
  border-radius: 8px;
}.menu .destaque {
  background-color: #096f69;
  color: white;
  padding: 12px 20px;
  border-radius: 8px;
  text-decoration: none;
  cursor: pointer;
}

.menu .destaque:hover {
  background-color: #10514d;
  color: white;
}

@media (max-width: 600px) {
  .cabecalho {
    flex-direction: column;
    padding: 20px 15px;
    gap: 20px;
  }

  .marca {
    justify-content: center;
  }

  .nome-sistema h1 {
    font-size: 22px;
  }

  .menu {
    width: 100%;
    justify-content: center;
    gap: 18px;
    flex-wrap: wrap;
  }

  .menu a {
    font-size: 13px;
  }

  .menu .destaque {
    padding: 10px 15px;
  }
}

</style>
