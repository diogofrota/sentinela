# Sentinela – Monitoramento Inteligente de Ocorrências Policiais

O **Sentinela** é um sistema web desenvolvido como projeto da disciplina de Engenharia de Software, com foco em apoiar o trabalho policial por meio do **registro estruturado de ocorrências**, **análise de dados operacionais** e **visualização em dashboard**.

O sistema foi pensado a partir da rotina real de um batalhão da Polícia Militar, substituindo controles manuais em planilhas por um fluxo integrado com API e interface web.

---

## 🎯 Objetivos do Projeto

- Centralizar o **registro de ocorrências** em uma base única.
- Facilitar o **acompanhamento da produtividade operacional** (presos, armas, drogas, veículos).
- Entregar **dashboards visuais** para apoiar a tomada de decisão do comando.
- Servir como **prova de conceito** para implantação em ambiente real de quartel.

---

## 🖥️ Funcionalidades

### 1. Home
- Apresentação do sistema e proposta do Sentinela.
- Destaque dos benefícios: monitoramento em tempo real, inteligência operacional e relatórios consolidados.

### 2. Cadastro de Ocorrências
Tela para registrar novas ocorrências com os campos principais:

- ID Ocorrência  
- Dia, Mês, Ano  
- Hora  
- Quantidade de Presos  
- Quantidade de Drogas Apreendidas  
- Veículos Recuperados  
- Armas Apreendidas  
- RG do Policial  
- ID do Local  

Os dados são enviados para o **back-end Java**, que grava as informações no banco de dados.

### 3. Listagem / Edição / Exclusão
- Tabela com a **lista de ocorrências** já cadastradas.
- Ações por linha:
  - **Editar** (carrega os dados no formulário inferior para alteração).
  - **Excluir** (remove a ocorrência do banco).
- Atualização dinâmica da tabela após operações de CRUD.

### 4. Dashboard Operacional
Painel com visão consolidada dos dados:

- **KPIs** (cards superiores):
  - Total de ocorrências
  - Total de presos
  - Total de armas apreendidas
  - Total de veículos recuperados
- **Gráficos**:
  - Ocorrências por dia
  - Ocorrências por horário
  - Ranking de policiais por número de ocorrências
  - Gráfico de totais (drogas, armas, veículos, presos)
- **Card de “Dicas Inteligentes (IA)”** com insights baseados nos dados do dashboard
  (ex.: horários críticos, aumento de ocorrências, desempenho de equipes).

---

## 🧩 Arquitetura da Solução

### Front-end
- **HTML5**, **CSS3** e **JavaScript**
- Layout responsivo com foco em usabilidade
- Navegação por menu:
  - `Home`
  - `Cadastro`
  - `Ler/Editar/Excluir`
  - `DashBoard`
- Consumo da API via `fetch` para:
  - Cadastrar ocorrências
  - Listar dados
  - Atualizar e excluir registros
  - Atualizar gráficos do dashboard

### Back-end
- **Java** (JDK 11 ou superior)
- **Jersey (JAX-RS)** para criação da API REST
- **Grizzly HTTP Server** para subir o servidor HTTP embutido
- Organização em camadas:
  - **Model** – classes de domínio (Policial, Local, Ocorrencia)
  - **DAO/Repository** – acesso ao banco de dados
  - **Resource/Controller** – endpoints REST

### Banco de Dados
- Banco relacional (Oracle DB)
- Tabelas principais:

#### `SENTINELA_POLICIAL`
- `RG_POLICIAL` (PK)
- `NOME`

#### `SENTINELA_LOCAL`
- `ID_LOCAL` (PK)
- Campos de identificação do local (ex.: descrição, bairro, cidade, etc.)

#### `SENTINELA_OCORRENCIA`
- `ID_OCORRENCIA` (PK)
- `DIA_OCORRENCIA`
- `MES_OCORRENCIA`
- `ANO_OCORRENCIA`
- `HORA_OCORRENCIA`
- `QTD_PRESOS`
- `QTD_DROGA_APREENDIDA`
- `QTD_VEICULOS_RECUPERADOS`
- `QTD_ARMAS_APREENDIDAS`
- `RG_POLICIAL` (FK → SENTINELA_POLICIAL)
- `ID_LOCAL` (FK → SENTINELA_LOCAL)

> Obs.: ajuste os nomes das colunas conforme o script SQL final usado no projeto.

---

## 🔌 Endpoints da API (exemplo)

Base URL (exemplo): `http://localhost:8080/api`

### Policial
- `GET /policial` – lista todos os policiais
- `POST /policial` – cadastra um novo policial

### Local
- `GET /local` – lista todos os locais
- `POST /local` – cadastra um novo local

### Ocorrência
- `GET /ocorrencia` – lista todas as ocorrências
- `POST /ocorrencia` – cadastra nova ocorrência
- `PUT /ocorrencia/{id}` – atualiza uma ocorrência
- `DELETE /ocorrencia/{id}` – exclui uma ocorrência

> Os endpoints podem variar conforme a versão do código; atualize aqui com as rotas definitivas do seu projeto.

---

## 🚀 Como Executar o Projeto Localmente

### Pré-requisitos

- **JDK 11+**
- **Maven** instalado
- Banco de dados (Oracle ou compatível) configurado
- Git (para clonar o repositório)

### 1. Clonar o repositório

```bash
git clone https://github.com/SEU_USUARIO/sentinela.git
cd sentinela
