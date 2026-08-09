# Pacote Gemini Reviewer

Este pacote contém os componentes principais do **Gemini AI Code Reviewer**, estruturados de forma modular para organizar o fluxo de revisão automática de código.

## Estrutura do Pacote

```text
gemini_reviewer/
├── __init__.py       # Inicialização e exportação do pacote
├── models.py         # Estruturas de dados e modelos
├── config.py         # Gerenciamento de configurações
├── github_client.py  # Cliente de integração com a API do GitHub
├── gemini_client.py  # Cliente de integração com a IA do Gemini
├── diff_parser.py    # Lógica de processamento de alterações (Git diff)
└── code_reviewer.py  # Classe principal que orquestra o sistema
```

## Visão Geral dos Módulos

- **`models.py`**: Contém as estruturas de dados usadas na aplicação, como detalhes do Pull Request (PR), formato dos comentários e resultados da revisão.
- **`config.py`**: Centraliza as configurações do sistema. Permite carregar dados de variáveis de ambiente e definir o rigor da revisão (estrito, padrão, etc.).
- **`github_client.py`**: Gerencia a comunicação com o GitHub. É responsável por buscar as alterações de código e publicar os comentários no repositório.
- **`gemini_client.py`**: Lida com a integração da IA. Envia o código modificado para o Gemini e estrutura os prompts para obter as melhores sugestões.
- **`diff_parser.py`**: Analisa os arquivos modificados. Ele filtra o que precisa ser revisado, identifica a complexidade das mudanças e ignora arquivos binários.
- **`code_reviewer.py`**: É o orquestrador do sistema. Ele conecta todos os módulos acima para executar o fluxo completo de revisão de ponta a ponta.

## Como Usar

A interação com o pacote é feita de forma simples através da classe principal `CodeReviewer`:

```python
from gemini_reviewer import Config, CodeReviewer

# 1. Carrega as configurações do ambiente
config = Config.from_environment()

# 2. Instancia e executa o revisor de código
with CodeReviewer(config) as reviewer:
    result = await reviewer.review_pull_request(event_path)
```

## Princípios de Arquitetura

Para garantir a qualidade do software, o pacote foi desenvolvido com base nos seguintes princípios:

1. **Modularidade**: Cada módulo possui uma responsabilidade única e bem definida.
2. **Testabilidade**: Os componentes são independentes, facilitando a criação de testes isolados.
3. **Configuração Flexível**: Adaptável a diferentes ambientes sem necessidade de alterar o código-fonte.
4. **Tratamento de Erros**: Previne falhas inesperadas e mantém a estabilidade do fluxo.
5. **Desempenho**: Utiliza processamento concorrente para agilizar o tempo de resposta das revisões.