## Visão Geral
- Sistema open-source de gerenciamento de projetos
- Permite controle de tarefas, equipes, prazos e workflows
- Inclui recursos como Kanban, Gantt e tracking de atividades
- Papel no homelab: centralização da gestão de projetos e tarefas

## Objetivo no Ambiente
- Organizar projetos técnicos e operacionais do homelab
- Controlar tarefas, prazos e progresso
- Escolhido por ser uma solução completa, open-source e self-hosted

## Arquitetura
- Execução em container (LXC)
- Host: Proxmox
- Instalação via script automatizado da comunidade ProxmoxVE
- Dependências provisionadas automaticamente pelo script

## Setup

### Ambiente
- Container criado no Proxmox
- Recursos:
  - CPU: 2 vCPUs
  - RAM: 4GB
  - Storage: 8GB

### Configuração

**Instalação via script**
```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/openproject.sh)"
````

- Instalação totalmente automatizada
## Rede e Acesso
- IP: 192.168.15.8
- Porta: 80

Acesso via navegador:
- [http://192.168.15.8](http://192.168.15.8)
- [http://192.168.15.8/openproject](http://192.168.15.8/openproject)

Credenciais padrão:
- Usuário: admin
- Senha: admin

## Uso

- Criação e gerenciamento de projetos
- Organização de tarefas com Kanban
- Planejamento com Gantt
- Acompanhamento de progresso e atividades

## Problemas e Soluções

### Problema

Serviço não acessível após instalação
- Possível causa: container ainda inicializando
- Solução: aguardar finalização completa do setup

### Problema

Acesso com credenciais padrão falha
- Possível causa: senha alterada no primeiro acesso
- Solução: utilizar recuperação de senha ou redefinir usuário

## Segurança

- Serviço exposto na rede local via HTTP (porta 80)
- Uso inicial de credenciais padrão
- Boas práticas:
    - Alterar senha do admin imediatamente
    - Implementar HTTPS via reverse proxy
    - Restringir acesso externo (VPN)

## Melhorias Futuras

- Configurar HTTPS (Nginx ou Traefik)
- Automatizar backups
- Criar templates de projetos
- Integrar com outras ferramentas do homelab

## Aprendizados

- Deploy automatizado via scripts no Proxmox
- Uso de containers LXC para aplicações web
- Configuração inicial de ferramentas de gestão
- Exposição e acesso a serviços web internos