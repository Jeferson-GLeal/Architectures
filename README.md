# 🧩 Arquiteturas de Software

A **arquitetura de software** define **como os componentes de um sistema se organizam, interagem e evoluem** ao longo do tempo.  
Ela serve como um guia estrutural que equilibra **performance, manutenibilidade, escalabilidade e flexibilidade**.

Existem diversos estilos arquiteturais, e a escolha do modelo certo depende do **tamanho do projeto**, **requisitos de negócio** e **maturidade da equipe**.

---

## 🏗️ 1. Arquitetura Monolítica

### 💡 Descrição
É o modelo mais tradicional, onde **toda a aplicação é construída e implantada como um único bloco**.  
Todas as camadas (apresentação, lógica de negócio e persistência) estão no mesmo código e deploy.

### ⚙️ Exemplo
Uma aplicação Spring Boot única (`algafood-api.jar`) com pacotes:

com.algaworks.algafood.api  
com.algaworks.algafood.domain  
com.algaworks.algafood.infrastructure  

---  

### ✅ Vantagens
- Simples de desenvolver e implantar  
- Baixo custo inicial  
- Ideal para MVPs e sistemas pequenos  

### ⚠️ Desvantagens
- Dificuldade de escalar partes específicas  
- Deploy único (um erro afeta tudo)  
- Manutenção complexa a longo prazo  

---

## 🧱 2. Arquitetura em Camadas (Layered Architecture)

### 💡 Descrição
Divide o sistema em **camadas horizontais**, onde cada uma possui uma responsabilidade específica.  
É uma das arquiteturas mais utilizadas em sistemas corporativos Java.

### 🧩 Camadas típicas
- **Controller:** entrada das requisições HTTP  
- **Service:** regras de negócio  
- **Repository:** acesso a dados  
- **Model:** entidades e domínio

### ✅ Vantagens
- Estrutura organizada e intuitiva  
- Separação de responsabilidades  
- Base para arquiteturas mais avançadas  

### ⚠️ Desvantagens
- Dependências entre camadas podem gerar acoplamento  
- Escalabilidade limitada  

---

## ☁️ 3. Arquitetura de Microsserviços (Microservices Architecture)

### 💡 Descrição
A aplicação é dividida em **vários serviços pequenos e independentes**, cada um com uma responsabilidade específica e banco de dados próprio.  
Os serviços se comunicam via **REST API** ou **mensageria** (RabbitMQ, Kafka).

### ⚙️ Exemplo

pedido-service/  
pagamento-service/  
notificacao-service/  

---

### ✅ Vantagens
- Escalabilidade e deploy independentes  
- Alta resiliência  
- Ideal para equipes e domínios separados  

### ⚠️ Desvantagens
- Complexidade de comunicação e infraestrutura  
- Necessidade de observabilidade (logs, tracing, monitoramento)

---

## 🔄 4. Arquitetura Orientada a Eventos (Event-Driven Architecture)

### 💡 Descrição
Os serviços não se comunicam diretamente, mas sim **por meio de eventos assíncronos**.  
Quando algo acontece em um serviço, ele **publica um evento**, e outros serviços **reagem** a ele.

### ⚙️ Exemplo
- `PedidoService` publica “PagamentoConfirmado”  
- `EntregaService` consome o evento e processa a entrega  

### ✅ Vantagens
- Desacoplamento total entre os serviços  
- Alta performance e escalabilidade  
- Comunicação assíncrona  

### ⚠️ Desvantagens
- Fluxo difícil de rastrear  
- Complexidade de monitoramento  

---

## 🧠 5. Arquitetura Hexagonal (Ports and Adapters)

### 💡 Descrição
Proposta por **Alistair Cockburn**, essa arquitetura separa o **núcleo da aplicação (regras de negócio)** da **infraestrutura (bancos, APIs, UI)**.  
A comunicação é feita por **Ports (interfaces)** e **Adapters (implementações concretas)**.

### ⚙️ Estrutura típica

core/  
├── domain/  
├── ports/  
│ ├── input/  
│ └── output/  
adapters/  
├── inbound/ (controllers)  
└── outbound/ (repositories, APIs)  


### ✅ Vantagens
- Domínio puro e independente de frameworks  
- Código mais testável e flexível  

### ⚠️ Desvantagens
- Estrutura inicial mais complexa  
- Curva de aprendizado maior  

---

## 🧼 6. Arquitetura Limpa (Clean Architecture)

### 💡 Descrição
Proposta por **Robert C. Martin (Uncle Bob)**, a **Clean Architecture** organiza o sistema em **camadas concêntricas**,  
onde as regras de negócio estão no centro e **não dependem de frameworks, banco ou interface externa**.

### ⚙️ Estrutura  

entities/ → Regras de negócio puras  
usecases/ → Casos de uso  
adapters/ → Controladores, gateways, presenters  
frameworks/ → Banco, API, mensageria  

### ✅ **Vantagens**
- Altamente modular e testável  
- Total independência de tecnologias externas  
- Excelente para sistemas corporativos  

### ⚠️ **Desvantagens**
- Sobrecarga inicial para sistemas pequenos  
- Exige forte disciplina arquitetural  

---

## 🧱 **7. Arquitetura Modular (Modular Monolith)**

### 💡 **Descrição**
Uma evolução do monólito tradicional.  
O sistema é único, mas o código é **dividido em módulos independentes**, cada um representando um **domínio de negócio**.

### ⚙️ **Exemplo**  

core/  
pedido/  
pagamento/  
cliente/  

---

### ✅ **Vantagens**
- Simplicidade do monólito com melhor organização  
- Facilidade para evoluir para microsserviços  
- Build e deploy únicos  

### ⚠️ **Desvantagens**
- Ainda há dependência entre módulos  
- Escalabilidade limitada  

---

## 🧭 **8. Arquitetura Orientada a Serviços (SOA)**

### 💡 **Descrição**
Divisão do sistema em **serviços corporativos reutilizáveis**, geralmente comunicando-se por um **barramento (ESB)**.  
Foi o precursor dos microsserviços.

### ✅ **Vantagens**
- Reuso entre sistemas  
- Integração com sistemas legados  

### ⚠️ **Desvantagens**
- Forte acoplamento com o barramento  
- Escalabilidade limitada  

---

## 🪶 **9. Arquitetura Serverless**

### 💡 **Descrição**
A aplicação é composta por **funções executadas sob demanda** na nuvem, sem a necessidade de gerenciar servidores.  
Cada função é chamada via **API Gateway** e executa uma tarefa isolada.

### ⚙️ **Exemplo**
- AWS Lambda + API Gateway + DynamoDB

### ✅ **Vantagens**
- Escalabilidade automática  
- Pagamento apenas pelo uso  
- Sem manutenção de servidores  

### ⚠️ **Desvantagens**
- Dificuldade para testes locais  
- Cold start em execuções ocasionais  

---

## 🧭 **Resumo Comparativo**

| Arquitetura | Tipo | Escalabilidade | Complexidade | Ideal para |
|--------------|------|----------------|---------------|-------------|
| **Monolítica** | Local | 🔸 Baixa | 🟢 Baixa | MVPs e sistemas pequenos |
| **Em Camadas** | Local | 🔸 Média | 🟢 Média | APIs REST corporativas |
| **Modular** | Local | 🔸 Média | 🟡 Média | Sistemas médios/grandes |
| **Hexagonal** | Local | 🔸 Alta | 🟠 Alta | Projetos com domínio forte |
| **Clean Architecture** | Local | 🔸 Alta | 🔴 Alta | SaaS, fintechs, produtos longos |
| **SOA** | Distribuída | 🔸 Média | 🟠 Alta | Integrações corporativas |
| **Microsserviços** | Distribuída | 🔸 Muito Alta | 🔴 Alta | Sistemas escaláveis |
| **Event-Driven** | Distribuída | 🔸 Muito Alta | 🔴 Alta | Sistemas reativos/distribuídos |
| **Serverless** | Nuvem | 🔸 Alta | 🟡 Média | Automaçã

