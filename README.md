# 📄 Guia Completo: Setup de Automação (Robot Framework + Python) & Fluxo Git

Este documento é um guia passo a passo unificado para configurar do zero um ambiente profissional de automação de testes em Linux (Ubuntu) e executar o fluxo completo de Git para publicar o projeto no GitHub.


## 🛠️ Parte 1: Instalação e Configuração do Ambiente

Execute os comandos abaixo no seu terminal para preparar o sistema e isolar as dependências do projeto utilizando um Ambiente Virtual (`venv`), evitando conflitos com o Python nativo do Ubuntu (PEP 668).

### 1. Atualizar o sistema e instalar o suporte completo ao Python 3:

```bash

sudo apt update && sudo apt install python3-full -y

2. Criar o Ambiente Virtual (.venv) na raiz do projeto:

'''bash

python3 -m venv .venv

3. Ativar o Ambiente Virtual:

'''bash

source .venv/bin/activate

(Repare que o prefixo (.venv) aparecerá no início da linha de comandos do seu terminal, indicando que o ambiente está ativo).

4. Atualizar o pip e instalar o Robot Framework e as bibliotecas Web/API:

''''bash

pip install --upgrade pip
pip install robotframework
pip install robotframework-seleniumlibrary
pip install robotframework-requests

5. Validar se a instalação foi concluída com sucesso:

''''bash

robot --version

📂 Parte 2: Estrutura Arquitetural do Projeto

Para garantir a organização dos testes para o ecossistema SAP S/4HANA (Fiori/Web e APIs), utilize a seguinte estrutura de pastas na raiz do projeto:

web_tests/ — Destinado aos scripts de automação de interface gráfica (ex: portais SAP Fiori).

api_tests/ — Destinado aos scripts de validação de endpoints e integrações de sistemas (SIT).

massa_dados/ - Armazenamento de payloads JSON, configurações ou scripts SQL de validação.

🚀 Parte 3: O Fluxo de Git em 7 Passos Práticos

Certifique-se de que o seu terminal está aberto na pasta principal do projeto (Projeto_Sipal) e execute os passos na ordem exata abaixo:

Passo 1: Criar o ficheiro .gitignore

Este passo é obrigatório para impedir que a pasta .venv (que contém os binários pesados do Python) seja enviada para o GitHub.

''''bash

echo ".venv/" > .gitignore

Passo 2: Inicializar o repositório Git local

''''bash

**git init**

Passo 3: Adicionar os ficheiros ao "palco" de envio (Stage)

''''bash

git add README.md .gitignore

Passo 4: Criar o primeiro Commit

Grava o estado atual do código com uma mensagem descritiva.

''''bash

git commit -m "chore: setup inicial do ambiente de automação e estrutura de pastas"

Passo 5: Criar e mudar para uma nova Branch de trabalho

Seguindo as boas práticas do mercado (Git Flow), isolamos o desenvolvimento criando uma ramificação:

''''bash

git checkout -b feature/estrutura-testes

Passo 6: Vincular o computador local ao repositório do GitHub

Aceda ao GitHub e crie um novo repositório chamado sap-robot-automation-setup como Public (Público).

Deixe todas as caixas de seleção iniciais (README, .gitignore) desmarcadas.

Copie a linha de comando de vínculo gerada pelo GitHub e execute-a no seu terminal:

Bash

git remote add origin [https://github.com/SEU_USUARIO/sap-robot-automation-setup.git](https://github.com/SEU_USUARIO/sap-robot-automation-setup.git)

Passo 7: Enviar a branch para o servidor remoto (Push!)

''''bash
git push -u origin feature/estrutura-testes

💡 Dica de QA: Sempre que fechar o terminal e voltar a estudar no dia seguinte, lembre-se de reativar o ambiente virtual na pasta do projeto executando o comando do Passo 3 da Parte 1: source .venv/bin/activate.

------------------------------------------------------------------------------------------------------------------------------

# SAP Robot Automation Setup - Guia do Ambiente

Este repositório contém a infraestrutura inicial e o histórico de configuração para o ambiente de automação de testes SAP e Web utilizando o Robot Framework.

---

## 1. Estrutura Inicial do Repositório

O projeto foi iniciado com a seguinte organização de arquivos fundamentais:

* `.gitignore`: Configurado para omitir arquivos de log do Robot Framework (`log.html`, `report.html`, `output.xml`) e pastas virtuais do Python (`.venv/`).
* `README.md`: Documentação principal de controle de versão e setup.

---

## 2. Histórico de Comandos e Configuração do Git

Abaixo está o registro dos comandos executados para inicialização do repositório local, correção de rotas remotas e sincronização com o GitHub via HTTPS utilizando autenticação segura por token (PAT):

| Comando Executado | Objetivo e Descrição Técnica |
| :--- | :--- |
| `git config --global user.email "..."`<br>`git config --global user.name "..."` | Identificação global do autor no ambiente Git local para permitir a assinatura de commits. |
| `git commit -m "chore: setup inicial..."` | Geração do primeiro ponto de salvamento oficial (root-commit) na branch principal. |
| `git checkout -b feature/estrutura-testes` | Criação e alternância para a branch dedicada ao desenvolvimento da estrutura de testes, seguindo as boas práticas do Git Flow. |
| `git remote remove origin` | Remoção de referências remotas incorretas (links genéricos salvos por engano). |
| `git remote add origin https://github.com/...` | Vinculação definitiva do repositório local ao endereço correto do repositório remoto no GitHub via HTTPS. |
| `git remote -v` | Validação e checagem detalhada (verbose) das URLs de *fetch* e *push* configuradas. |
| `git push -u origin feature/estrutura-testes` | Envio da branch de trabalho local e seus respectivos commits para o servidor remoto do GitHub. |

---

## 3. Fluxo de Autenticação Segura (GitHub PAT)

Devido à descontinuação da autenticação por senhas comuns via terminal no GitHub, o acesso foi estabelecido através de um **Personal Access Token (Classic)**:

1. Navegação até a seção interna de segurança em *Developer Settings > Personal Access Tokens > Tokens (classic)*.
2. Criação de token dedicado com escopo restrito ao escopo `repo` (controle total de repositórios privados e públicos).
3. Utilização do hash criptográfico gerado no campo `Password` diretamente no fluxo de autenticação do terminal Linux.

---

## 4. Próximos Passos do Projeto

* Construção dos arquivos de teste estruturados (`.robot`) na pasta correspondente.
* Mapeamento das Keywords e Variáveis de ambiente para o fluxo SAP/Web.