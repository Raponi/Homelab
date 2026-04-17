## Visão Geral
- Sistema de gerenciamento de projetos e issues da JetBrains
- Permite controle de tarefas, bugs, workflows e equipes
- Interface web com foco em rastreamento de issues e produtividade
- Papel no homelab: gerenciamento de tarefas técnicas e projetos

## Objetivo no Ambiente
- Centralizar gestão de tarefas e issues do homelab
- Substituir ou complementar ferramentas de gerenciamento de projetos
- Escolhido por ser robusto, self-hosted e com integração a workflows

## Arquitetura
- Execução via Docker
- Host: VM no Proxmox
- Serviço containerizado utilizando imagem oficial da JetBrains
- Persistência de dados via volumes (data, logs, conf, backups)

## Setup

### Ambiente
- VM no Proxmox
- Recursos:
  - CPU: 4 cores
  - RAM: 4GB
  - Storage: 32GB
- Docker previamente instalado

### Configuração

**Criação de diretórios**
```bash
for i in data logs conf backups; do mkdir -p -m 750 $i && chown -R 13001:13001 $i ; done
````

**Execução do container**

```bash
docker run -it --name youtrack \
-v ./data:/opt/youtrack/data \
-v ./conf:/opt/youtrack/conf \
-v ./logs:/opt/youtrack/logs \
-v ./backups:/opt/youtrack/backups \
-p 8080:8080 \
jetbrains/youtrack:2026.1.12458
```

**Script para execução simplificada**

```bash
vi start_docker.sh
```

Conteúdo do arquivo:

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

**Permissão e execução**

```bash
chmod +x start_docker.sh
./start_docker.sh
```

**Configuração inicial**

- Acessar interface web
- Copiar o _Wizard Token_ exibido no terminal/logs
- Finalizar setup via navegador

## Rede e Acesso

- IP: 192.168.15.9
- Porta HTTP: 8080
- Porta HTTPS: 443

Acesso via navegador:

- [http://192.168.15.9:8080](http://192.168.15.9:8080)

Acesso SSH:

```bash
ssh roger@192.168.15.9
```

## Uso

- Gerenciamento de issues e tarefas
- Organização de projetos técnicos
- Criação de workflows personalizados
- Acompanhamento de bugs e demandas

## Problemas e Soluções

### Problema

Permissões incorretas nos diretórios
- Possível causa: container exige UID específico (13001)
- Solução:

```bash
chown -R 13001:13001 data logs conf backups
```

### Problema

Dados não persistem após reinício

- Possível causa: volumes não configurados corretamente
- Solução: garantir uso dos volumes no comando `docker run`

### Problema

Acesso inicial não funciona

- Possível causa: setup não finalizado (Wizard Token não utilizado)
- Solução: copiar token e concluir configuração via navegador

## Segurança

- Serviço exposto na rede local
- Porta 8080 (HTTP) ativa
- Porta 443 configurada no container (HTTPS ainda não implementado)
- Acesso inicial protegido por Wizard Token
- Recomenda-se:
    - Configurar HTTPS corretamente
    - Restringir acesso externo via VPN
    - Utilizar firewall para controle de portas

## Melhorias Futuras

- Configurar HTTPS funcional
- Criar container com restart automático (`--restart unless-stopped`)
- Utilizar Docker Compose para melhor gerenciamento
- Implementar backups automatizados
- Integrar com outras ferramentas do homelab

## Aprendizados

- Deploy de aplicações via Docker
- Gerenciamento de volumes e persistência de dados
- Controle de permissões com UID/GID em containers
- Exposição de serviços web via portas
- Setup inicial com tokens de autenticação