# Device Management & Troubleshooting

Este guia contém os comandos essenciais para gerenciamento remoto, verificação de estado, solução de problemas e backup de dispositivos Cisco IOS

## 1. Acesso Remoto (SSH & Telnet)
>Configuração e conexão segura (SSH) aos dispositivos

### Habilitar o SSH no Dispositivo
```bash
`1. Definir domínio`
(config)# ip domain-name minhaempresa.local
!(necessário para gerar chaves criptográficas)

`2. Gerar chaves criptográficas`
(config)# crypto key generate rsa

`3. Definir o nível de segurança e poder da chave`
[512]: 1024
!(mínimo 1024 bits para SSH v2)

`4. Criar usuário local`
!(config)# username admin privilege 15 secret [Senha]

`5. Configurar linhas VTY (0-4) para aceitar apenas SSH`
(config)# line vty 0 4
(config-line)# login local
(config-line)# transport input ssh
(config-line)# exit
!(O número da vty é a quantidade de acesso simultâneos que a porta suporta.
Usar os comandos "exec" e "logging" é de sua preferência)
```

### Habilitar o Telnet no Dispositivo
```bash
`1. Configurar linhas VTY (0-4) para habilitar Telnet`
(config)# line vty 0 4
(config-line)# password [Senha]
(config-line)# login
(config-line)# exit
!(O número da vty é a quantidade de acesso simultâneos que a porta suporta.
Usar os comandos "exec" e "logging" é de sua preferência)
```

### Comandos de Conexão (Cliente)
| Comando | Descrição |
|---------|-----------|
| ssh -l [usuário] [IP] | Conecta via SSH com o usuário específico |
| Telnet [IP] | Conecta via Telnet |
| Exit | Encerra a sessão remota |

## 2. Troubleshooting (Solução de Problemas)
> Comandos para diagnosticar falhas de conectividade e configuração

| Comando | Descrição |
|---------|-----------|
| ping [IP] | Testa conectividade ICMP (Camada 3) |
| traceroute [IP] | Rastreia o caminho até o destino (identifica onde o pacote morre) |

## 3. Verificação e Estado (Show Commands)
> Comandos para visualizar status de configurações, interfaces e protocolos

| Comando | Descrição |
|---------|-----------|
| show ip interface brief | Comando para mostrar os status UP/DOWN das interfaces e IPs configurados |
| show running-config | Comando para mostrar a configuração atual (memória RAM) |
| show startup-config | Comando para mostrar a configuração salva (memória NVRAM) |
| show cdp neighbors | Comando para mostrar dispositivos vizinhos Cisco de forma resumida (Nome, Porta, Equipamento) |
| show cdp neighbors detail | Comando para mostrar dispositivos vizinhos Cisco de forma detalhada (Nome, IP, Porta, Modelo) |
| show ip route | Comando para mostrar a tabela de roteamento (Rotas conectadas, estáticas e dinâmicas) |
| show vlan brief | Comando para mostrar as VLANs criadas e portas associadas |
| show mac address-table | Comando para mostrar a tabela MAC aprendida pelo Switch |
| show interfaces [tipo/n] | Comando para mostrar os detalhes físicos, contagem de erros e CRC |
| show version | Comando para exibir informações detalhadas sobre o hardware, software e status de funcionamento do dispositivo |

## 4. Backup e Restore (Flash e TFTP)
> Procedimento para salvar e restaurar as configurações e o IOS

### Backup e Restore Flash
```bash
`1. Criar uma cópia da sua configuração atual na Flash`
#copy run flash
[Running-config]? Yes [ou nome do arquivo]

`2. Recuperar a cópia na Flash para o próximo Boot`
#copy flash start
Source filename []? [nome do arquivo]
```

### Backup e Restore TFTP
> O comando `Show Flash` vai mostrar o espaço na Flash
```bash
`1. Criar um backup da RAM no servidor`
#copy run tftp
Address or name of remote host []? [IP do servidor]
Destination filename [Roteador-config]? [Nome do arquivo]
                ou
`1. Criar um backup da NVRAM no servidor`
#copy flash tftp
Source filename []? [Nome do arquivo]
Address or name of remote host []? [IP do servidor]
Destination filename []? [Nome dado ao arquivo]

`2. Recuperar a cópia direto na run`
#copy tftp run
Address or name of remote host []? [IP do servidor]
Source filename []? [Nome do arquivo]
Destination filename []? [Nome dado ao arquivo]
                   ou
`2. Recuperar a cópia direto na Flash`
#copy tftp flash
Address or name of remote host []? [IP do servidor]
Source filename []? [Nome do arquivo]
Destination filename []? [Nome dado ao arquivo]
```

---

🔗 **Navegação:** [← Voltar](./README.md) • [🏠 Início](../README.md) • [↑ Topo](#topo)
