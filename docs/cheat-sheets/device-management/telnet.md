# Habilitar e configurar telnet
> Telnet envia credenciais em texto puro, por isso use apenas em laboratórios ou redes isoladas. Para produção, use SSH.

**1. Configurar linhas VTY (0-4) para habilitar Telnet**
```bash
(config)# line vty 0 4
(config-line)# password [Senha]
(config-line)# login
(config-line)# transport input telnet
(config-line)# exit
!(O número da vty é a quantidade de acessos simultâneos que a porta suporta.
Usar os comandos "exec" e "logging" é opcional)
```

### Comandos de Conexão (Cliente)
| Comando | Descrição |
|---------|-----------|
| `telnet 192.168.1.1` | Conecta via Telnet |
| `exit` ou `logout` | Encerra a sessão remota |
