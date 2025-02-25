# Como rodar o projeto
## Pré-requisitos
Docker e Docker Compose instalados
Node.js e npm instalados para rodar o frontend sem Docker
Comandos Docker

Este guia contém os passos necessários para configurar e executar corretamente o projeto.

## Backend

### 1. Executar Docker Compose

Abra um terminal na raiz do projeto backend e rode o seguinte comando:

```bash
docker-compose up --build
```

**Nota:** Caso precise parar os containers, utilize:

```bash
docker-compose down
```

### 2. Rodar migrations

Com os containers rodando, entre no container da aplicação PHP:

```bash
docker-compose exec app bash
```

Dentro do container, execute as migrations com o comando (caso necessário):

```bash
php artisan migrate
```

### 3. Sincronizar Pokémons

Após as migrations, faça uma requisição POST para sincronizar os Pokémons. Você pode usar uma ferramenta como Postman, Insomnia, ou curl:

```bash
curl -X POST http://localhost:8000/api/admin/pokemons/sync
```

## Frontend

Abra outro terminal e navegue até o diretório do projeto frontend.

### 1. Instalar dependências

Execute o comando abaixo para instalar ou atualizar as dependências do projeto:

```bash
cd frontend
npm install
```

### 2. Rodar o projeto

Após a instalação das dependências, execute o comando:

```bash
npm run dev
```

O frontend estará disponível em http://localhost:3000.

Agora o frontend estará rodando normalmente e pronto para uso.



