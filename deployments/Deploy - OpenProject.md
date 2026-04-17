## Visão Geral  
Deploy do OpenProject em container LXC no Proxmox utilizando script automatizado da comunidade.  

---  

## Pré-requisitos  
- Proxmox VE  
- Acesso ao shell do host Proxmox  
- Conectividade com internet  
- Container LXC disponível ou permissões para criação automática  
- Porta disponível:  
  - 80 (HTTP)  

---  

## Passo a Passo  

### 1. Preparação do ambiente  
Acessar o shell do Proxmox:  

```bash
ssh root@<ip-do-proxmox>
````

### 2. Instalação do OpenProject

Executar o script automatizado:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/openproject.sh)"
```

- O script cria o container automaticamente
- Instala todas as dependências
- Configura o serviço

### 3. Finalização

Aguardar a conclusão do script.  
Após finalizar, o container estará em execução com o serviço disponível.

---

## Comandos

```bash
# Executar instalação automatizada
bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/openproject.sh)"

# Acessar container (substituir ID)
pct enter <CTID>

# Verificar status do container
pct status <CTID>

# Reiniciar container
pct restart <CTID>
```

---

## Configurações

- Porta: 80
- Caminho de acesso: `/openproject` (dependendo da configuração do script)
- Credenciais padrão:
    - Usuário: admin
    - Senha: admin

---

## Acesso

- URL: [http://192.168.15.8](http://192.168.15.8)
- Alternativo: [http://192.168.15.8/openproject](http://192.168.15.8/openproject)
- Tipo: acesso local via navegador (HTTP)

---

## Verificação

- Acessar a interface web no navegador
- Validar carregamento da página do OpenProject
- Confirmar login com usuário admin
- Verificar se é possível criar projeto

---

## Problemas comuns

### Serviço não acessível após instalação

- Causa: container ainda inicializando
- Solução: aguardar finalização completa do setup

### Falha no acesso com credenciais padrão

- Causa: senha alterada no primeiro acesso
- Solução: utilizar recuperação de senha ou redefinir usuário

---

## Reexecução / Manutenção

Reiniciar container:

```bash
pct restart <CTID>
```

Parar container:

```bash
pct stop <CTID>
```

Iniciar container:

```bash
pct start <CTID>
```

Acessar shell do container:

```bash
pct enter <CTID>
```

---

## Observações

- Alterar credenciais padrão imediatamente após o primeiro acesso
- Recomenda-se uso de HTTPS via reverse proxy
- Ideal restringir acesso externo via VPN
- Script automatiza todo o processo, reduzindo necessidade de configuração manual