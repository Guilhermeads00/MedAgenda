

<
  <script setup>
  defineProps(['consultas'])
  </script>
  
  <template>
  <section class="consultas" id="consultas">
      <div class="titulo-consultas">
        <h2>Minhas consultas</h2>
        <p>Acompanhe seus agendamentos em um só lugar.</p>
      </div>
  
      <div v-if="consultas.length === 0" class="sem-consultas">
        <div class="icone-calendario">+</div>
        <h3>Nenhuma consulta agendada</h3>
        <p>Seus próximos agendamentos aparecerão aqui.</p>
      </div>
  
      <div
        v-for="(consulta, index) in consultas"
        :key="index"
        class="card-consulta"
      >
        <div class="status">
          ✓ Consulta agendada
        </div>
  
        <div class="dados-principais">
          <div class="avatar-medico">
            +
          </div>
  
          <div>
            <h3>{{ consulta.medico }}</h3>
            <p>Paciente: {{ consulta.nome }}</p>
          </div>
        </div>
  
        <div class="detalhes">
          <div class="detalhe">
            <span>Data da consulta</span>
            <strong>{{ consulta.data }}</strong>
          </div>
  
          <div class="detalhe">
            <span>Horário</span>
            <strong>{{ consulta.horario }}</strong>
          </div>
        </div>
      </div>
    </section>
  </template>
  
  <style scoped>
  .consultas {
    background-color: #f7f9fc;
    padding: 50px 25px;
  }
  
 
.titulo-consultas {
  text-align: left;
  max-width: 1050px;
  margin: 0 auto 30px;
}

  
  .titulo-consultas h2 {
    color: #12344a;
    font-size: 26px;
    margin-bottom: 10px;
  }
  
  .titulo-consultas p {
    color: #64748b;
    font-size: 14px;
  }
  
  .sem-consultas {
    background-color: white;
    border: 1px solid #dfe8e7;
    border-radius: 14px;
    padding: 30px;
    max-width: 1050px;
    margin: 0 auto;
    text-align: center;
  }
  
  .icone-calendario {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: #e9f7f3;
    color: #096f69;
    font-size: 28px;
    margin: 0 auto 15px;
  }
  
  .sem-consultas h3 {
    color: #12344a;
  }
  
  .sem-consultas p {
    color: #64748b;
    font-size: 14px;
  }
  
  .card-consulta {
    background-color: white;
    border: 1px solid #dfe8e7;
    border-radius: 14px;
    padding: 25px;
max-width: 1050px;
width: 100%;
box-sizing: border-box;

    margin: 18px auto;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.04);
  }
  
  .status {
    color: #096f69;
    background-color: #e9f7f3;
    padding: 8px 12px;
    border-radius: 8px;
    font-size: 12px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  .dados-principais {
    display: flex;
    align-items: center;
    gap: 15px;
    margin-bottom: 20px;
  }
  
  .avatar-medico {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background-color: #e9f7f3;
    color: #096f69;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    font-weight: bold;
  }
  
  .dados-principais h3 {
    color: #12344a;
    margin: 0 0 6px;
  }
  
  .dados-principais p {
    color: #64748b;
    margin: 0;
    font-size: 14px;
  }
  
  .detalhes {
    display: flex;
    gap: 15px;
    border-top: 1px solid #e5eceb;
    padding-top: 20px;
  }
  
  .detalhe {
    flex: 1;
    background-color: #f7f9fc;
    border-radius: 8px;
    padding: 12px;
  }
  
  .detalhe span {
    display: block;
    color: #64748b;
    font-size: 12px;
    margin-bottom: 6px;
  }
  
  .detalhe strong {
    color: #12344a;
    font-size: 15px;
  }
  
@media (max-width: 600px) {
  .consultas {
    padding: 30px 15px;
  }

  .titulo-consultas h2 {
    font-size: 23px;
  }

  .card-consulta {
    padding: 18px;
    width: 100%;
  }

  .dados-principais {
    gap: 10px;
  }

  .detalhes {
    flex-direction: column;
    gap: 10px;
  }

  .detalhe {
    width: 100%;
  }
}

  </style>
  