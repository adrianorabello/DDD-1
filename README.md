# Dinâmica: Design Estratégico do Projeto

## Objetivo
Identificar os subdomínios do projeto, classificá-los (Core, Supporting, Generic) e desenhar os bounded contexts, incluindo suas interações. Esse exercício ajudará a criar uma visão clara e estratégica do domínio.

---

## 1. Nome do Projeto
**Magraz – Plataforma Inteligente de Gestão e Personalização de Dietas Saudáveis.**

---

## 2. Objetivo Principal do Projeto
Desenvolver uma plataforma digital que conecte nutricionistas, fornecedores de refeições saudáveis e clientes finais, oferecendo planos nutricionais personalizados e acompanhamento em tempo real, com o objetivo de promover hábitos alimentares saudáveis, reduzir tempo de planejamento e aumentar a adesão às dietas..
### **Fase 1 – Conexão e Gestão de Planos Nutricionais**
Criar uma plataforma que conecte **nutricionistas**, **fornecedores de refeições saudáveis** e **clientes finais**, possibilitando a **criação e gestão de planos nutricionais personalizados**, com acompanhamento básico de progresso.  
Foco inicial: disponibilizar uma solução funcional que reduza o tempo de planejamento e facilite a comunicação entre os envolvidos.

### **Fase 2 – Inteligência e Otimização em Tempo Real**
Evoluir a plataforma para oferecer **acompanhamento em tempo real**, com recomendações automáticas e ajustes inteligentes nos planos com base em métricas e preferências do cliente.  
Foco: **promover hábitos alimentares saudáveis**, aumentar a adesão às dietas e otimizar a experiência do usuário.


---

## 3. Identificação dos Subdomínios
Liste os subdomínios do sistema e classifique-os como **Core Domain**, **Supporting Subdomain** ou **Generic Subdomain**.

| **Subdomínio**                                           | **Descrição**                                       | **Tipo**                |
|----------------------------------------------------------|-----------------------------------------------------|-------------------------|
| Gestão de Planos Nutricionais                            | Criação, personalização e acompanhamento de dietas  | Core Domain             |                                                          |                                                     |                         |
| Cadastro e Perfil de Usuário                             | Clientes, nutricionistas, fornecedores              | Subdomínios de Suporte  |
| Catálogo de Refeições                                    | Cardápios, ingredientes, valores nutricionais       | Subdomínios de Suporte  |
| Agendamento e Entrega                                    | Integração com logística)                           | Subdomínios de Suporte  |                                                          |                                                     |                         |
| Autenticação e Autorização                               | Login, permissões, segurança                        | Subdomínios Genéricos   |
| Pagamento e Faturamento                                  | Integração com gateways de pagamento                | Subdomínios Genéricos   |
| Notificações                                             | e-mail, push, SMS                                   | Subdomínios Genéricos   |


| Categoria                           | Subdomínio                           | Descrição                                                                                                                                                  |
|-------------------------------------|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Domínio Principal (Core Domain)** | Gestão de Planos Nutricionais        | Criação, personalização e acompanhamento de dietas. Inclui análise de progresso do cliente e ajustes automáticos baseados em métricas e preferências.      |
| **Subdomínios de Suporte**          | Cadastro e Perfil de Usuário         | Gerenciamento de dados de clientes, nutricionistas e fornecedores.                                                                                         |
|                                     | Catálogo de Refeições                | Registro de cardápios, ingredientes e valores nutricionais.                                                                                                |
|                                     | Agendamento e Entrega                | Integração com serviços de logística para entrega de refeições.                                                                                            |
| **Subdomínios Genéricos**           | Autenticação e Autorização           | Controle de login, permissões e segurança do sistema.                                                                                                      |
|                                     | Pagamento e Faturamento              | Integração com gateways de pagamento e gestão financeira.                                                                                                  |
|                                     | Notificações                         | Envio de alertas e mensagens via e-mail, push e SMS.                                                                                                       |
---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context**           | **Responsabilidade**                                                                        | **Subdomínios Relacionados** |
|-------------------------------|---------------------------------------------------------------------------------------------|-----------------------------|
| Contexto de Consultas    | Gerencia as consultas médicas, do agendamento à finalização, incluindo emissão de receitas. | Gestão de Consultas         |
| Contexto de Pagamentos   | Processa cobranças de consultas e repasses para médicos ou clínicas.                        | Pagamentos                  |

---

## 5. Comunicação entre os Bounded Contexts
Para manter consistência na comunicação entre negócio e tecnologia, definimos alguns termos:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)**           | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                  |
|---------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
| Plano Nutricional         | Contexto de Pagamentos      | Mensageria (Evento)         | "Consulta Finalizada"                         |
| Contexto de Cadastro      | Contexto de Consultas      | API                         | Obter informações de um Paciente pelo ID      |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**         | **Descrição**                                                       |
|-------------------|---------------------------------------------------------------------|
| Plano Nutricional | Conjunto de refeições e orientações adaptadas ao perfil do cliente  |
| Fornecedor        | Pessoa ou empresa que produz e entrega refeições.                   |
| Nutricionista     | Profissional que prescreve e ajusta o plano nutricional.            |
| Cliente           | Pessoa que recebe e segue o plano nutricional.                      |
| Refeição          | Preparação alimentar cadastrada no sistema com dados nutricionais.  |
| Entregador        | Responsável por levar a refeição ao cliente.                        |
| Dashboard         | Painel de acompanhamento do progresso do cliente.                   |

---

## 7. Estratégia de Desenvolvimento
Para cada tipo de subdomínio, explique a abordagem para implementação:
- **Core Domain:** Desenvolver internamente com foco total.
- **Supporting Subdomain:** Desenvolver internamente ou parcialmente terceirizar.
- **Generic Subdomain:** Usar ferramentas ou serviços de mercado.

| **Subdomínio**                  | **Estratégia**                   | **Ferramentas ou Serviços (se aplicável)**                                                                                                                                                                                  |
|---------------------------------|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gestão de Planos Nutricionais   | Desenvolvimento interno          | Microservices para escalabilidade e independência de cada contexto delimitado.<br/>Comunicação assíncrona entre serviços usando mensageria (Kafka ou RabbitMQ).<br/>API Gateway para centralizar autenticação e roteamento. |
| Cadastro de Usuários            | Interno com uso de Auth0, Oauth2 | Auth0, Oauth2                                                                                                                                                                                                               |
| Pagamentos                      | Terceirizar usando API           | Api de pagamentos                                                                                                                                                                                                           |
| Entregador                      | Integração com API de terceiros  | Uber, Entrega fácil                                                                                                                                                                                                         |    


---

## 8. Diagrama Visual (Opcional, mas Recomendado)
Desenhe um diagrama que mostre:
- Os bounded contexts.
- Como eles se comunicam.
- A relação com os subdomínios.

Use ferramentas como **Miro**, **Lucidchart** ou mesmo papel e caneta para criar seu diagrama e adicionar ao projeto.

---

## Dicas para Apresentação
- Explique cada parte do design, focando no **Core Domain** (o coração do negócio).
- Justifique por que certos subdomínios foram classificados como Supporting ou Generic.
- Destaque como a comunicação entre bounded contexts foi pensada para ser escalável.

---

Boa sorte com a dinâmica! 🚀
