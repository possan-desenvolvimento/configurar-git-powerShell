# 🛠️ Configurando o Git com SSH via PowerShell (Windows)

Este guia tem como objetivo ensinar como configurar o Git para autenticação via **SSH** utilizando o **PowerShell no Windows**. Ideal para quem deseja trabalhar com repositórios privados de forma segura e prática.

---

## ✅ Pré-requisitos

- Git instalado: [Baixar Git](https://git-scm.com/download/win)
- Conta no [GitHub](https://github.com)
- PowerShell (vem instalado por padrão no Windows)

---

## 📦 Etapas de Configuração

### 1. Verifique se o Git está instalado

No PowerShell, digite:

git --version

Você deverá ver algo como:
- git version 2.xx.x

---
### 2. Gere uma nova chave SSH
Execute o comando: 

ssh-keygen

Pressione Enter para aceitar o caminho padrão (C:\Users\SeuUsuario\.ssh\id_ed25519)

(Opcional) Defina uma senha para proteger a chave, ou apenas pressione Enter novamente

---

### 3. Ative e inicie o ssh-agent
Abra o PowerShell como administrador e execute:

Set-Service ssh-agent -StartupType Automatic

Depois:

Start-Service ssh-agent

Isso garante que o agente de autenticação SSH inicie automaticamente com o Windows.

---

### 4. Adicione sua chave privada ao ssh-agent

Execute no PowerShell (normal, não administrador):

ssh-add $env:USERPROFILE\.ssh\id_ed25519

Confirme que a chave foi adicionada com:

ssh-add -l

---

# 5. Adicione sua chave pública ao GitHub
Abra o arquivo da chave pública:

notepad $env:USERPROFILE\.ssh\id_ed25519.pub

Copie o conteúdo completo (começa com ssh-ed25519)

---

# No GitHub, vá em:
Settings → SSH and GPG keys → New SSH key

Cole a chave, dê um nome (ex: Notebook-Pessoal) e clique em Add SSH key

--- 

### 6. Teste sua conexão com o GitHub
No PowerShell:

ssh -T git@github.com

Você deve ver uma mensagem como:

Hi seu-usuario! You've successfully authenticated, but GitHub does not provide shell access.

--- 

# 7. Configure seu nome e e-mail no Git

git config --global user.name "Seu Nome"

git config --global user.email "seu@email.com"

--- 

# 8. Clone um repositório via SSH

git clone git@github.com:usuario/repositorio.git

--- 

# 🚀 Pronto!
Seu ambiente Git com autenticação SSH está configurado com sucesso! Agora você pode clonar, fazer push e pull em repositórios privados sem precisar digitar seu usuário e senha.

---

# 🔒 Dica extra: nunca compartilhe sua chave privada (id_ed25519) com ninguém!



