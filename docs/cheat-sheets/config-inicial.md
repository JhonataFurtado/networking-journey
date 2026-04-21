# Configuração Inicial de Dispositivos

Este guia contém os comandos básicos para quase todos os dispositivos Cisco IOS para garantir o minímo de segurança e acessibilidade

## 1. Identificação e Segurança Básica
> "A identificação básica serve para gerenciamento, praticidade em encontrar problemas e monitorar a própria topologia. A segurança básica serve para assegurar que ninguém autorizado vai mexer, analisar ou hackear seu dispositivo"
```bash
>Enable
#Configure Terminal
(config)#Hostname [Nome do Dispositivo]
(config)#Enable Secret [Senha]
(config)#Banner motd "ACESSO RESTRITO E MONITORADO"
```

## 2. Otimização do Console
> "A configuração da porta console serve para configurar a interface que você se conecta"

```bash
(config)#line console 0
(config-line)#password [SENHA]
(config-line)#Login
(config-line)#logging synchronous
(config-line)#Exec-timeout 5 0
(config-line)#Exit
(config)#Service password-encryption
```

## 3. Gerenciamento IP (Roteador)
> "O IP no roteador serve para roteamento"

```bash
(config)#Interface [x]
(config-if)#Ip address [IP] [Máscara]
(config-if)#No shutdown
(config-if)#Do copy running-config startup-config
```

## 4. Gerenciamento IP (Switch)
> "O IP no switch serve para gerenciamento/acesso remoto (SSH/Telnet)

```bash
(config)#Interface vlan 1
(config-if)#Ip address [IP] [Máscara]
(config-if)#No shutdown
(config-if)#Exit
(config)#Ip default-gateway [IP do gateway]
(config)#Do copy running-config startup-config
```

---

## Explicação dos Comandos
| Comando | Descrição |
|---------|-----------|
| `Enable` | Comando usado para acessar o modo privilegiado |
| `Configure Terminal` | Comando usado para acessar o mode de configuração global do dispositivo |
| `Hostname [Nome do Dispositivo]` | Comando usado para adicionar um nome Lógico para esse dispositivo |
| `Enable Secret [Senha]` | Comando usado para adicionar uma senha criptografada com hashing unidirecional ao modo privilegiado |
| `Banner motd "ACESSO RESTRITO E MONITORADO"` | Comando para adicionar uma mensagem no boot do dispositivo (Aviso Legal) |
| `line console 0` | Comando para acessar a porta console do dispositivo |
| `password [SENHA]` | Comando para adicionar uma senha a porta console do dispositivo |
| `Login` | Comando para ativar a senha da porta console |
| `logging synchronous` | Comando para criptografa as senhas que ficam visíveis em texto claro no show run |
| `Exec-timeout 5 0` | Comando para adicionar um tempo de inatividade da sessão (5=minutos/0=segundos) |
| `Service password-encryption` | Comando para salvar a configuração atual na memória não volátil (NVRAM) para que persista após reinicializações |
| `Interface [x]` | Comando para acessar a interface do roteador |
| `Ip address [IP] [Máscara]` | Comando para adicionar um endereço ip e máscara na interface do roteador |
| `No shutdown` | Comando para ativar a interface do roteador |
| `Interface vlan 1` | Comando para acessar a vlan nativa do switch |
| `Ip address [IP] [Máscara]` | Comando para adicionar um endereço ip e máscara na vlan nativa do switch |
| `No shutdown` | Comando para ativar a vlan nativa do switch |
| `Exit` | Comando para subir um nível na hierarquia (voltar ao modo de configuração anterior) |
| `Ip default-gateway [IP do gateway]` | Comando para adicionar um gateway padrão ao switch |
| `copy running-config startup-config` | Comando para salvar a configuração atual na memória não volátil (NVRAM) para que persista após reinicializações |
| `Do` | Serve para executar comandos do modo EXEC privilegiado enquanto você está em qualquer submodo de configuração |

---

🔗 **Navegação:** [← Voltar](./README.md) • [🏠 Início](../README.md) • [↑ Topo](#topo)
