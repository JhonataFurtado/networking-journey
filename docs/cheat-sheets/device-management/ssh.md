# Habilitar e configurar SSH

**1. Definir domínio**
```bash
(config)# ip domain-name minhaempresa.local
!(necessário para gerar chaves criptográficas)
```
**2. Gerar chaves criptográficas**
```bash
(config)# crypto key generate rsa modulus 2048
!(mínimo 1024 bits para SSH v2. 2048 é o recomendado hoje)   
```

**3. Forçar SSH versão 2**
```bash
(config)# ip ssh version 2
!(SSH v1 é inseguro, não use)
```

**4. Criar usuário local**
```bash
(config)# username admin privilege 15 secret [Senha]
```

5. Configurar linhas VTY (0-4) para aceitar apenas SSH
```bash
(config)# line vty 0 4
(config-line)# login local         
(config-line)# transport input ssh         
(config-line)# exit          
!(O número da vty é a quantidade de acesso simultâneos que a porta suporta.
Usar os comandos "exec" e "logging" é de sua preferência)
```

### Comandos de Conexão (Cliente)
| Comando | Descrição |
|---------|-----------|
| `ssh -l admin 192.168.1.1` | Conecta via SSH com o usuário específico |
| `ssh admin@192.168.1.1` | Sintaxe alternativa (mais comum) |
| `exit` ou `logout` | Encerra a sessão remota |
