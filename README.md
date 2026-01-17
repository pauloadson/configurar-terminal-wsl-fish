# Configurando o Terminal com Fish e WSL

Este guia mostra como instalar e configurar o [Fish](https://fishshell.com/), um shell amigável e interativo, no Windows usando o [Subsistema Windows para Linux (WSL)](https://learn.microsoft.com/pt-br/windows/wsl/install).

## Pré-requisitos

- **Windows 10 ou 11:** O WSL requer uma versão recente do Windows.
- **WSL instalado:** Você precisa ter o WSL instalado em sua máquina. Se não tiver, siga o [guia de instalação oficial da Microsoft](https://learn.microsoft.com/pt-br/windows/wsl/install).
- **Uma distribuição Linux instalada (Ubuntu):** Este guia usa o Ubuntu como exemplo. Você pode instalar o Ubuntu a partir da Microsoft Store.

## Passos

### 1. Inicie o WSL e o Ubuntu

Abra o seu terminal e inicie o WSL:

```bash
wsl
```

### 2. Instale o Fish

No terminal do Ubuntu, atualize os seus pacotes e instale o Fish:

```bash
sudo apt-get update
sudo apt-get install fish
```

### 3. Defina o Fish como o seu shell padrão

Para usar o Fish como o seu shell padrão, execute o seguinte comando:

```bash
chsh -s /usr/bin/fish
```

Feche e reabra o seu terminal. Você deve ser saudado com o prompt do Fish.

### 4. Configure o Fish (Opcional)

O Fish é altamente configurável. Você pode personalizar o seu prompt, adicionar aliases e instalar plugins.

- **Configuração baseada na Web:** O Fish oferece uma interface de configuração baseada na Web. Para iniciá-la, execute:

  ```bash
  fish_config
  ```

- **Arquivo de configuração:** Você pode editar o arquivo de configuração do Fish diretamente em `~/.config/fish/config.fish`.

### 5. Instale um Gerenciador de Plugins (Fisher)

[Fisher](https://github.com/jorgebucaran/fisher) é um gerenciador de plugins para o Fish.

**Instalação:**

```bash
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher
```

**Gerenciando Plugins com Fisher:**

- **Instalar um plugin (ex: `jorgebucaran/nvm.fish`):**
  ```bash
  fisher install jorgebucaran/nvm.fish
  ```

- **Listar plugins instalados:**
  ```bash
  fisher list
  ```

- **Atualizar todos os plugins:**
  ```bash
  fisher update
  ```

- **Remover um plugin (ex: `jorgebucaran/nvm.fish`):**
  ```bash
  fisher remove jorgebucaran/nvm.fish
  ```

### 6. Plugins e Ferramentas Adicionais

Aqui estão alguns plugins e ferramentas úteis que se integram bem com o Fish e o Fisher.

**Instalação de Ferramentas e Plugins:**

```bash
sudo apt install fzf
sudo apt install fd-find
sudo apt install bat
fisher install PatrickF1/fzf.fish
```

**Atalhos do `fzf.fish`:**

```
    By default, commands are bound to a mnemonic key sequence, shown below. Each command's binding
    can be configured using a namesake corresponding option:
        COMMAND            |  DEFAULT KEY SEQUENCE         |  CORRESPONDING OPTION
        Search Directory   |  Ctrl+Alt+F (F for file)      |  --directory
        Search Git Log     |  Ctrl+Alt+L (L for log)       |  --git_log
        Search Git Status  |  Ctrl+Alt+S (S for status)    |  --git_status
        Search History     |  Ctrl+R     (R for reverse)   |  --history
        Search Processes   |  Ctrl+Alt+P (P for process)   |  --processes
        Search Variables   |  Ctrl+V     (V for variable)  |  --variables
    Override a command's binding by specifying its corresponding option with the desired key
    sequence. Disable a command's binding by specifying its corresponding option with no value.
```

## Habilitando a Interoperabilidade do WSL e Fish

Para uma integração mais robusta entre o WSL e o Windows, como usar o navegador do Windows a partir do Fish, siga estes passos.

### 1️⃣ Habilitar interoperabilidade do WSL

No WSL, edite ou crie o arquivo `/etc/wsl.conf`:

```bash
sudo nano /etc/wsl.conf
```

Adicione o seguinte conteúdo:

```
[interop]
enabled=true
appendWindowsPath=true
```

### 2️⃣ Reiniciar o WSL

No **PowerShell** ou **Prompt de Comando** do Windows, desligue o WSL para que as alterações sejam aplicadas:

```powershell
wsl --shutdown
```

Depois, abra o WSL novamente.

### 3️⃣ Testar interop

No terminal do WSL, verifique se a comunicação com o Windows está funcionando:

```bash
powershell.exe -c "echo OK"
cmd.exe /c echo OK
```

### 4️⃣ Instalar wslview

A ferramenta `wslview` permite abrir links e arquivos do WSL no Windows.

Instale o pacote `wslu` que a contém:
```bash
sudo apt update
sudo apt install wslu
```

Teste a instalação:

```bash
wslview https://www.google.com
```

### 5️⃣ Configurar Fish para usar navegador do Windows

Edite o arquivo de configuração do Fish:

```bash
nano ~/.config/fish/config.fish
```

Adicione a seguinte linha para definir o `wslview` como o navegador padrão:

```fish
set -x BROWSER wslview
```

Recarregue a configuração:

```fish
source ~/.config/fish/config.fish
```

### 6️⃣ Testar Fish

Execute o comando de configuração web do Fish para testar:

```fish
fish_config
```

Isso deve abrir a interface de configuração no seu navegador padrão do Windows.

### 7️⃣ Diagnóstico rápido (opcional)

Verifique o status da interoperabilidade:

```bash
cat /proc/sys/fs/binfmt_misc/WSLInterop
```

O resultado esperado é `enabled`.

## Conclusão

Agora você tem um terminal poderoso e amigável com o Fish rodando no WSL. Explore os temas e plugins para personalizar a sua experiência!
