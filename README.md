# Kit de Início para IA Auto-hospedada

**Self-hosted AI Starter Kit** é um modelo de Docker Compose de código aberto projetado para inicializar rapidamente um ambiente abrangente de desenvolvimento de IA e low-code local.

![n8n.io - Captura de Tela](https://raw.githubusercontent.com/n8n-io/self-hosted-ai-starter-kit/main/assets/n8n-demo.gif)

Criado por <https://github.com/n8n-io>, ele combina a plataforma n8n auto-hospedada com uma lista selecionada de produtos e componentes de IA compatíveis para começar rapidamente a criar fluxos de trabalho de IA auto-hospedados.

> [!DICA]
> [Leia o anúncio](https://blog.n8n.io/self-hosted-ai/)

### O que está incluído

✅ [**n8n auto-hospedado**](https://n8n.io/) - Plataforma low-code com mais de 400 integrações e componentes avançados de IA

✅ [**Ollama**](https://ollama.com/) - Plataforma LLM multiplataforma para instalar e executar os mais recentes modelos de linguagem locais

✅ [**Qdrant**](https://qdrant.tech/) - Armazenamento vetorial de alto desempenho com uma API abrangente

✅ [**PostgreSQL**](https://www.postgresql.org/) - O cavalo de batalha do mundo de Engenharia de Dados, lida com grandes quantidades de dados com segurança.

✅ [**Open WebUI**](https://github.com/open-webui/open-webui) - Interface web amigável para interagir com LLMs locais através do Ollama

### O que você pode construir

⭐️ **Agentes de IA** para agendamento de compromissos

⭐️ **Resumir PDFs da Empresa** com segurança sem vazamento de dados

⭐️ **Bots do Slack mais inteligentes** para melhorar as comunicações e operações de TI da empresa

⭐️ **Análise de Documentos Financeiros Privados** com custo mínimo

## Instalação

### Clonando o Repositório

```bash
git clone https://github.com/fabriciosilvasantos/self-hosted-ai-starter-kit.git
cd self-hosted-ai-starter-kit
cp .env.example .env # você deve atualizar os segredos e senhas dentro
```

### Executando n8n usando Docker Compose

#### Para usuários com GPU Nvidia

```bash
git clone https://github.com/fabriciosilvasantos/self-hosted-ai-starter-kit.git
cd self-hosted-ai-starter-kit
cp .env.example .env # você deve atualizar os segredos e senhas dentro
docker compose --profile gpu-nvidia up
```

> [!NOTA]
> Se você nunca usou sua GPU Nvidia com o Docker antes, siga as
> [instruções do Docker da Ollama](https://github.com/ollama/ollama/blob/main/docs/docker.md).

### Para usuários com GPU AMD no Linux

```bash
git clone https://github.com/fabriciosilvasantos/self-hosted-ai-starter-kit.git
cd self-hosted-ai-starter-kit
cp .env.example .env # você deve atualizar os segredos e senhas dentro
docker compose --profile gpu-amd up
```

#### Para usuários de Mac / Apple Silicon

Se você estiver usando um Mac com processador M1 ou mais recente, infelizmente não é possível expor sua GPU para a instância do Docker. Existem duas opções neste caso:

1. Execute o kit de início totalmente na CPU, como na seção "Para todos os outros" abaixo
2. Execute o Ollama no seu Mac para inferência mais rápida e conecte-se a ele a partir da instância do n8n

Se você quiser executar o Ollama no seu Mac, verifique a [página inicial do Ollama](https://ollama.com/) para obter instruções de instalação e execute o kit de início da seguinte forma:

```bash
git clone https://github.com/fabriciosilvasantos/self-hosted-ai-starter-kit.git
cd self-hosted-ai-starter-kit
cp .env.example .env # você deve atualizar os segredos e senhas dentro
docker compose up
```

##### Para usuários de Mac executando OLLAMA localmente

Se você estiver executando o OLLAMA localmente no seu Mac (não no Docker), você precisa modificar a variável de ambiente OLLAMA_HOST

1. Defina OLLAMA_HOST como `host.docker.internal:11434` no seu arquivo .env.
2. Além disso, depois de ver "Editor is now accessible via: <http://localhost:5678/>":

    1. Acesse <http://localhost:5678/home/credentials>
    2. Clique em "Local Ollama service"
    3. Altere a URL base para "http://host.docker.internal:11434/"

#### Para todos os outros

```bash
git clone https://github.com/fabriciosilvasantos/self-hosted-ai-starter-kit.git
cd self-hosted-ai-starter-kit
cp .env.example .env # você deve atualizar os segredos e senhas dentro
docker compose --profile cpu up
```

## ⚡️ Início rápido e uso

O núcleo do Self-hosted AI Starter Kit é um arquivo Docker Compose, pré-configurado com configurações de rede e armazenamento, minimizando a necessidade de instalações adicionais.
Após concluir as etapas de instalação acima, basta seguir as etapas abaixo para começar.

1. Abra <http://localhost:5678/> no seu navegador para configurar o n8n. Você só precisará fazer isso uma vez.
2. Abra o fluxo de trabalho incluído: <http://localhost:5678/workflow/srOnR8PAY3u4RSwb>
3. Clique no botão **Chat** na parte inferior da tela para começar a executar o fluxo de trabalho.
4. Se esta for a primeira vez que você executa o fluxo de trabalho, pode ser necessário aguardar até que o Ollama termine de baixar o Llama3.2. Você pode inspecionar os logs do console do docker para verificar o progresso.

Para abrir o n8n a qualquer momento, visite <http://localhost:5678/> no seu navegador.

Com sua instância do n8n, você terá acesso a mais de 400 integrações e um conjunto de nós de IA básicos e avançados, como [Agente de IA](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/), [Classificador de Texto](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.text-classifier/) e [Extrator de Informações](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.information-extractor/). Para manter tudo local, lembre-se de usar o nó Ollama para seu modelo de linguagem e Qdrant como seu armazenamento vetorial.

> [!NOTA]
> Este kit de início foi projetado para ajudá-lo a começar com fluxos de trabalho de IA auto-hospedados. Embora não seja totalmente otimizado para ambientes de produção, ele combina componentes robustos que funcionam bem juntos para projetos de prova de conceito. Você pode personalizá-lo para atender às suas necessidades específicas.

## Atualização

* ### Para configurações com GPU Nvidia:

```bash
docker compose --profile gpu-nvidia pull
docker compose create && docker compose --profile gpu-nvidia up
```

* ### Para usuários de Mac / Apple Silicon

```bash
docker compose pull
docker compose create && docker compose up
```

* ### Para configurações sem GPU:

```bash
docker compose --profile cpu pull
docker compose create && docker compose --profile cpu up
```

## 👓 Leitura recomendada

O n8n está repleto de conteúdo útil para começar rapidamente com seus conceitos e nós de IA. Se você encontrar algum problema, vá para [suporte](#suporte).

- [Agentes de IA para desenvolvedores: da teoria à prática com n8n](https://blog.n8n.io/ai-agents/)
- [Tutorial: Crie um fluxo de trabalho de IA no n8n](https://docs.n8n.io/advanced-ai/intro-tutorial/)
- [Conceitos de Langchain no n8n](https://docs.n8n.io/advanced-ai/langchain/langchain-n8n/)
- [Demonstração das principais diferenças entre agentes e cadeias](https://docs.n8n.io/advanced-ai/examples/agent-chain-comparison/)
- [O que são bancos de dados vetoriais?](https://docs.n8n.io/advanced-ai/examples/understand-vector-databases/)

## 🎥 Demonstração em vídeo

- [Instalando e usando IA Local para n8n](https://www.youtube.com/watch?v=xz_X2N-hPg0)

## 🛍️ Mais modelos de IA

Para mais ideias de fluxos de trabalho de IA, visite a [galeria oficial de modelos de IA do n8n](https://n8n.io/workflows/categories/ai/). Em cada fluxo de trabalho, selecione o botão **Usar fluxo de trabalho** para importar automaticamente o fluxo de trabalho para sua instância local do n8n.

### Modelos de IA local

- [Assistente de Código Tributário](https://n8n.io/workflows/2341-build-a-tax-code-assistant-with-qdrant-mistralai-and-openai/)
- [Dividir Documentos em Notas de Estudo com MistralAI e Qdrant](https://n8n.io/workflows/2339-breakdown-documents-into-study-notes-using-templating-mistralai-and-qdrant/)
- [Assistente de Documentos Financeiros usando Qdrant e Mistral.ai](https://n8n.io/workflows/2335-build-a-financial-documents-assistant-using-qdrant-and-mistralai/)
- [Recomendações de Receitas com Qdrant e Mistral](https://n8n.io/workflows/2333-recipe-recommendations-with-qdrant-and-mistral/)

## Dicas e truques

### Acessando arquivos locais

O kit de início de IA auto-hospedada criará uma pasta compartilhada (por padrão, localizada no mesmo diretório) que é montada no contêiner n8n e permite que o n8n acesse arquivos em disco. Esta pasta dentro do contêiner n8n está localizada em `/data/shared` - este é o caminho que você precisará usar em nós que interagem com o sistema de arquivos local.

**Nós que interagem com o sistema de arquivos local**

- [Ler/Escrever Arquivos do Disco](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.filesreadwrite/)
- [Gatilho de Arquivo Local](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.localfiletrigger/)
- [Executar Comando](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.executecommand/)

## 📜 Licença

Este projeto está licenciado sob a Licença Apache 2.0 - consulte o arquivo [LICENSE](LICENSE) para obter detalhes.

## 💬 Suporte

Participe da conversa no [Fórum do n8n](https://community.n8n.io/), onde você pode:

- **Compartilhar Seu Trabalho**: Mostre o que você construiu com o n8n e inspire outras pessoas na comunidade.
- **Fazer Perguntas**: Seja você um iniciante ou um profissional experiente, a comunidade e nossa equipe estão prontas para ajudar com quaisquer desafios.
- **Propor Ideias**: Tem uma ideia para um recurso ou melhoria? Conte para nós! Estamos sempre ansiosos para ouvir o que você gostaria de ver em seguida.
