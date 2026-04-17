## Visão Geral  
Deploy do Crafty Controller em VM Ubuntu para gerenciamento de servidores Minecraft via interface web.  

---  

## Pré-requisitos  
- Ubuntu Server 24.04+  
- Acesso root ou sudo  
- Git  
- Python 3.10+ (instalado automaticamente pelo script, se necessário)  
- Portas disponíveis:  
  - 8443 (WebUI)  
  - 25565 (Minecraft)  

---  

## Passo a Passo  

### 1. Preparação do ambiente  
Atualizar o sistema:  

```bash
sudo apt update && sudo apt upgrade -y
````

### 2. Instalação de dependências

Instalar Git:

```bash
sudo apt install git -y
```

### 3. Instalação do Crafty Controller

Clonar o repositório e executar o instalador:

```bash
git clone https://gitlab.com/crafty-controller/crafty-installer-4.0.git
cd crafty-installer-4.0
sudo ./install_crafty.sh
```

### 4. Execução do serviço

Iniciar o serviço:

```bash
sudo systemctl start crafty
```

Habilitar no boot:

```bash
sudo systemctl enable crafty
```

---

## Comandos

```bash
# Atualizar sistema
sudo apt update && sudo apt upgrade -y

# Instalar Git
sudo apt install git -y

# Clonar e instalar Crafty
git clone https://gitlab.com/crafty-controller/crafty-installer-4.0.git
cd crafty-installer-4.0
sudo ./install_crafty.sh

# Gerenciar serviço
sudo systemctl start crafty
sudo systemctl enable crafty

# Execução manual (alternativa)
sudo su crafty
cd /var/opt/minecraft/crafty
./run_crafty.sh

# Acesso SSH
ssh crafty@192.168.15.15
```

---

## Configurações

- Porta WebUI: 8443
- Porta Minecraft: 25565
- Diretório de instalação: `/var/opt/minecraft/crafty`
- Usuário do serviço: `crafty`

---

## Acesso

- URL: [https://192.168.15.15:8443](https://192.168.15.15:8443)
- Tipo: acesso local via navegador (HTTPS)
- SSH:

```bash
ssh crafty@192.168.15.15
```

---

## Verificação

- Acessar a interface web no navegador
- Validar carregamento da WebUI
- Verificar status do serviço:

```bash
systemctl status crafty
```

- Verificar logs:

```bash
journalctl -u crafty
```

---

## Problemas comuns

### Serviço não inicia automaticamente

- Causa: não habilitado no boot
- Solução:

```bash
sudo systemctl enable crafty
```

### Serviço não está rodando

- Causa: não iniciado após instalação
- Solução:

```bash
sudo systemctl start crafty
```

---

## Reexecução / Manutenção

Reiniciar serviço:

```bash
sudo systemctl restart crafty
```

Parar serviço:

```bash
sudo systemctl stop crafty
```

Atualizar (script):

```bash
sudo -u crafty /var/opt/minecraft/crafty/update_crafty.sh
```

---

## Observações

- Utilizar IP fixo ou reserva DHCP para acesso consistente
- Recomendado uso de VPN para acesso externo
- Pode ser executado manualmente sem systemd para debug
- Ideal para centralizar múltiplos servidores Minecraft em uma única interface