# 🩺 MedAgenda 3.0 — Sistema de Agendamento de Consultas

**Projeto acadêmico da disciplina de Front-End Frameworks — Análise e Desenvolvimento de Sistemas (ADS)**

## 1. Apresentação do produto

O **MedAgenda** é um protótipo de aplicação web criado para tornar mais simples a organização de consultas médicas.

Em uma única interface, o paciente pode conhecer os profissionais, preencher um agendamento, consultar um endereço pelo CEP, escolher uma unidade de atendimento e acompanhar suas consultas registradas.

**Problema abordado:** informações sobre médicos, localização de unidades e agendamentos podem ficar dispersas e dificultar a jornada do paciente.

**Público-alvo:** pacientes que desejam uma experiência de agendamento mais organizada e, futuramente, clínicas e consultórios que precisem centralizar esse atendimento.

**Diferenciais:** navegação intuitiva, validação do formulário, consulta de CEP integrada à escolha da unidade e visualização dos agendamentos em uma página própria.

**Observação:** o MedAgenda é uma simulação acadêmica. Os médicos e as unidades são fictícios e não há agendamento real com clínicas.

## 2. Funcionalidades

- Página inicial com apresentação do serviço e acesso rápido às demais páginas.
- Lista de médicos por especialidade, utilizando componentes reutilizáveis.
- Formulário com nome do paciente, médico, data e horário.
- Formatação automática da data (`DD/MM/AAAA`) e horário (`HH:MM`).
- Validação de campos obrigatórios, datas inexistentes ou passadas e horários inválidos.
- Consulta de endereço pela **API ViaCEP**, utilizando requisição HTTP GET.
- Exibição das unidades somente após uma consulta de CEP bem-sucedida.
- Sugestão de unidade no mesmo município, quando houver correspondência.
- Seleção da unidade como parte do agendamento.
- Confirmação visual da consulta.
- Listagem e cancelamento dos agendamentos.
- Armazenamento das consultas por meio de `localStorage`.
- Layout responsivo e navegação sem recarregar toda a aplicação.

## 3. Tecnologias utilizadas

| Tecnologia | Utilização |
|---|---|
| Vue.js 3 | Componentes, diretivas, eventos e reatividade |
| Vue Router 4 | Navegação SPA entre quatro rotas |
| Bootstrap 5 | Grid, formulários, botões e responsividade |
| JavaScript | Validação e lógica de agendamento |
| API ViaCEP | Consulta de endereço usando `fetch()` e JSON |
| localStorage | Persistência local dos agendamentos |
| Vite e npm | Desenvolvimento e execução |
| HTML e CSS | Estrutura e identidade visual personalizada |

O Bootstrap complementa o CSS do projeto, preservando a identidade visual do MedAgenda.

## 4. Navegação com Vue Router

O MedAgenda utiliza o conceito de **Single Page Application (SPA)**.

Isso significa que o usuário pode navegar entre diferentes páginas sem recarregar todo o documento HTML.

| Rota | Página | Funcionalidade |
|---|---|---|
| `/` | `InicioView.vue` | Apresentação do produto |
| `/medicos` | `MedicosView.vue` | Listagem e seleção de médicos |
| `/agendar` | `AgendarView.vue` | Formulário e confirmação |
| `/consultas` | `ConsultasView.vue` | Consultas registradas |

As rotas são configuradas em `src/router/index.js`, utilizando `createRouter()` e `createWebHistory()`.

O componente `RouterLink` permite a navegação entre as páginas, enquanto `RouterView`, localizado em `App.vue`, exibe a página selecionada.

## 5. Componentização e reatividade

O projeto foi organizado em componentes reutilizáveis para facilitar a manutenção e evitar a repetição de código.

**Principais componentes:**

- `Cabecalho.vue`: identidade visual e navegação.
- `CardMedico.vue`: apresentação dos profissionais.
- `ConsultaCep.vue`: pesquisa de CEP e seleção de unidades.
- `ListaConsultas.vue`: visualização e cancelamento das consultas.
- `Rodape.vue`: informações finais da aplicação.

### Recursos Vue utilizados

**`ref()`**

Cria variáveis reativas para armazenar informações do formulário, resultados da API e agendamentos.

**`v-model`**

Conecta os campos do formulário às variáveis reativas.

**`v-if`**

Controla a exibição de resultados, mensagens de erro e confirmação.

**`v-for`**

Percorre listas de médicos, unidades e consultas.

**`@click`**

Executa funções quando o usuário interage com os botões.

**Props e eventos personalizados**

Permitem compartilhar informações entre componentes, incluindo a comunicação da unidade escolhida ao formulário.

Os dados compartilhados dos agendamentos estão organizados no arquivo `src/agenda.js`.

## 6. Integração com Bootstrap 5

O Bootstrap foi utilizado para melhorar a aparência, a organização dos elementos e a responsividade.

### Classes utilizadas

| Classe | Função |
|---|---|
| `container-xl` | Organiza a largura do conteúdo |
| `d-flex` | Alinha elementos utilizando Flexbox |
| `row` e `col-md-6` | Criam layouts responsivos |
| `form-control` | Estiliza campos de texto |
| `form-select` | Estiliza listas de seleção |
| `btn` | Padroniza botões |
| `shadow-sm` | Adiciona sombras |
| `rounded-4` | Arredonda bordas |
| `alert-danger` | Destaca mensagens de erro |

As principais melhorias foram realizadas no cabeçalho, nos cards dos médicos, no formulário e na organização das consultas.

## 7. Integração com a API ViaCEP

O MedAgenda utiliza a API pública **ViaCEP** para consultar informações de endereços brasileiros.

**API utilizada:** https://viacep.com.br/

**Endpoint:**

`https://viacep.com.br/ws/{cep}/json/`

**Método HTTP:** GET

**Formato de resposta:** JSON

A requisição é implementada no arquivo:

`src/services/cep.js`

### Exemplo de código

```javascript
const resposta = await fetch(
  `https://viacep.com.br/ws/${cep}/json/`,
  {
    method: 'GET'
  }
)

if (!resposta.ok) {
  throw new Error(
    'Não foi possível consultar o CEP. Tente novamente.'
  )
}

const dados = await resposta.json()
```

A função `fetch()` realiza a requisição HTTP.

O `await` aguarda a resposta da API, enquanto `json()` interpreta os dados recebidos para utilização no JavaScript.

A integração utiliza programação assíncrona para consultar informações externas sem bloquear toda a interface.

### Tratamento de erros

O sistema verifica diferentes situações:

- CEP com quantidade incorreta de números.
- Falha de comunicação com a API.
- Resposta HTTP inválida.
- CEP não encontrado.
- Consulta em andamento.
- Endereço recebido com sucesso.

Durante a consulta, o botão apresenta uma mensagem de carregamento. Após a resposta, os dados são exibidos dinamicamente pelo Vue.

## 8. Escolha das unidades de atendimento

A consulta de CEP foi integrada ao formulário para permitir que o paciente escolha onde deseja ser atendido.

Foram cadastradas três unidades fictícias:

| Unidade | Localização |
|---|---|
| Unidade BR-316 | Região da BR-316, Marituba/PA |
| Unidade Umarizal | Bairro Umarizal, Belém/PA |
| Unidade Cidade Nova | Bairro Cidade Nova, Ananindeua/PA |

O cadastro está localizado em `src/services/unidades.js`.

### Funcionamento

1. O paciente informa seu CEP.
2. O MedAgenda consulta a API ViaCEP.
3. O endereço retornado é apresentado na interface.
4. As três unidades cadastradas ficam disponíveis.
5. Uma unidade da mesma cidade pode ser destacada como sugestão.
6. O paciente seleciona a unidade desejada.
7. A unidade é registrada junto aos dados do agendamento.

A consulta utiliza a cidade e, quando aplicável, a referência de bairro.

**Importante:** o ViaCEP não calcula distâncias entre endereços e consultórios. Portanto, a sugestão não representa necessariamente a unidade mais próxima em quilômetros.

## 9. Como realizar um agendamento

O paciente deve:

1. Acessar a página **Médicos** e escolher um profissional, ou abrir **Agendar** diretamente.
2. Informar nome, médico, data e horário.
3. Consultar um CEP válido.
4. Escolher uma unidade de atendimento.
5. Confirmar o agendamento.
6. Acessar **Minhas consultas** para visualizar os dados registrados.

O sistema impede a confirmação quando existem campos obrigatórios inválidos ou quando nenhuma unidade foi selecionada.

Os agendamentos podem ser cancelados posteriormente.

## 10. Organização dos arquivos

```text
src/
├── assets/
│   └── hospital-corredor.jpg
├── components/
│   ├── Cabecalho.vue
│   ├── CardMedico.vue
│   ├── ConsultaCep.vue
│   ├── ListaConsultas.vue
│   └── Rodape.vue
├── router/
│   └── index.js
├── services/
│   ├── cep.js
│   └── unidades.js
├── views/
│   ├── InicioView.vue
│   ├── MedicosView.vue
│   ├── AgendarView.vue
│   └── ConsultasView.vue
├── agenda.js
├── App.vue
├── main.js
├── medagenda.css
└── style.css
```

Essa organização separa a interface, a lógica de agendamentos, as rotas e a integração com a API.

## 11. Como executar o projeto

É necessário ter Node.js e npm instalados em versões compatíveis com as dependências do projeto.

Depois de baixar ou clonar o repositório, abra a pasta do MedAgenda no terminal.

### Instalar dependências

```bash
npm install
```

### Iniciar a aplicação

```bash
npm run dev
```

Abra no navegador o endereço informado pelo Vite.

### Gerar a versão de produção

```bash
npm run build
```

Também é possível executar a aplicação pelo StackBlitz.

A consulta ViaCEP depende de acesso à internet.

## 12. Evolução do projeto

O MedAgenda foi desenvolvido e aprimorado ao longo da disciplina de Front-End Frameworks.

**Primeira etapa — Vue.js**

Desenvolvimento da estrutura inicial, componentes reutilizáveis, formulários, props, eventos e reatividade.

**Segunda etapa — Bootstrap 5**

Melhorias na identidade visual, nos botões, nos cards, no formulário e na responsividade.

**Terceira etapa — Vue Router**

Organização da aplicação em quatro páginas, com navegação SPA sem recarregamento completo.

**Quarta etapa — Integração com API**

Consumo de dados externos por meio da API ViaCEP, utilizando `fetch()`, HTTP GET, JSON e programação assíncrona.

**Quinta etapa — Consolidação**

Integração da escolha da unidade ao agendamento, validação das informações, armazenamento local, melhorias visuais e preparação da versão final.

## 13. Dificuldades e aprendizados

Durante o desenvolvimento, enfrentamos dificuldades relacionadas à organização dos componentes, adaptação do Bootstrap ao CSS existente, configuração das rotas e integração da API ao formulário.

Também foi necessário compreender como diferentes componentes se comunicam e como manter as informações dos agendamentos disponíveis durante a navegação.

Com o projeto, aprofundamos nossos conhecimentos sobre componentização, reatividade, Single Page Applications, programação assíncrona, requisições HTTP e tratamento de dados JSON.

Se iniciássemos o projeto novamente, priorizaríamos desde o começo uma separação mais clara entre componentes, páginas, serviços e lógica de negócio.

## 14. Possíveis melhorias futuras

O MedAgenda poderá evoluir com:

- Autenticação de pacientes e profissionais.
- Banco de dados para armazenamento centralizado.
- Cadastro de clínicas e unidades reais.
- Disponibilidade de horários por médico.
- Confirmação real de consultas.
- Notificações e lembretes.
- Cálculo de distância e rotas até as unidades.
- Painel administrativo para gerenciamento de agendamentos.

Essas funcionalidades não fazem parte da versão atual.

## 15. Limitações

O MedAgenda é um protótipo desenvolvido para fins acadêmicos.

Os médicos e as unidades de atendimento são fictícios.

As consultas não são enviadas a clínicas reais e o projeto não possui um back-end próprio para gerenciar agendamentos.

Os dados são armazenados localmente no navegador por meio de `localStorage`, podendo ser apagados ao limpar os dados do navegador.

A integração com ViaCEP consulta informações de endereço, mas não realiza cálculos de distância nem confirma a disponibilidade das unidades.

## 16. Utilização de inteligência artificial

Durante o desenvolvimento, utilizamos o ChatGPT para auxiliar na compreensão de conceitos, organização do código, correção de erros e implementação de funcionalidades.

Alguns dos principais prompts utilizados foram:

| Prompt | Etapa |
|---|---|
| "beleza, entao me da ai o passo a passo da instalação do vue router e do bootstrap" | Instalação das dependências |
| "vamos para a função de impedir horarios e datas impossiveis" | Validação do formulário |
| "atualize a funcionalidade e adicione ai tres unidades BR-316, Marituba umarizal, Belém cidade nova, ananindeua" | Cadastro das unidades |
| "eu não gostei mostrar as unidades deforma fixa, quando o usuario adicionar o cep, coloque para mostrar as uniades, quanto menos coisa grande na tela, melhor" | Simplificação da interface de CEP |
| "tá, agora integre tudo isso no formulario de agendamento, para que o paciente selecione em qual undade ele quer ser atendido, adicionando funcionalidade aos botoes" | Integração com o formulário |
| "abre o arquivo e compara com o que o professor pede para a apresentação final" | Revisão da entrega final |

As sugestões foram revisadas e testadas durante o desenvolvimento no StackBlitz.

O uso de IA foi uma ferramenta de apoio. A equipe é responsável por compreender e apresentar as funcionalidades implementadas.

## 17. Integrantes da equipe

- Guilherme da Rocha da Silva
- Enzo Lira da Silva
- Fernando Noronha Braga da Silva
- Salomão Bayonas Miranda Ribeiro

**Curso:** Análise e Desenvolvimento de Sistemas (ADS)

**Disciplina:** Front-End Frameworks

**Professor:** André Neto

---

### Conclusão

O MedAgenda demonstra como uma aplicação Vue.js pode evoluir de um formulário simples para uma SPA organizada, responsiva e integrada a serviços externos.

A solução reúne navegação, validação, consulta de CEP, seleção de unidade e acompanhamento de agendamentos em uma única interface.

Com a evolução do projeto, conseguimos aplicar os principais conhecimentos adquiridos na disciplina e demonstrar tanto o funcionamento técnico quanto o potencial do MedAgenda como produto.
