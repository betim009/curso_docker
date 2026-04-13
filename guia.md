# Passo 1 — Teste inicial do Docker

Abra o terminal do Mac e rode:

```bash
docker --version
```

Depois rode:

```bash
docker compose version
```

Para confirmar que o Docker está funcionando:

```bash
docker run hello-world
```

### Resultado esperado

- Baixa uma imagem automaticamente
- Cria um container
- Executa
- Mostra:

```bash
Hello from Docker!
```

Isso confirma:
- Docker instalado ✅
- Download de imagens funcionando ✅
- Containers funcionando ✅

---

# Passo 2 — Entender o fluxo básico

O Docker funciona assim:

```bash
docker pull nome-da-imagem
docker run opções nome-da-imagem
```

- `pull` → baixa a imagem
- `run` → cria e executa o container

---

# Passo 3 — Baixar uma imagem (Ubuntu)

```bash
docker pull ubuntu:24.04
```

Verificar:

```bash
docker images
```

Saída esperada:

```bash
REPOSITORY   TAG     IMAGE ID     SIZE
ubuntu       24.04   xxxxxxxx     xxxMB
```

---

# Passo 4 — Entrar no container Ubuntu

```bash
docker run -it --name meu-ubuntu ubuntu:24.04 bash
```

Você verá:

```bash
root@abc123:/#
```

Teste:

```bash
ls
pwd
echo "funcionando docker"
apt update
```

---

# Passo 5 — Sair do container

```bash
exit
```

Depois:

```bash
docker ps -a
```

---

# Passo 6 — Ligar container novamente

```bash
docker start meu-ubuntu
```

---

# Passo 7 — Entrar novamente

```bash
docker exec -it meu-ubuntu bash
```

---

# Passo 8 — Conectar com VS Code

1. `Shift + Command + P`
2. Digite:

```
Dev Containers: Attach to Running Container...
```

3. Selecione `meu-ubuntu`

Teste no terminal do VS Code:

```bash
pwd
ls
```

---

# Passo 9 — Baixar imagem Node

```bash
docker pull node:22
```

```bash
docker images
```

---

# Passo 10 — Rodar Node no Docker

```bash
docker run -it --name meu-node node:22 bash
```

Teste:

```bash
node -v
npm -v
```

Saída esperada:

```bash
v22.x.x
```
# Guia Docker no Mac — Passo a Passo Detalhado

Este guia foi escrito pensando em quem está começando do zero no Docker usando Mac, VS Code e Node.js.

A ideia aqui é seguir uma ordem simples:

1. testar se o Docker está instalado corretamente
2. baixar uma imagem Linux
3. criar e executar um container
4. entender como sair e voltar para o container
5. usar o VS Code junto com Docker
6. rodar Node.js dentro de um container
7. usar volume para manter os arquivos no Mac

---

# Passo 1 — Testar se o Docker está instalado corretamente

Abra o terminal do Mac e rode:

```bash
docker --version
```

## O que esse comando faz

Esse comando mostra a versão do Docker instalada no seu computador.

## O que você deve esperar

A saída normalmente será parecida com isso:

```bash
Docker version 28.x.x, build xxxxxxx
```

Se aparecer a versão, isso já indica que o comando `docker` está disponível no seu sistema.

Agora rode também:

```bash
docker compose version
```

## O que esse comando faz

Esse comando mostra a versão do Docker Compose, que hoje já vem junto com o Docker Desktop.

## Saída esperada

Algo parecido com:

```bash
Docker Compose version v2.x.x
```

Agora faça o teste mais importante:

```bash
docker run hello-world
```

## O que esse comando faz

Esse comando testa o fluxo real do Docker:

- baixa uma imagem automática, se ela ainda não existir no seu computador
- cria um container
- executa esse container
- mostra uma mensagem final de confirmação

## Resultado esperado

A saída deve conter algo parecido com:

```bash
Hello from Docker!
```

## O que isso confirma

Se esse teste funcionar, significa que:

- Docker está instalado corretamente ✅
- Docker consegue baixar imagens ✅
- Docker consegue criar e executar containers ✅

---

# Passo 2 — Entender o fluxo básico do Docker

Antes de continuar, você precisa guardar esta ideia:

```bash
docker pull nome-da-imagem
docker run opções nome-da-imagem
```

## Significado

### `docker pull`

Baixa uma imagem para a sua máquina.

### `docker run`

Cria e executa um container com base na imagem escolhida.

## Regra simples para decorar

- **imagem** = modelo pronto
- **container** = imagem em execução

Exemplo:

- imagem: `ubuntu:24.04`
- container: uma instância rodando desse Ubuntu

---

# Passo 3 — Baixar uma imagem Linux (Ubuntu)

Agora vamos baixar uma imagem de verdade para praticar.

Rode:

```bash
docker pull ubuntu:24.04
```

## O que esse comando faz

- baixa a imagem oficial do Ubuntu
- salva a imagem localmente no seu Docker
- permite reutilizar essa imagem depois sem precisar baixar novamente

Depois verifique as imagens existentes:

```bash
docker images
```

## Saída esperada

Algo parecido com:

```bash
REPOSITORY   TAG     IMAGE ID     SIZE
ubuntu       24.04   xxxxxxxx     xxxMB
```

## O que isso significa

- `REPOSITORY` → nome da imagem
- `TAG` → versão da imagem
- `IMAGE ID` → identificador interno
- `SIZE` → tamanho da imagem

---

# Passo 4 — Entrar em um container Ubuntu

Agora vamos criar um container baseado nessa imagem e abrir um terminal dentro dele.

Rode:

```bash
docker run -it --name meu-ubuntu ubuntu:24.04 bash
```

## O que cada parte faz

### `docker run`
Cria e executa um container novo.

### `-it`
Abre o container em modo interativo, permitindo usar o terminal.

### `--name meu-ubuntu`
Define o nome do container como `meu-ubuntu`.

### `ubuntu:24.04`
Indica qual imagem será usada.

### `bash`
Abre o terminal Bash dentro do container.

## Resultado esperado

Você verá algo parecido com:

```bash
root@abc123:/#
```

Isso significa que você entrou no terminal do Linux que está rodando dentro do container.

## Faça alguns testes

```bash
ls
pwd
echo "funcionando docker"
apt update
```

## O que esses testes mostram

- `ls` → lista arquivos e pastas
- `pwd` → mostra a pasta atual
- `echo` → imprime um texto
- `apt update` → atualiza os índices de pacotes do Ubuntu

---

# Passo 5 — Sair do container sem apagar nada

Quando quiser sair do container, rode:

```bash
exit
```

## O que acontece quando você usa `exit`

- você sai do terminal do container
- o container para de rodar
- a imagem continua salva
- o container continua existindo

Agora confira isso com:

```bash
docker ps -a
```

## O que esse comando faz

Lista todos os containers, inclusive os que já foram encerrados.

## O que você deve observar

Você deve ver o container `meu-ubuntu` com status parecido com:

```bash
Exited (0)
```

Isso quer dizer que ele existe, mas está parado.

---

# Passo 6 — Ligar o container novamente

Para religar o container parado:

```bash
docker start meu-ubuntu
```

## O que esse comando faz

Ele apenas liga o container novamente.

⚠️ Importante: esse comando não entra no terminal. Ele só faz o container voltar a rodar.

---

# Passo 7 — Entrar novamente no container

Agora que ele está rodando, entre de novo com:

```bash
docker exec -it meu-ubuntu bash
```

## O que esse comando faz

- `exec` executa um comando em um container que já existe e já está rodando
- `-it` abre de forma interativa
- `bash` abre o terminal do container

## Regra prática para decorar

Quando o container já existe:

1. `docker start nome-do-container`
2. `docker exec -it nome-do-container bash`

Esse é um dos fluxos mais comuns no dia a dia.

---

# Passo 8 — Conectar esse container ao VS Code

Agora vamos usar o VS Code junto com Docker.

## Pré-requisito

Tenha a extensão **Dev Containers** instalada no VS Code.

## Como conectar

1. deixe o container rodando
2. abra o VS Code
3. pressione:

```text
Shift + Command + P
```

4. digite:

```text
Dev Containers: Attach to Running Container...
```

5. selecione o container `meu-ubuntu`

## O que acontece depois

O VS Code abre uma nova janela conectada diretamente ao container.

Isso significa que o terminal dessa nova janela estará executando comandos dentro do container.

## Teste dentro do terminal do VS Code

```bash
pwd
ls
```

Se funcionar, significa que o VS Code conseguiu se conectar ao container corretamente.

---

# Passo 9 — Baixar a imagem oficial do Node

Agora vamos sair do Ubuntu e trabalhar com uma imagem própria para Node.js.

No terminal do Mac, rode:

```bash
docker pull node:22
```

Depois confira:

```bash
docker images
```

## O que isso faz

Baixa uma imagem oficial que já vem com:

- Linux
- Node.js instalado
- NPM instalado

## Por que isso é melhor do que instalar Node manualmente no Ubuntu?

Porque esse é o padrão do Docker:

- cada imagem já vem preparada para uma finalidade
- você evita instalação manual dentro do container
- seu ambiente fica mais limpo e reproduzível

---

# Passo 10 — Rodar Node dentro do Docker

Agora vamos criar um container baseado na imagem do Node.

Rode:

```bash
docker run -it --name meu-node node:22 bash
```

Depois teste:

```bash
node -v
npm -v
```

## Saída esperada

Algo parecido com:

```bash
v22.x.x
10.x.x
```

## O que isso confirma

- Node está instalado dentro do container ✅
- NPM está instalado dentro do container ✅

---

# Passo 11 — Criar um projeto Node simples dentro do container

Ainda dentro do container `meu-node`, rode:

```bash
mkdir app
cd app
npm init -y
```

## O que esses comandos fazem

### `mkdir app`
Cria uma pasta chamada `app`.

### `cd app`
Entra nessa pasta.

### `npm init -y`
Cria um projeto Node básico automaticamente.

Agora crie um arquivo JavaScript:

```bash
echo "console.log('Docker Node OK')" > index.js
```

Depois execute:

```bash
node index.js
```

## Resultado esperado

```bash
Docker Node OK
```

## Atenção

Esse teste é útil para entender o funcionamento do Node dentro do container.

Mas esse ainda não é o fluxo ideal de desenvolvimento.

### Por quê?

Porque os arquivos estão dentro do container.
Se o container for removido, esses arquivos podem ser perdidos.

É por isso que o próximo passo é o mais importante.

---

# Passo 12 — Criar uma pasta do projeto no Mac

Agora vamos montar o fluxo profissional:

- código no Mac
- Docker apenas executando

No terminal do Mac, rode:

```bash
mkdir -p ~/projeto-node
cd ~/projeto-node
```

## O que isso faz

### `mkdir -p ~/projeto-node`
Cria a pasta do projeto no seu Mac.

### `cd ~/projeto-node`
Entra na pasta.

Agora crie um arquivo inicial:

```bash
echo "console.log('rodando com volume')" > index.js
```

Confira:

```bash
ls
```

Você deve ver o arquivo `index.js`.

---

# Passo 13 — Abrir essa pasta no VS Code

Ainda no terminal do Mac, dentro da pasta `~/projeto-node`, rode:

```bash
code .
```

## O que esse comando faz

Abre a pasta atual no VS Code.

## O que você deve fazer no VS Code

1. conferir se a pasta aberta é a `projeto-node`
2. localizar o arquivo `index.js`
3. editar esse arquivo pelo editor do VS Code

Por exemplo, você pode trocar o conteúdo dele para:

```js
console.log('rodando com volume no VS Code')
```

Salve o arquivo.

---

# Passo 14 — Rodar um container usando volume

Agora vamos conectar a pasta do Mac com uma pasta dentro do container.

No terminal do VS Code, ou no terminal do Mac, rode:

```bash
docker run -it \
-v ~/projeto-node:/app \
-w /app \
--name node-volume \
node:22 \
bash
```

## O que cada parte faz

### `-v ~/projeto-node:/app`
Conecta a pasta `~/projeto-node` do Mac com a pasta `/app` dentro do container.

### `-w /app`
Define `/app` como pasta de trabalho inicial do container.

### `--name node-volume`
Define um nome para o container.

## O que isso muda na prática

Agora o código não está mais preso dentro do container.

Você vai:

- editar os arquivos no Mac ou no VS Code
- executar os arquivos dentro do Docker

Esse é o fluxo profissional de desenvolvimento.

---

# Passo 15 — Testar se o volume está funcionando

Depois de entrar no container com volume, rode:

```bash
ls
node index.js
```

## O que deve acontecer

- `ls` deve mostrar o arquivo `index.js`
- `node index.js` deve executar o arquivo que está no Mac

Agora faça o teste mais importante:

1. volte no VS Code
2. altere o conteúdo do `index.js`
3. salve o arquivo
4. volte no terminal do container
5. rode de novo:

```bash
node index.js
```

## O que isso prova

Se a saída mudar, significa que:

- o arquivo está sendo editado no Mac
- o container está lendo esse mesmo arquivo em tempo real

Isso é exatamente o comportamento esperado de um volume.

---

# Passo 16 — Como sair e voltar sem perder o trabalho

## Para sair do terminal do container e parar o container

```bash
exit
```

## Para ligar o container de novo

```bash
docker start node-volume
```

## Para entrar novamente

```bash
docker exec -it node-volume bash
```

## Para sair sem parar o container

Use:

```text
Ctrl + P, depois Ctrl + Q
```

Esse atalho desacopla o terminal, mas mantém o container rodando.

---

# Passo 17 — Criar um servidor Node para acessar no navegador

Agora vamos criar um arquivo de servidor na pasta do projeto.

No VS Code, dentro da pasta `~/projeto-node`, crie um arquivo chamado `server.js` com este conteúdo:

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
  res.end('Rodando no Docker 🚀');
});

server.listen(3000, '0.0.0.0', () => {
  console.log('Servidor rodando na porta 3000');
});
```

## O que esse código faz

- cria um servidor HTTP simples
- responde com texto no navegador
- escuta na porta `3000`
- usa `0.0.0.0` para permitir acesso de fora do container

---

# Passo 18 — Rodar o servidor com mapeamento de porta

Agora rode este container:

```bash
docker run -it \
-v ~/projeto-node:/app \
-w /app \
-p 3000:3000 \
--name node-server \
node:22 \
bash
```

## O que a opção `-p 3000:3000` faz

Ela conecta:

- porta 3000 do Mac
- com a porta 3000 do container

Agora, dentro do container, rode:

```bash
node server.js
```

Você deve ver:

```bash
Servidor rodando na porta 3000
```

---

# Passo 19 — Abrir no navegador

Agora abra no navegador do Mac:

```text
http://localhost:3000
```

## Resultado esperado

Você verá:

```text
Rodando no Docker 🚀
```

Se isso aconteceu, significa que:

- seu código está no Mac
- o Docker executou o Node
- a porta foi exposta corretamente
- o navegador conseguiu acessar o container

---

# Passo 20 — Regra mais importante para guardar

## Regra de ouro

**Código fica no Mac. Docker executa.**

Esse é o fluxo ideal para desenvolvimento.

## Evite este erro

❌ Criar o projeto inteiro dentro do container sem volume.

## Prefira este fluxo

✅ Criar a pasta no Mac  
✅ Abrir no VS Code  
✅ Conectar com volume  
✅ Rodar dentro do Docker  

---

# Resumo final

Você aprendeu a:

- testar o Docker
- baixar imagens
- criar containers
- sair e voltar para containers
- usar Ubuntu no Docker
- usar VS Code com Docker
- baixar a imagem do Node
- rodar Node dentro do container
- usar volume entre Mac e container
- criar um servidor Node
- acessar esse servidor no navegador

---

# Comandos principais para decorar

```bash
docker --version
docker compose version
docker run hello-world
docker pull ubuntu:24.04
docker run -it --name meu-ubuntu ubuntu:24.04 bash
docker start meu-ubuntu
docker exec -it meu-ubuntu bash
docker pull node:22
docker run -it --name meu-node node:22 bash
docker run -it -v ~/projeto-node:/app -w /app --name node-volume node:22 bash
docker run -it -v ~/projeto-node:/app -w /app -p 3000:3000 --name node-server node:22 bash
```