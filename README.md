# CRIMYS

> Assistente de IA local, autonomo e evolutivo.
> Roda na sua maquina. Aprende com o uso. Controla tudo.

---

## O que e

Crimys e um assistente de IA construido sobre um fork do [OpenCode](https://github.com/anomalyco/opencode),
adaptado para ser um sistema autonomo de controle de computador e base de conhecimento centralizada.

O projeto tem trÊes funções que operam em conjunto:

**Side assistant de Terminal IA no Visual Code**
Quando o Claude Code ou qualquer outra IA precisa de documentacao ou precisa resolver um erro,
ela consulta o Crimys via MCP. O Crimys ja tem tudo indexado localmente e responde sem gastar
tokens buscando na internet. As IAs param de procurar e comecam a perguntar.

**Controlador autonomo do computador**
Acesso total ao Windows. Executa macros, abre programas, gerencia processos, monitora o sistema
em background e corrige erros acumulados quando solicitado. Modo full-auto para correcoes.

**Assistente pessoal evolutivo**
Aprende continuamente via memoria vetorial. Cada interacao util vira contexto futuro.
Padroes identificados sao promovidos automaticamente. Sem fine-tuning, sem custo adicional.

---

## Stack

| Camada          | Tecnologia               |
|-----------------|--------------------------|
| Interface       | OpenCode fork (Bubble Tea / TUI) |
| Modelo local    | Ollama + qwen3.5-coder |
| RAG             | ChromaDB + busca semantica |
| Memoria         | Mem0 + arquivos Markdown  |
| Controle do PC  | pyautogui + psutil        |
| Monitoramento   | psutil + watchdog         |
| Protocolo       | MCP (Model Context Protocol) |
| Base de dados   | Obsidian Vault (Markdown) |

---

## Estrutura

```
Crimys/
|-- app/              fork do OpenCode
|-- mcp/              servidores MCP (Python)
|-- chromadb/         banco vetorial local
|-- core/             identidade e prompts da IA
|-- docs/             documentacao das bibliotecas
|-- automations/      macros, triggers e rotinas
|-- memory/           memoria evolutiva
|-- logs_pc/          registros do monitor
`-- config/           configuracoes e integracoes
```

## Modelos

O modelo padrao é sempre local. A troca é sempre manual, nunca automática.

```
Padrao   ollama / qwen2.5-coder:7b   gratis, local, 4GB VRAM
Manual   groq / llama-3.3-70b        gratis com limite, requer internet
Manual   anthropic / claude-sonnet   pago por uso
Manual   openai / gpt-4o             pago por uso
```

# Planejamento:
Para trocar: `crimys model --set [provider]`

---

## Instalacao

```powershell
# 1. Instalar Ollama
# Baixar em: https://ollama.com/download

# 2. Baixar o modelo, por ex:
ollama pull qwen2.5-coder:7b

# 3. Instalar OpenCode
npm i -g opencode-ai@latest

# 4. Instalar dependencias Python
pip install -r mcp\requirements.txt

# 5. Iniciar
crimys
```

---

## Comandos principais

```
crimys                    inicia em modo interativo
crimys monitor            ativa monitoramento em background
crimys monitor --status   status do monitor
crimys logs --fix         correcao automatica de erros acumulados
crimys docs --index       indexa documentacoes no ChromaDB
crimys model              troca o modelo de IA
```

---

## Como o aprendizado funciona

O Crimys nao usa fine-tuning. O aprendizado e baseado em memoria vetorial:

```
interacao util
      |
      v
memory/interactions/     indexado no ChromaDB
      |
      | (3+ ocorrencias do mesmo padrao)
      v
memory/learned/          promovido como padrao confirmado
      |
      | (padrao e uma sequencia de acoes)
      v
automations/macros/      vira macro executavel
```

Feedback negativo vai para `memory/feedback/` como anti-padrao a evitar.
A Vault e versionada com git, entao qualquer aprendizado incorreto pode ser revertido.

---

## Permissoes

Configuradas no arquivo `.crimys` em `C:\Users\yagohmz\.crimys`.

Por padrao, o Crimys pode ler e escrever arquivos, executar comandos,
abrir e fechar aplicativos e controlar mouse e teclado.

Acoes que sempre requerem confirmacao explicita, independente do modo de autonomia:
deletar arquivos permanentemente, encerrar processos do sistema operacional,
modificar o registro do Windows e instalar software.

---

## Nome

**Crimys** = Crimson (vermelho profundo) + Nemys (time de Valorant do criador).
Cores do projeto: `#DC2626` vermelho e `#7C3AED` roxo.

---

## Licenca

Baseado no [OpenCode](https://github.com/anomalyco/opencode) sob licenca MIT.
Este fork e distribuido sob os mesmos termos.

---

*Para navegacao detalhada do projeto, consulte GUIA_NAVEGACAO.md.*
*Para arquitetura completa e decisoes de projeto, consulte core\CRIMYS_FULL.md.*
