# 🧪 Engenharia do Caos com Chaos Toolkit, Node.js e Redis

Este projeto demonstra uma prova de conceito de **Engenharia do Caos** usando o [Chaos Toolkit](https://chaostoolkit.org/) para simular falhas no Redis de uma aplicação Node.js. Tudo é orquestrado com Docker Compose.

---

## ⚙️ Tecnologias usadas
<table>
  <tr>
    <th></th>
    <th>Tecnologia</th>
    <th>Versão</th>
    <th>Ferramentas</th>    
  </tr>
  <tr>
    <td><img align="center" alt="Rafa-Csharp" height="30" width="40" src="https://icongr.am/devicon/nodejs-original.svg?size=40&color=currentColor"></td>
    <td><a href="https://nodejs.org/">Node.js</a></td>
    <td>v20.16.0</td>
    <td><a href="https://expressjs.com/pt-br/">Express</a></td>
  </tr>
  <tr>
    <td><img align="center" alt="Rafa-Csharp" height="30" width="40" src="https://icongr.am/devicon/visualstudio-plain.svg?size=40"></td>
    <td>Visual Studio</td>
    <td>Code</td>
    <td></td>
  </tr>    
  <tr>
    <td><img align="center" alt="Rafa-Csharp" height="30" width="40" src="https://icongr.am/devicon/git-original.svg?size=40"></td>
    <td><a href="https://git-scm.com/">Git</a></td>
    <td>lasted</td>
    <td></td>    
  </tr>  
  <tr>
    <td><img align="center" alt="Rafa-Csharp" height="30" width="40" src="https://icongr.am/devicon/redis-original.svg?size=40&color=currentColor"></td>
    <td><a href="https://redis.io/">Redis</a></td>
    <td>lasted</td>
    <td></td>    
  </tr> 
  <tr>
    <td><img align="center" alt="Rafa-Csharp" height="30" width="40" src="https://www.vectorlogo.zone/logos/grafana/grafana-icon.svg?size=40"></td>
    <td><a href="https://chaostoolkit.org/">Chaos Toolkit</a></td>
    <td>lasted</td>
    <td></td>    
  </tr> 
  <tr>
    <td><img align="center" alt="Rafa-Csharp" height="30" width="40" src="https://icongr.am/devicon/docker-original.svg?size=40"></td>
    <td><a href="https://www.docker.com/">Docker</a></td>
    <td>lasted</td>
    <td><a href="https://docs.docker.com/compose">Docker Compose</a></td>    
  </tr>
</table>

---

## ⚙️ Pré-requisitos

- 🐳 [Docker](https://www.docker.com/get-started)
- 📦 [Docker Compose](https://docs.docker.com/compose/install/)
---
## 🚀 Como rodar

### 1. Clonar o repositório

```bash
git clone https://github.com/seu-usuario/chaos-node-redis.git
cd chaos-node-redis
```

### 2. Subir os containers

```bash
docker-compose up --build
```

> O experimento do Chaos Toolkit será executado automaticamente após subir a aplicação.

---

## 🌐 Aplicação

A aplicação expõe o endpoint:

```
GET /health
```

Este endpoint interage com o Redis e responde:

```json
{
  "status": "ok",
  "redis": "pong"
}
```

---

## 🔥 Experimento Chaos Toolkit

O experimento (`chaos/redis-failure.json`) realiza os seguintes passos:

1. Verifica se a aplicação responde (`/health`)
2. Para o container Redis (`docker stop redis`)
3. Verifica o comportamento da aplicação sem Redis
4. Religa o Redis (`docker start redis`)
5. Verifica novamente a saúde da aplicação

---

## ✍️ Saída esperada

```
[INFO] Steady state hypothesis is met!
[INFO] Action: parar_container_redis
[INFO] Probe: verifica_servico_aplicacao_apos_falha
[ERROR] => failed: activity took too long to complete
[INFO] Action: iniciar_container_redis
[INFO] Steady state hypothesis is met!
```

---

## ✅ Testes manuais

```bash
# Subir Redis e app
docker-compose up -d redis app

# Verificar endpoint
curl http://localhost:3000/health

# Parar Redis
docker stop redis

# Verificar resposta da app
curl http://localhost:3000/health

# Subir Redis novamente
docker start redis
```

---
