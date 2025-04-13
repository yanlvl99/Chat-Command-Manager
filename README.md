# CommandRegistry

Um sistema para gerenciar comandos por chat no Roblox.

Desenvolvido por: yanlvl99_

## Carregando o Sistema

O CommandRegistry pode ser carregado usando `loadstring` através de um link HTTP:

```lua
-- Carregar o sistema
local CommandRegistry = loadstring(game:HttpGet("Meusite.com"))()
local registry = CommandRegistry.new()

```

## Exemplos de Comandos
### Comando Speed (Velocidade)

#### Descrição
Define a velocidade do personagem.

#### Uso
- `!speed 16` - Define velocidade para 16
- `!s 16` - Define velocidade para 16 (alias)
- `!spd 16` - Define velocidade para 16 (alias)

#### Exemplo
```lua
local Speed = registry:RegisterCommand("speed", {
    handler = function(player, args)
        local speed = args[1]
        if speed then
            player.Character.Humanoid.WalkSpeed = speed
            return true
        end
        return false
    end,
    description = "Define a velocidade do personagem",
    prefix = "!",
    log = false, -- Desativa logs para este comando
    enabled = true
})

Speed:AddArgType("speed", "number")
Speed:AddAlias("s", "spd", "velocidade")
```

## Configurações de Log

O sistema de logs pode ser configurado em dois níveis:

1. **Nível do Registro**:
```lua
-- Criar registro com logs ativados
local registry = CommandRegistry.new({ log = true })

-- Criar registro sem logs
local registry = CommandRegistry.new({ log = false })
```

2. **Nível do Comando**:
```lua
-- Comando com logs ativados (mesmo se o registro tiver logs desativados)
local MeuComando = registry:RegisterCommand("comando", {
    handler = function() end,
    description = "",
    log = true
})

-- Comando com logs desativados (mesmo se o registro tiver logs ativados)
local MeuComando = registry:RegisterCommand("comando", {
    handler = function() end,
    description = "",
    log = false
})
```

## Configurações Personalizadas

### Mudar Configurações
```lua
-- Mudar várias configurações de uma vez
MeuComando:ChangeConfig({
    prefix = "/",     -- Mudar prefixo
    enabled = false,   -- Desativar comando
    log = true,        -- Ativar logs
    returnType = "boolean" -- Mudar tipo de retorno
})
```

### Prefixo Personalizado
```lua
-- Mudar prefixo usando ChangeConfig
MeuComando:ChangeConfig({
    prefix = "/" -- Usar "/" em vez de "!"
})
```

### Estado Inicial
```lua
-- Criar comando desativado por padrão
local MeuComando = registry:RegisterCommand("comando", {
    handler = function() end,
    description = "",
    enabled = false -- Comando começa desativado
})

-- Ativar comando depois
MeuComando:ChangeConfig({
    enabled = true
})
```

## Funções Auxiliares

### Gerenciamento de Aliases

#### Adicionar Alias
```lua
MeuComando:AddAlias("alias1", "alias2", "alias3")
```

#### Remover Alias
```lua
MeuComando:RemoveAlias("alias1", "alias2")
```

#### Remover Todos os Aliases
```lua
MeuComando:RemoveAllAliases()
```

#### Obter Aliases
```lua
local aliases = MeuComando:GetAliases()
```

### Gerenciamento de Argumentos

#### Adicionar Tipo de Argumento
```lua
MeuComando:AddArgType("numero", "number")
```

#### Remover Tipo de Argumento
```lua
MeuComando:RemoveArgType("numero")
```

#### Obter Tipos de Argumentos
```lua
local args = MeuComando:GetArgs()
```

### Configuração do Comando

#### Obter/Definir Prefixo
```lua
local prefix = MeuComando:GetPrefix()
MeuComando:ChangeConfig({
    prefix = "/"
})
```

#### Obter/Definir Descrição
```lua
local desc = MeuComando:GetDescription()
```

#### Obter/Definir Tipo de Retorno
```lua
local returnType = MeuComando:GetReturnType()
MeuComando:ChangeConfig({
    returnType = "boolean"
})
```

#### Remover Comando
```lua
MeuComando:Remove()
```

### Gerenciamento do Registro

#### Obter Comando
```lua
local comando = registry:GetCommand("nome")
```

#### Obter Todos os Comandos
```lua
local todosComandos = registry:GetCommands()
```

#### Obter Todos os Aliases
```lua
local todosAliases = registry:GetAliases()
```

## Exemplo Completo com Configurações Personalizadas

```lua
-- Criar registro com logs ativados
local registry = CommandRegistry.new({ log = true })

-- Criar comando com configurações personalizadas
local MeuComando = registry:RegisterCommand("meucomando", {
    handler = function(player, args)
        local numero = args[1]
        local ativo = args[2]
        
        if ativo then
            return true
        end
        return false
    end,
    description = "Meu comando exemplo",
    prefix = "/", -- Usar "/" em vez de "!"
    log = true,    -- Ativar logs para este comando
    enabled = true -- Comando começa ativado
})

-- Configurar argumentos
MeuComando:AddArgType("numero", "number")
MeuComando:AddArgType("ativo", "boolean")
MeuComando:AddAlias("cmd", "meu", "mc")

-- Mudar configurações depois
MeuComando:ChangeConfig({
    enabled = false, -- Desativar comando
    log = false      -- Desativar logs
})

-- Usar o comando
-- Com prefixo personalizado: /meucomando 10 true
-- Com alias: /cmd 10 true
```

## Uso no Chat

Os comandos podem ser usados no chat com o prefixo configurado:

- `!meucomando 10 true` (prefixo padrão "!")
- `/meucomando 10 true` (prefixo personalizado "/")
- `!cmd 10 on` (com alias)
- `/mc 10 1` (com prefixo personalizado e alias)

## Logs e Debug

O sistema inclui logs detalhados que aparecem no console, mas podem ser configurados para cada comando:

```
[CommandRegistry] Mensagem recebida: /meucomando 10 true
[CommandRegistry] Prefixo detectado
[CommandRegistry] Comando: meucomando
[CommandRegistry] Argumentos: 10, true
[CommandRegistry] Comando encontrado
[CommandRegistry] Executando comando: meucomando
[CommandRegistry] Validando argumento: numero -> 10
[CommandRegistry] Validando argumento: ativo -> true
[CommandRegistry] Argumentos validados: 10, true
[CommandRegistry] Resultado do handler: true
[CommandRegistry] Enviando mensagem ao chat
```

## Recursos

- Validação automática de argumentos
- Suporte a múltiplos aliases
- Tipagem forte (number, boolean, string)
- Logs detalhados para debug (configuráveis por comando)
- Sistema de prefixos personalizáveis
- Retorno consistente de valores
- Remoção de comandos e aliases
- Gerenciamento de argumentos
- Configurações personalizadas por comando
- Sistema de logs granular (por comando e por registro)

## Suporte

Para mais informações ou suporte, entre em contato através do Discord ou GitHub.

## Licença

MIT License - Copyright (c) 2025
