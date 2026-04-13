Teste no terminal

Abra o terminal do Mac e rode:
```bash
docker --version
```

Depois rode:
```bash
docker compose version
```

Se quiser confirmar que o Docker está funcionando mesmo, rode:
```bash
docker compose version
```

Passo 2 — Entender o fluxo básico
O docker run cria e inicia um container, e se a imagem ainda não existir localmente ele pode puxar a imagem automaticamente. 
O fluxo principal é esse:
```bash
docker pull nome-da-imagem
docker run opções nome-da-imagem
```

Testando!
```bash
docker run hello-world
```
O que deve acontecer
Se tudo estiver certo, ele vai:
	1.	baixar uma imagem automaticamente
	2.	criar um container
	3.	executar
	4.	mostrar uma mensagem tipo:
```bash
    Hello from Docker!
```
Isso confirma que:
	•	Docker está instalado ✅
	•	Docker consegue baixar imagens ✅
	•	Containers estão funcionando ✅


Passo 3 — Baixar uma imagem de verdade (Ubuntu)
Agora sim, vamos trabalhar com algo real.
Roda isso:
```bash
docker pull ubuntu:24.04
```
O que você deve ver
Vai aparecer algo tipo:
24.04: Pulling from library/ubuntu
...
Status: Downloaded newer image for ubuntu:24.04

```bash
docker images
```

Você deve ver algo assim:
```bash
REPOSITORY   TAG     IMAGE ID     SIZE
ubuntu       24.04   xxxxxxxx     xxxMB
```

Passo 4 — Entrar dentro do container (Ubuntu)

Agora você vai literalmente abrir um Linux dentro do seu terminal.

Roda isso:

```bash
docker run -it --name meu-ubuntu ubuntu:24.04 bash
```

O que vai acontecer

Se der certo, seu terminal vai mudar pra algo assim:
```bash
root@abc123:/#
```
👉 Isso significa:
Você está dentro do container

Agora faz esses testes lá dentro
Roda esses comandos:
```bash
ls
pwd
echo "funcionando docker"
apt update
```

Passo 5 — Sair do container sem apagar
Agora, dentro do container, rode:

```bash
exit
```
Isso vai te tirar de dentro do Ubuntu e voltar pro terminal normal do Mac.

Importante

Isso não apaga a imagem.
E também não apaga o container.

Ele só para a execução do container.

⸻

Depois que sair, rode:
```bash
docker ps -a
```

Passo 6 — Ligar o container de novo

Agora vamos religar ele.

Roda isso:
```bash
docker start meu-ubuntu
```
O que vai acontecer
Ele vai apenas ligar o container, mas você ainda NÃO entrou nele.

Passo 7 — Entrar de novo no container
Agora entra nele:
```bash
docker exec -it meu-ubuntu bash
```

O que isso significa
	•	start → liga
	•	exec -it → entra no container que já existe
👉 Esse é o fluxo mais usado no dia a dia

Agora faz esses testes lá dentro
Roda esses comandos:
```bash
ls
pwd
echo "funcionando docker"
apt update
```

3. Conectar no container

No VS Code:
	1.	Pressiona:
```bash
Shift + Command + P
```
    2.	Digita:
```bash
Dev Containers: Attach to Running Container...
```

```bash
meu-ubuntu
```
O que vai acontecer
O VS Code vai abrir uma nova janela conectada ao container.
👉 Agora tudo que você fizer ali roda dentro do Linux (container)

4. Teste no VsCode
```bash
pwd
ls
```

Rode no terminal do Mac:
```bash
docker pull node:22
```

```bash
docker images
```

Passo — Rodar Node dentro do Docker

Agora vamos subir um container já com Node e abrir o terminal dentro dele.

Roda isso:
```bash
docker run -it --name meu-node node:22 bash
```

O que vai acontecer

Você vai entrar dentro de um container com Node instalado.

⸻

Teste lá dentro

Agora roda:
```bash
node -v
```

Aparece:
```bash
v22.x.x
```