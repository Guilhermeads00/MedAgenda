
<script setup>
import { ref } from 'vue'

import Cabecalho from './components/Cabecalho.vue'
import CardMedico from './components/CardMedico.vue'
import ListaConsultas from './components/ListaConsultas.vue'
import Rodape from './components/Rodape.vue'



const medicos = [
  {
    id: 1,
    nome: 'Dra. Ana Souza',
    especialidade: 'Cardiologia',
    iniciais: 'AS'
  },
  {
    id: 2,
    nome: 'Dr. André Neto',
    especialidade: 'Dermatologia',
    iniciais: 'AN'
  },
  {
    id: 3,
    nome: 'Dra. Mariana Costa',
    especialidade: 'Clínica Geral',
    iniciais: 'MC'
  }
]


const mostrarFormulario = ref(false)

const nomePaciente = ref('')
const medicoSelecionado = ref('')
const dataConsulta = ref('')
const horarioConsulta = ref('')

const consultas = ref([])
const mensagemErro = ref('')
const mostrarSucesso = ref(false)
function abrirFormulario() {
  mostrarSucesso.value = false
  mostrarFormulario.value = true
}


function fecharFormulario() {
  mostrarFormulario.value = false
  mostrarSucesso.value = false
  mensagemErro.value = ''
}
function agendarComMedico(nome) {
  medicoSelecionado.value = nome
  mostrarSucesso.value = false
  mostrarFormulario.value = true
  mensagemErro.value = ''
}


  

function confirmarAgendamento() {
  if (
    nomePaciente.value.trim() === '' ||
    medicoSelecionado.value === '' ||
    dataConsulta.value === '' ||
    horarioConsulta.value === ''
  ) {
    mensagemErro.value = 'Preencha todos os campos para continuar.'
  } else if (!validarData()) {
    mensagemErro.value = 'Informe uma data válida que não esteja no passado.'
  } else if (!validarHorario()) {
    mensagemErro.value = 'Informe um horário válido entre 00:00 e 23:59.'
  } else {
    consultas.value.push({
      nome: nomePaciente.value,
      medico: medicoSelecionado.value,
      data: dataConsulta.value,
      horario: horarioConsulta.value
    })

    nomePaciente.value = ''
    medicoSelecionado.value = ''
    dataConsulta.value = ''
    horarioConsulta.value = ''

    mensagemErro.value = ''
    mostrarFormulario.value = false
    mostrarSucesso.value = true
  }
}

  


function novoAgendamento() {
  mostrarSucesso.value = false
  mostrarFormulario.value = true
  mensagemErro.value = ''
}

function formatarData() {
  let numeros = dataConsulta.value.replace(/\D/g, '')

  if (numeros.length > 4) {
    dataConsulta.value =
      numeros.slice(0, 2) + '/' +
      numeros.slice(2, 4) + '/' +
      numeros.slice(4, 8)
  } else if (numeros.length > 2) {
    dataConsulta.value =
      numeros.slice(0, 2) + '/' +
      numeros.slice(2, 4)
  } else {
    dataConsulta.value = numeros
  }
}

function formatarHorario() {
  let numeros = horarioConsulta.value.replace(/\D/g, '')

  if (numeros.length > 2) {
    horarioConsulta.value =
      numeros.slice(0, 2) + ':' +
      numeros.slice(2, 4)
  } else {
    horarioConsulta.value = numeros
  }
}

function validarData() {
  let partes = dataConsulta.value.split('/')

  if (partes.length !== 3) {
    return false
  }

  let dia = Number(partes[0])
  let mes = Number(partes[1])
  let ano = Number(partes[2])

  if (
    partes[0].length !== 2 ||
    partes[1].length !== 2 ||
    partes[2].length !== 4
  ) {
    return false
  }

  if (mes < 1 || mes > 12 || ano < 1) {
    return false
  }

  let data = new Date(ano, mes - 1, dia)

  if (
    data.getFullYear() !== ano ||
    data.getMonth() !== mes - 1 ||
    data.getDate() !== dia
  ) {
    return false
  }

  let hoje = new Date()
  hoje.setHours(0, 0, 0, 0)

  if (data < hoje) {
    return false
  }

  return true
}

function validarHorario() {
  let partes = horarioConsulta.value.split(':')

  if (partes.length !== 2) {
    return false
  }

  if (
    partes[0].length !== 2 ||
    partes[1].length !== 2
  ) {
    return false
  }

  let horas = Number(partes[0])
  let minutos = Number(partes[1])

  if (
    horas < 0 ||
    horas > 23 ||
    minutos < 0 ||
    minutos > 59
  ) {
    return false
  }

  return true
}

</script>

<template>
  
<Cabecalho
  nome="MedAgenda"
  descricao="Sua saúde em boas mãos"
  :fecharFormulario="fecharFormulario"
  :abrirFormulario="abrirFormulario"
/>


<div class="pagina" id="inicio">
    

<div class="apresentacao">

<div class="texto-apresentacao">
  <p class="etiqueta">
    CUIDADO E PRATICIDADE EM UM SÓ LUGAR
  </p>

  <h2>Sua saúde merece atenção sem complicação.</h2>

  <p class="descricao-inicial">
    Encontre especialistas e agende suas consultas
    de maneira simples e organizada.
  </p>

  <button @click="abrirFormulario">
    Agendar minha consulta →
  </button>

  <p class="vantagens">
    ✓ Simples &nbsp;&nbsp; ✓ Rápido &nbsp;&nbsp; ✓ Organizado
  </p>
</div>

<div class="painel-informativo">
  <div class="painel-titulo">
    <div class="icone-painel">+</div>

    <div>
      <h3>Agendamento simples</h3>
      <p>Três passos para sua próxima consulta</p>
    </div>
  </div>

  <div class="passo">
    <span>1</span>
    <p>Escolha um médico</p>
  </div>

  <div class="passo">
    <span>2</span>
    <p>Informe a data e o horário</p>
  </div>

  <div class="passo">
    <span>3</span>
    <p>Confirme sua consulta</p>
  </div>
</div>

</div>


   
<div
v-if="mostrarFormulario"
class="formulario"
id="agendamento"
>

      <h3>Agendamento de consulta</h3>

      <p class="subtitulo-formulario">
        Preencha os dados abaixo para confirmar sua consulta.
      </p>

      <div class="campo">
        <label>Nome do paciente:</label>
        <input
          type="text"
          v-model="nomePaciente"
          placeholder="Digite seu nome"
        >
      </div>

      <div class="campo">
        <label>Escolha o médico:</label>
        <select v-model="medicoSelecionado">
          <option value="">Selecione um médico</option>

          <option
            v-for="medico in medicos"
            :key="medico.id"
            :value="medico.nome"
          >
            {{ medico.nome }} - {{ medico.especialidade }}
          </option>
        </select>
      </div>




  <div class="linha-data-horario">
    <div class="campo">
      <label>Data da consulta:</label>
      <input
      type="text"
      v-model="dataConsulta"
      @input="formatarData"
      placeholder="DD/MM/AAAA"
      maxlength="10"
      >
    </div>
  
    <div class="campo">
      <label>Horário:</label>
      <input
      type="text"
      v-model="horarioConsulta"
      @input="formatarHorario"
      placeholder="HH:MM"
      maxlength="5"
      >
    </div>
  </div>
  



<p v-if="mensagemErro !== ''" class="mensagem-erro">
{{ mensagemErro }}
</p>
      <button @click="confirmarAgendamento">
        Confirmar agendamento
      </button>
    </div>
    <div v-if="mostrarSucesso" class="confirmacao">
      <div class="icone-sucesso">✓</div>
    
      <h2>Consulta agendada com sucesso!</h2>
    
      <p>
        Seu agendamento foi registrado.
        Você pode acompanhar os detalhes
        na seção Minhas consultas.
      </p>
    
      <div class="botoes-confirmacao">
        <a href="#consultas">
          Ver minhas consultas
        </a>
    
        <button @click="novoAgendamento">
          Agendar outra consulta
        </button>
      </div>
    </div>
    
  </div>

  <section class="medicos" id="medicos">
    
<h2>Encontre seu especialista</h2>
<p class="descricao-medicos">
  Conheça nossos profissionais disponíveis para agendamento.
</p>

    <div class="lista-medicos">
     

    <div
    v-for="medico in medicos"
    :key="medico.id"
    class="item-medico"
  >
    <CardMedico
      :nome="medico.nome"
      :especialidade="medico.especialidade"
      :iniciais="medico.iniciais"
    />
  
    <button @click="agendarComMedico(medico.nome)">
      Agendar consulta
    </button>
  </div>
  
    </div>
  </section>

  <ListaConsultas :consultas="consultas" />

  <Rodape />
</template>

<style scoped>
.pagina {
  text-align: center;
  padding: 50px 20px;
  font-family: Arial, sans-serif;
}

.pagina h2 {
  color: #176b66;
  margin-bottom: 10px;
}

.pagina p {
  color: #666666;
}

button {
  background-color: #176b66;
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 8px;
  cursor: pointer;
}

button:hover {
  background-color: #10514d;
}

.formulario {
  background-color: white;
  border: 1px solid #dddddd;
  border-radius: 16px;
  padding: 30px;
  margin: 35px auto 0;
  max-width: 420px;
  text-align: left;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.formulario h3 {
  color: #176b66;
  text-align: center;
  margin-top: 0;
  margin-bottom: 10px;
}

.formulario .subtitulo-formulario {
  text-align: center;
  color: #777777;
  font-size: 14px;
  margin-bottom: 25px;
}

.campo {
  margin-bottom: 18px;
}

.campo label {
  display: block;
  margin-bottom: 8px;
  color: #444444;
  font-weight: bold;
}

.formulario input,
.formulario select {
  width: 100%;
  padding: 12px;
  border: 1px solid #cccccc;
  border-radius: 8px;
  box-sizing: border-box;
  font-size: 15px;
  background-color: #f9f9f9;
}

.formulario input:focus,
.formulario select:focus {
  outline: none;
  border-color: #176b66;
  background-color: white;
}

.formulario button {
  display: block;
  width: 100%;
  margin: 25px auto 0;
  padding: 14px;
  font-size: 15px;
}

.medicos {
  padding: 35px 20px;
  background-color: #f4f8f7;
  text-align: center;
}


.medicos h2 {
  text-align: left;
  max-width: 1050px;
  margin: 0 auto 10px;
  color: #12344a;
  font-size: 26px;
}

.descricao-medicos {
  text-align: left;
  max-width: 1050px;
  margin: 0 auto 30px;
  color: #64748b;
  font-size: 15px;
}


.lista-medicos {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  flex-wrap: wrap;
  max-width: 1050px;
  margin: 0 auto;
}

.pagina {
  background-color: #e9f7f3;
}


.apresentacao {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 45px;
  max-width: 1000px;
  margin: 0 auto;
  text-align: left;
}


.texto-apresentacao {
  flex: 1;
}

.painel-informativo {
  flex: 1;
  background-color: white;
  border: 1px solid #dfe8e7;
  border-radius: 18px;
  padding: 30px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.05);
}

.painel-titulo {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 25px;
}

.icone-painel {
  background-color: #e9f7f3;
  color: #096f69;
  width: 45px;
  height: 45px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 28px;
  font-weight: bold;
}

.painel-titulo h3 {
  color: #12344a;
  margin: 0;
  font-size: 18px;
}

.painel-titulo p {
  color: #64748b;
  font-size: 13px;
  margin: 5px 0 0;
}

.passo {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-top: 18px;
}

.passo span {
  background-color: #e9f7f3;
  color: #096f69;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

.passo p {
  color: #12344a;
  font-size: 14px;
  margin: 0;
}



.apresentacao .etiqueta {
  color: #087d73;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1px;
  margin-bottom: 20px;
}

.apresentacao h2 {
  color: #12344a;
  font-size: 36px;
  line-height: 1.2;
  margin-bottom: 20px;
}

.apresentacao .descricao-inicial {
  color: #536779;
  font-size: 17px;
  line-height: 1.7;
  margin-bottom: 25px;
}

.apresentacao button {
  background-color: #096f69;
  font-size: 15px;
  padding: 15px 28px;
  border-radius: 10px;
}

.apresentacao .vantagens {
  
.texto-apresentacao {
  text-align: left;
}

.texto-apresentacao h2 {
  text-align: left;
}

.texto-apresentacao .descricao-inicial {
  text-align: left;
}

.texto-apresentacao .etiqueta {
  text-align: left;
}

.texto-apresentacao .vantagens {
  text-align: left;
}

}

.item-medico {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
  min-width: 220px;
  max-width: 340px;
}


.item-medico button {
  margin-top: 12px;
  width: 100%;
  background-color: #096f69;
}

.item-medico button:hover {
  background-color: #10514d;
}

.linha-data-horario {
  display: flex;
  gap: 15px;
}

.linha-data-horario .campo {
  flex: 1;
  min-width: 0;
}

.linha-data-horario input {
  width: 100%;
}

@media (max-width: 500px) {
  .linha-data-horario {
    flex-direction: column;
    gap: 0;
  }
}

.formulario .mensagem-erro {
  background-color: #fff1f0;
  color: #b42318;
  border: 1px solid #fecdca;
  border-radius: 8px;
  padding: 12px;
  font-size: 13px;
  text-align: center;
  margin: 15px 0;
}

@media (max-width: 600px) {
  .pagina {
    padding: 35px 15px;
  }

  .apresentacao h2 {
    font-size: 27px;
  }

  .apresentacao .descricao-inicial {
    font-size: 15px;
  }

  .medicos {
    padding: 30px 15px;
  }

  .lista-medicos {
    flex-direction: column;
    align-items: center;
    gap: 25px;
  }

  .item-medico {
    width: 100%;
    max-width: 320px;
  }

  .item-medico button {
    width: 100%;
  }

  .formulario {
    padding: 20px;
    width: 100%;
    max-width: 100%;
  }
}

@media (max-width: 600px) {
  .pagina {
    padding: 35px 15px;
  }

  .apresentacao h2 {
    font-size: 27px;
  }

  .apresentacao .descricao-inicial {
    font-size: 15px;
  }

  .medicos {
    padding: 30px 15px;
  }

  .lista-medicos {
    flex-direction: column;
    align-items: center;
    gap: 25px;
  }

  .item-medico {
    width: 100%;
    max-width: 320px;
  }

  .item-medico button {
    width: 100%;
  }

  .formulario {
    padding: 20px;
    width: 100%;
    max-width: 100%;
  }
}

@media (max-width: 700px) {
  .apresentacao {
    flex-direction: column;
    gap: 30px;
  }

  .texto-apresentacao {
    width: 100%;
  }

  .texto-apresentacao h2 {
    font-size: 28px;
  }

  .painel-informativo {
    width: 100%;
    box-sizing: border-box;
    padding: 25px;
  }
}

.confirmacao {
  background-color: white;
  border: 1px solid #dfe8e7;
  border-radius: 18px;
  padding: 35px;
  max-width: 460px;
  margin: 35px auto 0;
  text-align: center;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.05);
}

.icone-sucesso {
  background-color: #e9f7f3;
  color: #096f69;
  width: 65px;
  height: 65px;
  border-radius: 50%;
  margin: 0 auto 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 32px;
}

.confirmacao h2 {
  color: #12344a;
  font-size: 23px;
}

.confirmacao p {
  color: #64748b;
  line-height: 1.6;
  font-size: 14px;
}

.botoes-confirmacao {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 25px;
}

.botoes-confirmacao a,
.botoes-confirmacao button {
  display: block;
  padding: 13px;
  border-radius: 8px;
  text-decoration: none;
  font-size: 14px;
  text-align: center;
  cursor: pointer;
  width: 100%;
  box-sizing: border-box;
}

.botoes-confirmacao a {
  background-color: #096f69;
  color: white;
}

.botoes-confirmacao button {
  background-color: #e9f7f3;
  color: #096f69;
}

.medicos h2 {
  text-align: left;
  max-width: 1050px;
  margin: 0 auto 10px;
  color: #12344a;
  font-size: 26px;
}

.descricao-medicos {
  text-align: left;
  max-width: 1050px;
  margin: 0 auto 30px;
  color: #64748b;
  font-size: 15px;
}

.item-medico {
  flex: 1;
  min-width: 220px;
}

</style>
