## Visão Geral
- Painel de gerenciamento para servidores de Minecraft
- Permite criar, iniciar, parar e monitorar servidores
- Centraliza administração via interface web
- Papel no homelab: gerenciamento de servidores de jogos de forma simples e remota

## Objetivo no Ambiente
- Facilitar a gestão de servidores Minecraft sem uso direto de terminal
- Centralizar controle e monitoramento em uma interface web
- Escolhido por ser open-source e com suporte a múltiplos servidores

## Arquitetura
- Execução em VM
- Host: Proxmox
- Dependências: Git, Python 3.10+
- Integração com servidores Minecraft via porta padrão (25565)

## Setup

### Ambiente
- Sistema operacional: Ubuntu Server 24.04.3
- VM configurada com:
  - CPU: 4 vCPUs
  - RAM: 8GB
  - Storage: 128GB

### Configuração

**Instalação do Git**
```bash
sudo apt update && sudo apt upgrade && sudo apt install git
````

**Instalação do Crafty**

```bash
git clone https://gitlab.com/crafty-controller/crafty-installer-4.0.git && \
cd crafty-installer-4.0 && \
sudo ./install_crafty.sh
```

**Execução manual**

```bash
sudo su crafty
cd /var/opt/minecraft/crafty
./run_crafty.sh
```

**Execução como serviço**

Durante a instalação, é possível configurar como serviço.

Iniciar serviço:

```bash
sudo systemctl start crafty
```

Habilitar no boot:

```bash
sudo systemctl enable crafty
```

## Rede e Acesso

* IP da VM: 192.168.15.15
* Porta WebUI: 8443
* Porta de tráfego Minecraft: 25565

Acesso via navegador:

* [https://192.168.15.15:8443](https://192.168.15.15:8443)

Acesso SSH:

```bash
ssh crafty@192.168.15.15
```

* IP reservado no roteador para garantir acesso consistente

## Uso

* Criar e gerenciar servidores Minecraft via interface web
* Iniciar/parar servidores sem acesso direto ao terminal
* Monitorar uso de recursos e logs
* Gerenciar múltiplas instâncias de servidor

## Problemas e Soluções

### Problema

Serviço não inicia automaticamente

* Possível causa: serviço não habilitado no boot
* Solução:

```bash
sudo systemctl enable crafty
```

### Problema

Serviço instalado mas não está rodando

* Possível causa: serviço não iniciado após instalação
* Solução:

```bash
sudo systemctl start crafty
```

## Segurança

* Serviço acessível via rede local
* Porta 8443 exposta internamente
* Acesso via HTTPS (porta 8443)
* Uso de usuário dedicado (`crafty`) para execução do serviço
* Recomenda-se uso de VPN para acesso externo

## Melhorias Futuras

* Configurar acesso via domínio com reverse proxy (ex: Nginx)
* Implementar autenticação mais robusta (se aplicável)
* Backup automatizado dos servidores Minecraft

## Aprendizados

* Instalação e gerenciamento de serviços via systemd
* Uso de usuários dedicados para serviços
* Configuração de serviços em VM no Proxmox
* Exposição e gerenciamento de portas de rede
* Automação de instalação via scripts


[[Deploy - Crafty Controller]]