# 📘 Introdução aos Logs do Linux + Guia Rápido

Os logs do Linux são essenciais para **monitoramento do sistema, depuração, solução de problemas e análise de segurança**. Compreender como acessá-los e interpretá-los é uma habilidade fundamental para administradores de sistemas, engenheiros de DevOps e analistas de segurança.

---

## 📂 Onde os Logs do Linux São Armazenados?

A maioria dos logs no Linux é armazenada no diretório `/var/log/`.

---

## 📄 Arquivos de Log Comuns

| Arquivo de Log                    | Descrição                                           |
|----------------------------------|-----------------------------------------------------|
| `/var/log/syslog` / `messages`   | Logs gerais de atividades do sistema               |
| `/var/log/auth.log`              | Logs de autenticação (login, sudo, ssh)            |
| `/var/log/kern.log`              | Mensagens do kernel                                 |
| `/var/log/dmesg`                 | Mensagens do boot e relacionadas ao hardware        |
| `/var/log/faillog`               | Tentativas de login fracassadas                     |
| `/var/log/secure`                | Logs relacionados à segurança (RHEL/CentOS)         |
| `/var/log/boot.log`              | Logs de inicialização do sistema                    |
| `/var/log/cron` ou `cron.log`    | Logs de agendamento de tarefas (cron)              |
| `/var/log/httpd/`                | Logs do servidor web Apache                         |
| `/var/log/audit/`                | Logs do SELinux e do AuditD                         |

---

## 🧠 Guia Rápido de Logs no Linux

### 🔍 Visualizar Logs

```bash
cat /var/log/syslog              # Exibe todo o log
less /var/log/auth.log           # Navega pelos logs com rolagem
tail -f /var/log/syslog          # Monitoramento ao vivo dos logs
journalctl                       # Visualiza logs do journal do systemd
```

### 📌 Filtrar Logs

```bash
grep "error" /var/log/syslog                     # Busca por 'error'
journalctl -u ssh                                # Logs do serviço SSH
journalctl --since "1 hour ago"                  # Logs da última hora
journalctl --since "2024-10-01" --until "2024-10-02"  # Logs entre duas datas
```

### 🛠️ Comandos Úteis para Gerenciamento de Logs

```bash
dmesg | less                        # Visualiza o buffer do kernel
logrotate -d /etc/logrotate.conf   # Testa a rotação de logs
last                               # Mostra histórico de logins
lastb                              # Mostra tentativas de login fracassadas
```

### 🧾 Exemplo: Detectar Tentativas de Login SSH Fracassadas

```bash
grep "Failed password" /var/log/auth.log
```

### 🔐 Por Que os Logs São Importantes?

- 🔍 Monitoramento de Segurança – Detecta ataques de força bruta e logins não autorizados.
- 🛠️ Solução de Problemas – Identifica erros de serviços e falhas no sistema.
- 📜 Auditoria – Rastreia atividades de usuários e alterações no sistema.
