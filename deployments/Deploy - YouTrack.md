
## Visão Geral  
Deploy do YouTrack via Docker utilizando imagem oficial da JetBrains com persistência de dados em volumes locais.  

---  

## Pré-requisitos  
- VM Linux (Ubuntu recomendado)  
- Docker instalado
- Acesso sudo
- Portas disponíveis:
  - 8080 (HTTP)
  - 443 (HTTPS - opcional)

---  

## Passo a Passo  
### 1. Preparação do ambiente  
Criar diretório de trabalho e acessar:  
```bash
mkdir youtrack && cd youtrack
````

### 2. Criação dos volumes

Criar diretórios com permissões corretas:
```bash
for i in data logs conf backups; do mkdir -p -m 750 $i && chown -R 13001:13001 $i ; done
```

### 3. Execução do container
Executar o container manualmente:
```bash
docker run -it --name youtrack \
-v ./data:/opt/youtrack/data \
-v ./conf:/opt/youtrack/conf \
-v ./logs:/opt/youtrack/logs \
-v ./backups:/opt/youtrack/backups \
-p 8080:8080 \
-p 443:443 \
jetbrains/youtrack:2026.1.12458
```

### 4. Configuração inicial

- Acessar a interface web
- Copiar o Wizard Token exibido no terminal/logs
- Finalizar setup via navegador

---

## Comandos

```bash
# Criar diretórios com permissões
for i in data logs conf backups; do mkdir -p -m 750 $i && chown -R 13001:13001 $i ; done

# Executar container
docker run -it --name youtrack \
-v ./data:/opt/youtrack/data \
-v ./conf:/opt/youtrack/conf \
-v ./logs:/opt/youtrack/logs \
-v ./backups:/opt/youtrack/backups \
-p 8080:8080 \
-p 443:443 \
jetbrains/youtrack:2026.1.12458

# Script opcional
vi start_docker.sh

# Permissão e execução do script
chmod +x start_docker.sh
./start_docker.sh
```

---

## Configurações

- Porta HTTP: 8080
- Porta HTTPS: 443
- Diretórios persistentes:
    - `./data` → `/opt/youtrack/data`
    - `./conf` → `/opt/youtrack/conf`
    - `./logs` → `/opt/youtrack/logs`
    - `./backups` → `/opt/youtrack/backups`
- UID necessário: 13001

Exemplo de execução via script:

```bash
docker run -it --name youtrack \
-v ./data:/opt/youtrack/data \
-v ./conf:/opt/youtrack/conf \
-v ./logs:/opt/youtrack/logs \
-v ./backups:/opt/youtrack/backups \
-p 8080:8080 \
-p 443:443 \
jetbrains/youtrack:2026.1.12458
```

---

## Acesso

- URL: [http://192.168.15.9:8080](http://192.168.15.9:8080)
- Tipo: acesso local via navegador (HTTP)
- SSH:

```bash
ssh roger@192.168.15.9
```

---

## Verificação

- Acessar a interface web
- Validar exibição da tela de setup
- Confirmar uso do Wizard Token
- Após setup, validar criação de projetos/issues

Verificar container:

```bash
docker ps
```

Ver logs:

```bash
docker logs youtrack
```

---

## Problemas comuns

### Permissões incorretas nos diretórios

- Causa: UID exigido pelo container (13001)
- Solução:

```bash
chown -R 13001:13001 data logs conf backups
```

### Dados não persistem

- Causa: volumes não configurados corretamente
- Solução: garantir uso dos parâmetros `-v` no container

### Acesso inicial não funciona

- Causa: setup não finalizado (Wizard Token não utilizado)
- Solução: copiar token dos logs e concluir via navegador

---

## Reexecução / Manutenção

Parar container:

```bash
docker stop youtrack
```

Iniciar container:

```bash
docker start youtrack
```

Reiniciar:

```bash
docker restart youtrack
```

Remover container:

```bash
docker rm -f youtrack
```

Atualizar imagem:

```bash
docker pull jetbrains/youtrack:2026.1.12458
```

---

## Observações

- Recomenda-se uso de `--restart unless-stopped` em produção
- HTTPS precisa de configuração adicional (reverse proxy ou certificado)
- Garantir backup periódico do diretório `backups`
- Ideal uso de Docker Compose para padronização do deploy