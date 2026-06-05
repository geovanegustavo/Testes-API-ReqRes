# Testes-API-ReqRes

# Automação de Testes de API - ReqRes E2E & Contrato

Este repositório contém um projeto robusto de automação de testes de API de ponta a ponta (E2E) e testes de contrato, desenvolvido utilizando o **Postman** e integrado a uma esteira de Integração Contínua (CI/CD) via **GitHub Actions**.

O objetivo principal do projeto é garantir a qualidade, a integridade dos dados e a estabilidade dos contratos de comunicação das rotas de autenticação e gerenciamento de usuários da API pública **ReqRes.in**.

## Tecnologias e Ferramentas Utilizadas

* **Postman:** Criação, organização e gerenciamento das coleções de requisições e scripts de testes.
* **JavaScript (ES6):** Desenvolvimento de lógica para manipulação de dados, variáveis dinâmicas e asserções.
* **Ajv (Another JSON Schema Validator):** Biblioteca nativa do Postman utilizada para a validação rigorosa dos schemas de contrato.
* **Newman:** Executor de coleções do Postman via linha de comando (CLI), permitindo a portabilidade dos testes.
* **Newman-Reporter-Htmlextra:** Gerador de relatórios visuais avançados em formato HTML.
* **GitHub Actions:** Orquestração do pipeline de CI para execução automatizada dos testes a cada alteração de código.

## Escopo dos Testes Automatizados

O projeto cobre cenários críticos de testes organizados em fluxos lógicos e encadeados:

1.  **Fluxo de Autenticação (Login):**
    * Validação de resposta com Status Code `200 OK`.
    * Extração dinâmica do Token de Autenticação (`token`) via script de teste e armazenamento automático em Variável de Ambiente.
2.  **Gerenciamento Dinâmico de Usuários (Cadastro):**
    * Uso de *Pre-request Scripts* em JavaScript para geração randômica de massa de dados (`FirstName`, `LastName` e `FullName`).
    * Validação de resposta com Status Code `201 Created`.
    * **Teste de Contrato (JSON Schema):** Validação estrutural de tipos de dados e obrigatoriedade de campos complexos e objetos aninhados (como o bloco `_meta`).
    * **Teste de Integridade de Dados:** Asserção dinâmica comparando os valores enviados (variáveis) com o corpo de retorno da API.

## Arquitetura do Pipeline (CI/CD)

A esteira automatizada foi configurada para isolar dados sensíveis e garantir a segurança do projeto:
* **Gerenciamento de Ambientes:** Centralização de URLs e variáveis dinâmicas em arquivos de *Environment*.
* **Segurança da Informação:** Injeção segura da chave de acesso (`x-api-key`) em tempo de execução utilizando **GitHub Actions Secrets** (`secrets.REQRES_API_KEY`), evitando a exposição de credenciais no histórico do Git.
* **Artefatos de Execução:** Geração e armazenamento automatizado de relatórios gráficos de testes (`Report.html`) como artefatos de build na plataforma do GitHub.
