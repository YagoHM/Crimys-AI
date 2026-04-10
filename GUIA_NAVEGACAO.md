# CRIMYS
# Guia de Navegacao do Projeto

Versao: 1.0
Criado por: yagohmz
Raiz do projeto: C:\Users\yagohmz\Desktop\The Vault\Crimys

Este arquivo fica fora do projeto como referencia rapida.
Para documentacao completa, consulte: Crimys\core\CRIMYS_FULL.md

---

## O que e o Crimys

Assistente de IA local e autonomo que opera como side assistant do Claude Code
e controlador do computador. Roda inteiramente na maquina, sem dependencia de
nuvem. Aprende continuamente com o uso via memoria vetorial.

Tres funcoes principais:
- Side assistant do Claude Code: responde consultas de documentacao e erros via MCP,
  economizando tokens de outras IAs que nao precisam buscar na internet
- Controlador do computador: executa macros, gerencia processos, automatiza tarefas
- Assistente pessoal evolutivo: aprende padroes, melhora com o uso, conhece seus projetos

---

## Mapa de pastas

```
The Vault\
|
|-- Crimys\                        PROJETO PRINCIPAL
|   |
|   |-- app\                       Fork do OpenCode (interface do terminal)
|   |-- mcp\                       Servidores MCP em Python
|   |   |-- pc_server.py           Controle do computador
|   |   |-- monitor_server.py      Monitoramento em background
|   |   |-- vault_server.py        RAG e memoria
|   |   `-- requirements.txt       Dependencias Python
|   |
|   |-- chromadb\                  Banco vetorial (gerado automaticamente)
|   |
|   |-- core\                      Identidade e prompts da IA
|   |   |-- CRIMYS_FULL.md         Documento completo do projeto
|   |   |-- system_prompt.md       Personalidade e comportamento
|   |   |-- reasoning_prompt.md    Como a IA pensa antes de agir
|   |   |-- memory_prompt.md       Como a IA aprende e memoriza
|   |   |-- identity.md            Quem e o Crimys
|   |   `-- boundaries.md          O que ele nunca faz
|   |
|   |-- docs\                      Documentacao das ferramentas
|   |   |-- libs\                  n8n, Evolution, ChromaDB, MCP, etc
|   |   |-- languages\             Python, PHP/Laravel, JavaScript
|   |   |-- infra\                 Docker, Linux, Windows
|   |   `-- tools\                 Obsidian, Git, etc
|   |
|   |-- automations\               Tudo que o Crimys executa
|   |   |-- macros\                Sequencias de acoes predefinidas
|   |   |-- triggers\              Eventos que disparam acoes automaticas
|   |   `-- routines\              Rotinas agendadas por horario
|   |
|   |-- memory\                    Memoria evolutiva (machine learning)
|   |   |-- interactions\          Historico de interacoes uteis indexadas
|   |   |-- learned\               Padroes promovidos e confirmados
|   |   `-- feedback\              Anti-padroes registrados
|   |
|   |-- logs_pc\                   Registros do monitor
|   |   |-- errors\                Erros capturados com contexto
|   |   |-- processes\             Historico de processos problematicos
|   |   `-- corrections\           Correcoes aplicadas e como foram feitas
|   |
|   |-- config\                    Configuracoes e integracoes
|   |   |-- models.md              Modelos disponiveis e modelo ativo
|   |   `-- integrations.md        Conexoes externas configuradas
|   |
|   |-- opencode.json              Configuracao do fork (agentes, MCP, provider)
|   `-- .gitignore                 Arquivos ignorados pelo git
|
|-- projects\                      SEUS PROJETOS (contexto externo)
    |-- antigravity\
    |-- evolution_project\
    `-- [outros projetos]\
```

Arquivo de configuracao global: C:\Users\yagohmz\.crimys

---

## Onde encontrar cada coisa

| O que voce quer fazer                     | Onde                                  |
|-------------------------------------------|---------------------------------------|
| Mudar personalidade da IA                 | core\system_prompt.md                 |
| Mudar como a IA raciocina                 | core\reasoning_prompt.md              |
| Mudar como a IA aprende                   | core\memory_prompt.md                 |
| Ver ou criar macros                       | automations\macros\                   |
| Ver erros capturados pelo monitor         | logs_pc\errors\                       |
| Ver correcoes aplicadas                   | logs_pc\corrections\                  |
| Ver o que a IA aprendeu                   | memory\learned\                       |
| Ver historico de interacoes               | memory\interactions\                  |
| Adicionar documentacao de uma lib         | docs\libs\[nome_da_lib]\              |
| Mudar o modelo de IA                      | config\models.md + .crimys            |
| Editar os servidores MCP                  | mcp\                                  |
| Editar a interface do terminal            | app\                                  |
| Adicionar contexto de um projeto          | projects\[nome_do_projeto]\           |
| Documento completo do projeto             | core\CRIMYS_FULL.md                   |
| Configuracao global de permissoes         | C:\Users\yagohmz\.crimys              |
| Configuracao dos agentes e MCP            | opencode.json                         |

---

## Comandos do terminal

    crimys                       Inicia em modo interativo
    crimys monitor               Ativa monitoramento em background
    crimys monitor --status      Status atual do monitor
    crimys monitor --stop        Para o monitoramento
    crimys logs                  Resume erros acumulados
    crimys logs --week           Erros da ultima semana
    crimys logs --fix            Inicia ciclo de correcao automatica
    crimys config                Abre o arquivo .crimys
    crimys model                 Seletor interativo de modelo
    crimys model --set groq      Troca para Groq
    crimys model --set local     Volta para o modelo local
    crimys serve                 Sobe como servidor HTTP com API
    crimys docs --index          Reindexar documentacoes no ChromaDB
    crimys -p "prompt"           Executa prompt direto sem abrir interface

---

## Modelos disponiveis

    Padrao sempre: Ollama local (nunca troca automaticamente)

    ollama / qwen2.5-coder:7b    Padrao. Cabe nos 4GB de VRAM.
    groq  / llama-3.3-70b        Gratis com limite. Mais capaz. Requer internet.
    anthropic / claude-sonnet    Pago por uso. Maxima qualidade.
    openai / gpt-4o              Pago por uso. Alternativa ao Anthropic.

    Para trocar: crimys model --set [provider]

---

## Como adicionar documentacao de uma nova lib

    1. Crie a pasta:  Crimys\docs\libs\[nome_da_lib]\
    2. Adicione os arquivos .md com o conteudo da documentacao
    3. Execute:       crimys docs --index
    4. Pronto. A IA ja tem acesso via busca semantica.

---

## Como criar uma nova macro

Via conversa:
    "Crie uma macro chamada [nome] que faz [descricao]"
    O Crimys cria o arquivo automaticamente em automations\macros\

Manualmente, crie um arquivo .md em automations\macros\:

    # Macro: Nome da Macro
    Descricao: O que ela faz
    Criada em: YYYY-MM-DD

    ## Passos
    1. Primeiro passo
    2. Segundo passo
    3. Terceiro passo

---

## Como reverter um aprendizado incorreto

A Vault e versionada com git. Para desfazer:

    cd "C:\Users\yagohmz\Desktop\The Vault\Crimys"
    git log --oneline
    git revert [hash do commit]

Para ver apenas o que mudou na memoria:

    git log --oneline -- memory\

---

## Instalacao das dependencias Python

Rodar uma vez apos clonar ou configurar o projeto:

    pip install -r "C:\Users\yagohmz\Desktop\The Vault\Crimys\mcp\requirements.txt"

Dependencias: mcp, psutil, pyautogui, chromadb, mem0ai, watchdog

---

## Inicializacao do git

    cd "C:\Users\yagohmz\Desktop\The Vault\Crimys"
    git init
    git add .
    git commit -m "crimys: estrutura inicial"

    Para conectar ao GitHub:
    git remote add origin https://github.com/[usuario]/crimys
    git push -u origin main

---

## Roadmap de implementacao

    Fase 1   Instalar Ollama e baixar qwen2.5-coder:7b
    Fase 2   Instalar OpenCode e testar com Ollama local
    Fase 3   Fork do OpenCode, renomear para Crimys, ajustar cores
    Fase 4   Preencher os prompts em core\ com o conteudo do CRIMYS_FULL.md
    Fase 5   Instalar dependencias Python e testar os MCP servers
    Fase 6   Criar macros iniciais e testar controle do PC
    Fase 7   Ativar monitor e testar ciclo de correcao
    Fase 8   Adicionar documentacoes em docs\libs\ e indexar
    Fase 9   Configurar memoria e testar ciclo de aprendizado
    Fase 10  Publicar no GitHub como crimys-ai

---

Documento mantido manualmente. Atualizar apos mudancas estruturais no projeto.
