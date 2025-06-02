# Projeto CI/CD Pipeline

Este repositório contém a implementação de um pipeline de Integração Contínua e Entrega Contínua (CI/CD) para uma aplicação Python com Docker, utilizando GitHub Actions.

---

## O que foi implementado e modificado

### Workflow GitHub Actions

- Configuração do pipeline para rodar em pushes e pull requests nas branches `main` e `master`.
- Permissões configuradas para leitura de conteúdos e escrita de pacotes.
  
### Jobs configurados:

1. **Testes (`testing-job`)**
   - Checkout do código usando `actions/checkout@v4`.
   - Instalação do Python 3.11 com `actions/setup-python@v5`.
   - Cache do Poetry para acelerar instalação das dependências.
   - Instalação do Poetry via pip e configuração para uso sem virtualenvs.
   - Instalação das dependências do projeto via Poetry.
   - Execução dos testes com `pytest` incluindo geração de relatórios de cobertura (`coverage.xml`) e resultados (`test-results.xml`).
   - Upload dos artefatos de teste (`test-results.xml` e `coverage.xml`) para visualização posterior.

2. **Linting (`linting-job`)**
   - Mesma configuração inicial (checkout, Python, cache e Poetry).
   - Execução de verificações estáticas de código:
     - `flake8` para linting.
     - `black` para verificação de formatação.
     - `isort` para verificação da organização dos imports.

3. **Build da Imagem Docker (`build-job`)**
   - Checkout do código.
   - Configuração do Docker Buildx para builds avançados.
   - Build da imagem Docker com tags usando o hash do commit e `latest`.
   - Salvamento da imagem Docker em arquivo `app.tar`.
   - Upload do artefato da imagem Docker para ser utilizado em jobs posteriores.

4. **Execução da Imagem Docker (`run-built-image`)**
   - Download do artefato da imagem Docker.
   - Carregamento da imagem no Docker local do runner.
   - Execução da aplicação em container Docker, expondo a porta 8080.
   - Verificação se o container está rodando e health check via curl.
   - Exibição dos logs do container.
   - Parada e remoção do container após execução.

---

## Tecnologias utilizadas

- Python 3.11
- Poetry para gerenciamento de dependências
- Pytest para testes unitários e cobertura
- Docker para containerização da aplicação
- GitHub Actions para automação do pipeline CI/CD

---

## Como usar

Para rodar localmente, clone o repositório, instale as dependências com Poetry e execute os testes.

Para ver o pipeline funcionando, faça push para a branch `main` ou `master` e acompanhe as execuções na aba **Actions** do GitHub.

---

## Link para o repositório

https://github.com/Erica4Almeida/workshop_cv