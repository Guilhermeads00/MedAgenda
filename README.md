# 🩺 MedAgenda — Sistema de Agendamento de Consultas Médicas

## Sobre o projeto

O MedAgenda é uma aplicação front-end desenvolvida com Vue.js, com o objetivo de simular o agendamento de consultas médicas de maneira simples e organizada.

O projeto foi desenvolvido como atividade avaliativa da disciplina de Front-End Frameworks, do curso de Análise e Desenvolvimento de Sistemas.

Nossa proposta foi criar uma interface na qual o usuário pudesse visualizar os médicos disponíveis, escolher um profissional, preencher os dados necessários e acompanhar suas consultas agendadas.

Durante o desenvolvimento, procuramos aplicar os conceitos estudados em sala, principalmente componentização, props, diretivas, eventos e reatividade.

## Funcionalidades

- Visualização dos médicos e suas especialidades.
- Seleção de médicos diretamente pelos cards.
- Formulário para agendamento de consultas.
- Seleção de data e horário.
- Validação dos campos obrigatórios.
- Exibição das consultas agendadas.
- Menu com navegação entre seções da mesma página.
- Interface adaptada para computadores e celulares.

## Tecnologias utilizadas

- **Vue.js 3:** desenvolvimento da interface e dos componentes.
- **JavaScript:** funções, variáveis e interações.
- **HTML:** organização dos elementos.
- **CSS:** estilização e responsividade.
- **Vite:** ambiente de desenvolvimento.
- **StackBlitz:** desenvolvimento e testes da aplicação.

Não foram utilizados Vue Router, frameworks CSS ou bibliotecas externas de componentes.

## Organização dos componentes

O projeto foi dividido em quatro componentes principais:

| Componente | Função |
|---|---|
| `Cabecalho.vue` | Exibe a identidade do sistema e o menu. |
| `CardMedico.vue` | Apresenta os médicos e suas especialidades. |
| `ListaConsultas.vue` | Exibe as consultas agendadas. |
| `Rodape.vue` | Apresenta as informações finais do projeto. |

O `App.vue` reúne esses componentes e controla as principais funcionalidades do sistema.

### Conceitos de Vue utilizados

**Props:** utilizadas para passar informações entre os componentes, como o nome e a especialidade de cada médico.

**ref():** utilizado para criar variáveis reativas, armazenar os dados do formulário e atualizar a lista de consultas.

**v-model:** utilizado para conectar os campos do formulário às variáveis.

**v-if:** utilizado para controlar a exibição do formulário e das mensagens de validação.

**v-for:** utilizado para mostrar os médicos e as consultas a partir de listas.

**@click:** utilizado para executar funções quando o usuário clica nos botões.

### Reutilização de componentes

Um dos principais exemplos de reutilização está no `CardMedico.vue`.

Criamos apenas um componente para representar um médico, mas o utilizamos para apresentar diferentes profissionais. As informações são recebidas através de props, evitando a repetição de código.

## Como executar o projeto

É necessário ter o Node.js e o npm instalados.

1. Baixe ou clone este repositório.
2. Abra a pasta do projeto em um terminal.
3. Instale as dependências:

```bash
npm install
```

4. Inicie o ambiente de desenvolvimento:

```bash
npm run dev
```

5. Abra no navegador o endereço indicado pelo terminal.

## Uso de inteligência artificial

Durante o desenvolvimento, utilizamos o ChatGPT como ferramenta de apoio para compreender conceitos, organizar os componentes, corrigir erros e melhorar a interface.

A IA também auxiliou na adaptação de exemplos de Vue.js ao tema de consultas médicas.

Abaixo estão alguns dos principais prompts utilizados, com a indicação das etapas em que foram empregados.

### 1. Planejamento e divisão dos componentes

**Prompt:**

> "O tema da minha equipe é consultas médicas. me auxilie no desenvolvimento de uma aplicação Vue.js One Page, utilizando apenas os conteúdos ensinados pelo professor, sem Vue Router e sem bibliotecas externas."

**Etapa:** planejamento da aplicação e definição dos componentes.

### 2. Análise dos conteúdos estudados

**Prompt:**

> "Isso foi tudo o que foi passado durante as aulas dele. Preciso que você identifique tudo o que foi passado para minimizar comandos não vistos em sala."

**Etapa:** revisão das cinco aulas de Front-End Frameworks e definição dos recursos permitidos.

### 3. Configuração do projeto

**Prompt:**

> "Me auxicilie a criar o sistema de consultas médicas pelo StackBlitz. Quero seguir passo a passo e usar apenas os recursos das cinco aulas."

**Etapa:** configuração do ambiente Vue.js e criação dos arquivos iniciais.

### 4. Correção de erros

**Prompt:**

> "Vou mandar uma foto do código inteiro e você analisa e vê o que há de errado."

**Etapa:** identificação e correção de problemas nos componentes, principalmente na exibição dos cards dos médicos.

### 5. Identidade visual

**Prompt:**

> "Estou achando o site simples demais. Vou enviar alguns sites para você analisar e me indicar para usar como inspiração para a nova identidade visual do projeto."

**Etapa:** reformulação da aparência do MedAgenda, utilizando como referências Doctoralia, BoaConsulta e dr.consulta.

### 6. Melhorias no formulário

**Prompt:**

> "Quero melhorar a área separada para pôr o nome do paciente, a data, o horário e o médico. Dessa forma que está agora é simples e feia."

**Etapa:** organização visual dos campos e melhorias no CSS.

### 7. Eventos e validação

**Prompt:**

> "Agora o botão Agendar deve funcionar, e também a função de validação."

**Etapa:** implementação de interações com `@click`, `ref()` e verificação de campos obrigatórios.

### 8. Responsividade

**Prompt:**

> "Bom dia, chat, me ajude na melhora da responsividade."

**Etapa:** adaptação dos componentes, formulário e menu para diferentes tamanhos de tela utilizando CSS.

### Como utilizamos as respostas

As sugestões foram aplicadas gradualmente no StackBlitz. Durante esse processo, foram testados os componentes, identificados erros, corrigidos problemas de organização e ajuste da interface conforme as necessidades do projeto.

A utilização da IA não substituiu o acompanhamento do desenvolvimento e dos testes da aplicação.

## Limitações

O MedAgenda é uma simulação de front-end desenvolvida para fins acadêmicos.

Os médicos apresentados são fictícios, e os agendamentos ficam armazenados temporariamente durante a utilização da página.

Ao atualizar o navegador, as consultas cadastradas podem ser perdidas, pois o projeto não possui banco de dados.

O sistema não realiza agendamentos reais com clínicas ou profissionais de saúde.

## Integrantes da equipe

Integrante 1: Guilherme da Rocha da Silva
Integrante 2: Enzo Lira da Silva
Integrante 3: Fernando Noronha Braga da Silva
Integrante 4: Salomão Bayonas Miranda Ribeiro

## Disciplina

**Curso:** Análise e Desenvolvimento de Sistemas

**Disciplina:** Front-End Frameworks

**Professor:** André Neto

**Projeto:** MedAgenda — Sistema de Agendamento de Consultas Médicas