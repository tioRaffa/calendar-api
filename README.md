# Plataforma Interna de Agendamento de Consultas

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)

Uma ferramenta interna para clínicas e consultórios gerenciarem o agendamento de consultas com seus médicos, com um fluxo completo desde a marcação pelo paciente até o pagamento e notificação.

---

## ✨ Sobre o Projeto

Este projeto foi desenhado como uma solução completa para a gestão de agendamentos de uma empresa de saúde. O sistema centraliza a agenda dos médicos da casa, permitindo que pacientes realizem o agendamento de forma autônoma e segura.

A gestão dos médicos (cadastro de novos profissionais, definição de especialidades, valor da consulta e horários de trabalho) é realizada **exclusivamente pela equipe administrativa** através do painel de administração do Django, garantindo total controle sobre os profissionais listados na plataforma.

O projeto está **atualmente em fase de desenvolvimento**, com foco em criar um fluxo robusto e confiável para pacientes e administradores.

## 🚀 Principais Funcionalidades

* **Para Administradores da Clínica:**
    * Cadastro e gestão completa do perfil dos médicos da casa.
    * Definição centralizada da agenda de trabalho e horários de cada profissional.
    * Visualização de todas as consultas agendadas no sistema.
* **Para Pacientes:**
    * Autenticação simples e segura via Firebase.
    * Busca e visualização dos médicos disponíveis na clínica.
    * Acesso em tempo real aos horários livres de cada médico.
    * Agendamento com pagamento online integrado via Stripe.
    * Confirmação instantânea da consulta na própria plataforma após o pagamento.
    * Recebimento de um lembrete via WhatsApp no dia da consulta.

## 🛠️ Tecnologias Utilizadas

Este projeto utiliza um stack de tecnologias modernas, focado em entregar as funcionalidades de forma eficiente e organizada.

* **Backend:**
    * **Python 3.11+**
    * **Django 5.0+**
    * **Django REST Framework**
* **Banco de Dados:**
    * **PostgreSQL** (Para armazenamento persistente dos dados da aplicação)
* **Tarefas Assíncronas e Filas:**
    * **Celery** (Para executar o envio de notificações em segundo plano)
    * **Redis** (Como "fila de mensagens" para o Celery, não armazena dados da aplicação)
* **Conteinerização:**
    * **Docker & Docker Compose** (Para criar um ambiente de desenvolvimento consistente e isolado)
* **Servidor de Desenvolvimento:**
    * **Servidor nativo do Django** (`manage.py runserver`)
    *(Nota: Para um ambiente de produção real, a recomendação seria utilizar uma combinação como Gunicorn e Nginx. Para o desenvolvimento atual, o servidor do Django é suficiente.)*
* **Serviços Externos e APIs:**
    * **Firebase Authentication** (Autenticação de Pacientes)
    * **Stripe** (Processamento de Pagamentos)
    * **Meta/WhatsApp API** (Envio de Notificações)

## 🏗️ Como Executar o Projeto

Com o projeto totalmente conteinerizado, a configuração do ambiente de desenvolvimento é direta.

**Pré-requisitos:**
* [Docker](https://www.docker.com/get-started)
* [Docker Compose](https://docs.docker.com/compose/install/)

**Passos para a Instalação:**

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/tioRaffa/calendar-api.git]
    ```

2.  **Configure as variáveis de ambiente:**
    * Crie uma cópia de um arquivo de exemplo `.env.example` (se houver) para `.env`.
    * Preencha o arquivo `.env` com suas chaves de API e segredos (Stripe, Firebase, PostgreSQL, Django Secret Key, etc.).

3.  **Construa e inicie os contêineres:**
    Este comando irá construir a imagem da sua aplicação e iniciar todos os serviços definidos no `docker-compose.yml` (Django, Postgres, Redis, Celery).
    ```bash
    docker-compose up --build -d ou npm run up
    ```

4.  **Execute as migrações do banco de dados:**
    Este passo cria as tabelas no seu banco de dados PostgreSQL.
    ```bash
    docker-compose exec app python manage.py migrate
    ```

5.  **Crie um superusuário (Administrador):**
    Este usuário terá acesso ao painel de administração para cadastrar os médicos.
    ```bash
    docker-compose exec app python manage.py createsuperuser
    ```

6.  **Pronto!** A aplicação estará rodando e acessível.
    * **API:** `http://localhost:8000/api/`
    * **Painel Admin:** `http://localhost:8000/admin/`

## 📋 Roadmap de Desenvolvimento

- [x] Definição da arquitetura e stack simplificada.
- [x] Estrutura de pastas e configuração do Docker.
- [ ] Implementação da autenticação de pacientes com Firebase.
- [ ] Criação dos modelos e do painel de Admin para Médicos e Horários.
- [ ] Desenvolvimento da lógica para cálculo de horários disponíveis.
- [ ] Implementação do fluxo de agendamento com pagamento via Stripe.
- [ ] Criação do sistema de notificações com Celery e WhatsApp.
- [ ] Documentação dos endpoints da API.

---

_Este README será atualizado conforme o projeto avança._