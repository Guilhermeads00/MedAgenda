# 🩺 MedAgenda — Sistema de Agendamento de Consultas Médicas

## 1. Sobre o projeto

O **MedAgenda** é uma aplicação web desenvolvida em Vue.js 3 para simular o agendamento de consultas médicas de forma simples, rápida e organizada.

O projeto foi desenvolvido na disciplina de **Front-End Frameworks**, do curso de Análise e Desenvolvimento de Sistemas (ADS), e evoluiu ao longo das atividades acadêmicas, incorporando componentização, reatividade, responsividade, Bootstrap 5, Vue Router e integração com uma API externa.

Na atualização mais recente, implementamos a integração com a **API ViaCEP**, permitindo ao paciente consultar seu endereço e selecionar uma das unidades fictícias do MedAgenda antes de confirmar o agendamento.

## 2. Integrantes da equipe

- Guilherme da Rocha da Silva
- Enzo Lira da Silva
- Fernando Noronha Braga da Silva
- Salomão Bayonas Miranda Ribeiro

**Curso:** Análise e Desenvolvimento de Sistemas  
**Disciplina:** Front-End Frameworks  
**Professor:** André Neto

## 3. Tecnologias utilizadas

| Tecnologia | Aplicação no projeto |
|---|---|
| Vue.js 3 | Componentes e interface reativa |
| JavaScript | Lógica, eventos, validações e integração com API |
| Vue Router 4 | Navegação SPA entre as páginas |
| Bootstrap 5 | Estilização e responsividade |
| HTML e CSS | Estrutura e identidade visual |
| Vite | Ambiente de desenvolvimento |
| StackBlitz | Desenvolvimento e testes |
| API ViaCEP | Consulta de endereços por CEP |
| localStorage | Armazenamento local dos agendamentos |

O MedAgenda utiliza uma API pública para consultar endereços, mas não possui um back-end próprio para gerenciar consultas médicas.

## 4. Funcionalidades do sistema

O MedAgenda permite:

- Visualizar os profissionais e suas especialidades.
- Selecionar um médico e iniciar um agendamento.
- Preencher nome do paciente, data e horário.
- Formatar automaticamente a data e o horário.
- Impedir datas inexistentes, passadas e horários inválidos.
- Consultar endereços brasileiros por CEP.
- Visualizar três unidades fictícias de atendimento.
- Receber uma sugestão de unidade com base na cidade do CEP consultado.
- Selecionar a unidade desejada.
- Confirmar o agendamento com a unidade escolhida.
- Consultar e cancelar agendamentos.
- Manter os agendamentos salvos no navegador utilizando `localStorage`.
- Navegar entre páginas sem recarregar toda a aplicação.

A interface também possui estilos responsivos para diferentes tamanhos de tela.

## 5. Organização das páginas com Vue Router

O projeto utiliza Vue Router 4 para implementar uma **Single Page Application (SPA)**.

Uma SPA permite navegar entre diferentes páginas da aplicação sem recarregar todo o documento HTML.

As rotas implementadas são:

| Rota | Componente | Funcionalidade |
|---|---|---|
| `/` | `InicioView.vue` | Página inicial |
| `/medicos` | `MedicosView.vue` | Listagem dos médicos |
| `/agendar` | `AgendarView.vue` | Formulário de agendamento e consulta de CEP |
| `/consultas` | `ConsultasView.vue` | Visualização das consultas registradas |

A configuração das rotas está localizada em `src/router/index.js`.

O componente `RouterLink` realiza a navegação, enquanto `RouterView` exibe a página correspondente à rota atual.

## 6. Evolução visual com Bootstrap 5

O Bootstrap 5 foi integrado ao projeto para melhorar a organização visual, os componentes e a responsividade.

A instalação foi realizada via npm, e o CSS do Bootstrap foi importado no arquivo `src/main.js`.

### Classes utilizadas

| Classe | Função |
|---|---|
| `container-xl` | Organiza a largura do conteúdo |
| `d-flex` | Alinha elementos com Flexbox |
| `align-items-center` | Centraliza elementos verticalmente |
| `shadow-sm` | Adiciona sombra suave |
| `rounded-4` | Arredonda bordas dos componentes |
| `p-4` | Aplica espaçamento interno |
| `form-control` | Padroniza campos de texto |
| `form-select` | Estiliza listas de seleção |
| `row` e `col-md-6` | Organizam elementos em colunas responsivas |
| `btn` | Aplica estilos básicos aos botões |
| `alert-danger` | Destaca mensagens de erro |

As principais melhorias visuais foram realizadas no cabeçalho, nos cards dos médicos e no formulário de agendamento.

Mantivemos também estilos CSS personalizados para preservar a identidade visual do MedAgenda.

---

# 7. Integração Front-End e Back-End com API

## 7.1 API escolhida

Escolhemos a **API ViaCEP**, um serviço público e gratuito utilizado para consultar informações de endereços brasileiros.

A API foi escolhida porque permite acrescentar ao MedAgenda uma funcionalidade relacionada à localização das unidades de atendimento, sem exigir a criação de um servidor próprio.

**Site da API:** https://viacep.com.br/

**Endpoint utilizado:**

`https://viacep.com.br/ws/{cep}/json/`

**Exemplo de requisição:**

`https://viacep.com.br/ws/01001000/json/`

**Método HTTP:** GET  
**Formato dos dados:** JSON  
**Biblioteca utilizada:** `fetch()` nativo do JavaScript

Não é necessário cadastrar uma conta ou gerar uma chave de API para utilizar essa consulta pública.

## 7.2 Como funciona a integração

A integração ocorre na página **Agendar**, dentro do componente `ConsultaCep.vue`.

O funcionamento segue estas etapas:

1. O paciente informa seu CEP.
2. O sistema verifica se foram digitados oito números.
3. Ao clicar em **Buscar unidade**, é realizada uma requisição HTTP GET à API ViaCEP.
4. A API retorna os dados do endereço em formato JSON.
5. O JavaScript interpreta a resposta recebida.
6. O Vue atualiza a interface com o endereço encontrado.
7. O sistema mostra as três unidades cadastradas e destaca uma unidade da mesma cidade, quando disponível.
8. O paciente escolhe a unidade onde deseja ser atendido.
9. A unidade selecionada é registrada junto aos demais dados da consulta.

A consulta do CEP é feita em tempo de execução, utilizando uma API externa.

## 7.3 Código da requisição HTTP GET

A lógica de comunicação com a API está localizada em:

`src/services/cep.js`

Trecho utilizado:

```javascript
const resposta = await fetch(
  `https://viacep.com.br/ws/${cep}/json/`,
  {
    method: 'GET'
  }
)

const dados = await resposta.json()
```

A função `fetch()` realiza a requisição HTTP.

O `await` aguarda a conclusão da operação assíncrona.

O método `resposta.json()` interpreta o corpo da resposta e disponibiliza os dados em um objeto JavaScript.

Antes de utilizar a resposta, o código também verifica possíveis erros HTTP e a indicação de CEP inexistente retornada pelo ViaCEP.

## 7.4 Processamento dos dados JSON

A API pode retornar informações como:

```json
{
  "cep": "01001-000",
  "logradouro": "Praça da Sé",
  "bairro": "Sé",
  "localidade": "São Paulo",
  "uf": "SP"
}
```

O MedAgenda utiliza os dados relevantes para apresentar o endereço consultado.

Os campos utilizados incluem CEP, logradouro, bairro, município e estado.

No serviço `cep.js`, o campo `localidade` é convertido para `cidade`, facilitando sua utilização nos componentes.

## 7.5 Programação assíncrona

A consulta utiliza `async` e `await`.

A programação assíncrona permite que a aplicação faça uma requisição à API sem bloquear toda a interface enquanto aguarda a resposta.

No componente, também utilizamos `try`, `catch` e `finally` para controlar o processamento da requisição e os possíveis problemas.

## 7.6 Recursos de Vue utilizados na integração

**`ref()`**

Armazena informações reativas, como o CEP, o endereço encontrado, os estados de carregamento e as mensagens de erro.

**`v-model`**

Conecta o campo de CEP à variável correspondente.

**`v-if`**

Controla a exibição dos resultados, mensagens e indicadores de carregamento.

**`v-for`**

Percorre a lista das três unidades e apresenta seus cartões dinamicamente.

**Interpolação**

Apresenta valores das variáveis no HTML, utilizando a sintaxe `{{ ... }}`.

**`@click`**

Executa a pesquisa do CEP e permite selecionar a unidade desejada.

**Props e eventos personalizados**

Permitem que o componente `ConsultaCep.vue` comunique a unidade escolhida à página de agendamento.

## 7.7 Tratamento de carregamento, erros e ausência de resultados

Foram implementados diferentes estados para melhorar a experiência do usuário.

| Situação | Comportamento do sistema |
|---|---|
| Carregando | Mostra “Consultando...” e desabilita o botão |
| CEP incompleto | Solicita um CEP válido com oito números |
| Erro de rede ou HTTP | Exibe uma mensagem de erro |
| CEP inexistente | Informa que o endereço não foi encontrado |
| CEP encontrado | Mostra o endereço e as unidades disponíveis |
| Nenhuma unidade selecionada | Impede a confirmação do agendamento |

Esses tratamentos evitam que a interface apresente informações incorretas ou permita o envio de um agendamento incompleto.

---

# 8. Unidades de atendimento

Para integrar a consulta de CEP ao formulário, cadastramos três unidades fictícias do MedAgenda.

| Unidade | Localização de referência |
|---|---|
| Unidade BR-316 | Região da BR-316, Marituba/PA |
| Unidade Umarizal | Bairro Umarizal, Belém/PA |
| Unidade Cidade Nova | Bairro Cidade Nova, Ananindeua/PA |

As unidades estão cadastradas em:

`src/services/unidades.js`

## 8.1 Indicação da unidade

Após a consulta do CEP, o sistema identifica o município informado pela API.

Quando existe uma unidade cadastrada na mesma cidade, ela é destacada como sugestão.

Quando não existe unidade na cidade consultada, as três opções continuam disponíveis para escolha do paciente.

**Importante:** o sistema não calcula distâncias em quilômetros nem rotas de deslocamento. A indicação considera o município e, quando aplicável, a referência de bairro.

## 8.2 Seleção da unidade

As unidades são apresentadas em cartões clicáveis.

Quando o paciente seleciona uma unidade:

- O cartão escolhido recebe destaque visual.
- A identificação da unidade fica armazenada em uma variável reativa.
- O formulário exige uma unidade válida para confirmar o agendamento.
- A unidade escolhida é salva junto aos dados da consulta.
- A página **Minhas consultas** apresenta a unidade de atendimento selecionada.

O endereço pesquisado no ViaCEP não é armazenado junto ao agendamento; somente a unidade escolhida é registrada.

## 8.3 Armazenamento dos agendamentos

Os agendamentos são armazenados no navegador por meio do `localStorage`.

Entre as informações registradas estão:

- Nome do paciente.
- Médico escolhido.
- Data da consulta.
- Horário.
- Unidade de atendimento.
- Cidade da unidade.

O armazenamento é local e não representa um cadastro real em um servidor.

---

# 9. Organização dos arquivos

O projeto mantém uma separação entre páginas, componentes e serviços.

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

### Responsabilidades dos principais arquivos

| Arquivo | Responsabilidade |
|---|---|
| `App.vue` | Estrutura principal da aplicação |
| `main.js` | Inicialização do Vue, Bootstrap e roteador |
| `router/index.js` | Configuração das rotas |
| `agenda.js` | Lógica e estado compartilhado dos agendamentos |
| `ConsultaCep.vue` | Campo de pesquisa, resultados e seleção de unidade |
| `services/cep.js` | Requisição à API ViaCEP |
| `services/unidades.js` | Unidades fictícias e regra de sugestão |
| `AgendarView.vue` | Formulário e confirmação de agendamento |
| `ListaConsultas.vue` | Listagem e cancelamento de consultas |

Essa organização facilita a manutenção e a compreensão do código.

---

# 10. Como executar o projeto

O projeto pode ser executado no StackBlitz ou localmente.

Para execução local, é necessário possuir Node.js e npm instalados em versões compatíveis com as dependências do projeto.

### Passo 1 — Instalar as dependências

```bash
npm install
```

### Passo 2 — Iniciar o servidor de desenvolvimento

```bash
npm run dev
```

### Passo 3 — Abrir a aplicação

Abra no navegador o endereço informado pelo terminal do Vite.

Para testar a API, é necessário que o navegador tenha acesso à internet.

---

# 11. Testes realizados e demonstração

O projeto foi desenvolvido e testado durante suas diferentes etapas no StackBlitz.

Para demonstrar a integração com a API, sugerimos o seguinte roteiro:

1. Abrir a página **Agendar**.
2. Preencher o nome do paciente, médico, data e horário.
3. Digitar o CEP `68795-000`, correspondente a Benevides/PA.
4. Clicar em **Buscar unidade**.
5. Mostrar o endereço retornado pela API.
6. Explicar que, como não existe unidade fictícia cadastrada em Benevides, as três unidades são disponibilizadas para escolha.
7. Selecionar a Unidade Cidade Nova, por exemplo.
8. Confirmar o agendamento.
9. Navegar até **Minhas consultas** e mostrar a unidade registrada.

Também é possível demonstrar os estados de erro digitando um CEP incompleto ou consultando um CEP inexistente.

A resposta da API depende da disponibilidade do serviço e da conexão com a internet.

---

# 12. Utilização de inteligência artificial

Durante a evolução do MedAgenda, utilizamos o ChatGPT como ferramenta de apoio para organizar o desenvolvimento, compreender conceitos, corrigir erros e implementar novas funcionalidades.

A seguir estão alguns dos principais prompts utilizados durante o projeto.

### Planejamento e validação

**Prompt:**  
"vamos para a função de impedir horarios e datas impossiveis"

**Etapa:** implementação de validações para impedir agendamentos com informações inválidas.

### Integração do Vue Router e Bootstrap

**Prompt:**  
"beleza, entao me da ai o passo a passo da instalação do vue router e do bootstrap"

**Etapa:** instalação e configuração dos frameworks no StackBlitz.

### Nova atividade de integração com API

**Solicitação:**  
Envio do enunciado da atividade de integração Front-End e Back-End por meio de APIs, solicitando a evolução do projeto MedAgenda.

**Etapa:** escolha da API ViaCEP e planejamento da integração.

### Cadastro das unidades

**Prompt:**  
"atualize a funcionalidade e adicione ai tres unidades BR-316, Marituba umarizal, Belém cidade nova, ananindeua"

**Etapa:** definição das três unidades fictícias.

### Simplificação da interface

**Prompt:**  
"eu não gostei mostrar as unidades deforma fixa, quando o usuario adicionar o cep, coloque para mostrar as uniades, quanto menos coisa grande na tela, melhor"

**Etapa:** reorganização da interface para exibir as unidades somente após a consulta de CEP.

### Integração da escolha da unidade ao agendamento

**Prompt:**  
"tá, agora integre tudo isso no formulario de agendamento, para que o paciente selecione em qual undade ele quer ser atendido, adicionando funcionalidade aos botoes"

**Etapa:** implementação dos botões de seleção e armazenamento da unidade junto ao agendamento.

### Documentação do projeto

**Prompt:**  
"fala cara, atualiza o readme da med agenda com base no que o trabalho pede, voce lembra?"

**Etapa:** atualização da documentação conforme os requisitos acadêmicos.

As sugestões geradas com auxílio de IA foram incorporadas ao projeto e revisadas durante o desenvolvimento. O grupo é responsável por compreender, testar e apresentar as funcionalidades implementadas.

---

# 13. Limitações do projeto

O MedAgenda é uma aplicação acadêmica e demonstrativa.

- Os médicos e as unidades são fictícios.
- As consultas não são registradas em clínicas reais.
- O sistema não possui banco de dados nem servidor próprio para armazenar agendamentos.
- Os agendamentos são armazenados somente no navegador utilizado.
- A API ViaCEP fornece dados de endereço, mas não calcula distâncias.
- A indicação de unidade utiliza uma correspondência por município, e não geolocalização.
- A disponibilidade real dos médicos não é consultada.
- O funcionamento da consulta de CEP depende de acesso à internet.

## 14. Conclusão

A evolução do MedAgenda permitiu aplicar, na prática, conceitos importantes do desenvolvimento Front-End.

Inicialmente, trabalhamos com componentes, props, diretivas e reatividade no Vue.js.

Posteriormente, implementamos navegação SPA com Vue Router e aprimoramos a interface por meio do Bootstrap.

Na atividade mais recente, integramos a API ViaCEP ao formulário de agendamento utilizando requisições HTTP GET, programação assíncrona, respostas JSON e atualização reativa da interface.

Também criamos uma interação na qual o paciente consulta seu endereço, visualiza as unidades disponíveis, seleciona uma unidade e registra essa escolha junto ao agendamento.

Com isso, o projeto demonstra como uma aplicação Vue pode consumir informações externas e utilizá-las para oferecer novas funcionalidades sem reconstruir toda a aplicação.
