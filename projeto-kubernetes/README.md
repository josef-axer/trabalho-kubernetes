# Jogo de Adivinhação de Palavras

Um jogo de adivinhação de palavras baseado na web, desenvolvido com frontend em React e backend em Flask, implantável via Docker ou Kubernetes.

## Visão Geral

O Jogo de Adivinhação de Palavras é um jogo multiplayer onde:
- Um jogador (Criador) cria um jogo com uma palavra secreta
- Outros jogadores (Adivinhadores) tentam adivinhar a palavra
- O jogo fornece feedback para cada tentativa, indicando letras corretas em posições certas e erradas

## Stack Tecnológico

- **Frontend:**
  - React
  - TypeScript
  - Jest para testes
  - Docker para containerização

- **Backend:**
  - Flask (Python)
  - Suporte a múltiplos bancos de dados:
    - PostgreSQL (padrão)
    - DynamoDB
    - SQLite
  - OpenTelemetry para instrumentação

- **Infraestrutura:**
  - Docker Compose para desenvolvimento local
  - Kubernetes para implantação em produção
  - Nginx como proxy reverso

## Primeiros Passos

### Pré-requisitos

- Docker e Docker Compose
- Node.js (para desenvolvimento local)
- Python 3.8+ (para desenvolvimento local)

### Desenvolvimento Local com Docker Compose

1. Clone o repositório:
```bash
git clone <repository-url>
cd guess-word-game
```

2. Inicie a aplicação:
```bash
docker-compose up --build
```

A aplicação estará disponível em `http://localhost`.

### Desenvolvimento Local sem Docker

1. Inicie o backend:
```bash
pip install -r requirements-dev.txt
export FLASK_APP=run.py
export FLASK_DB_TYPE=postgres/dynamodb
flask run
```

2. Inicie o frontend:
```bash
cd frontend
npm install
npm start
```

## Implantação com Kubernetes

1. Aplique os ConfigMaps:
```bash
kubectl apply -f configmaps.yaml
```

2. Implante o banco de dados:
```bash
kubectl apply -f postgres-deployment.yaml
```

3. Implante os componentes da aplicação:
```bash
kubectl apply -f frontend-deployment.yaml
kubectl apply -f guess-deployment.yaml
kubectl apply -f nginx-deployment.yaml
```

## Testes

### Testes do Frontend
```bash
cd frontend
npm test
```

### Testes do Backend
```bash
pip install -r requirements-dev.txt
pytest
```

## Estrutura do Projeto

```
.
├── frontend/                # Aplicação frontend em React
├── guess/                   # Aplicação backend em Flask
├── repository/              # Camada de abstração do banco de dados
├── tests/                   # Testes do backend
├── kubernetes/              # Arquivos de implantação no Kubernetes
└── docker-compose.yml       # Configuração do Docker Compose
```

## Endpoints da API

### POST /create
Cria um novo jogo com uma palavra secreta.
- Corpo da requisição: `{ "password": "palavra-secreta" }`
- Resposta: `{ "game_id": "id-unico" }`

### POST /guess/{game_id}
Faz uma tentativa de adivinhação para um jogo específico.
- Corpo da requisição: `{ "guess": "palavra-tentativa" }`
- Resposta: `{ "result": "mensagem-de-feedback" }`

## Contribuindo

1. Faça um fork do repositório
2. Crie sua branch de feature (`git checkout -b feature/nova-feature`)
3. Commit suas alterações (`git commit -m 'Adiciona uma nova feature incrível'`)
4. Envie para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## Licença

Este projeto é licenciado sob a Licença MIT - veja o arquivo LICENSE para mais detalhes.