# **Dia#1: Introdução à Análise de Logs**

## **Objetivo:**
O objetivo deste laboratório é introduzir os alunos aos conceitos básicos de **análise de logs** e demonstrar como logs de diferentes sistemas podem ser coletados, analisados e utilizados para monitoramento de segurança. Os alunos aprenderão a gerar logs simples em sistemas Windows e Linux, além de como analistas de SOC utilizam esses registros para detectar incidentes de segurança.

---
## **▶️Vídeo Tutorial**

[![▶️Assista ao vídeo](https://img.youtube.com/vi/kzEutcdJVMw/maxresdefault.jpg)](https://youtu.be/kzEutcdJVMw)

---
## **O que é um Log?**
Um **log** é um registro de eventos em um sistema que captura ações importantes como erros, alertas ou atividades de usuários. Esses logs contêm informações essenciais, como:
- **Timestamp**
- **Descrição do Evento**
- **Severidade (Crítico, Erro, Aviso, Informação)**
- **Fonte (Usuário, Processo, Serviço)**

Logs são essenciais para compreender o comportamento do sistema, detectar incidentes de segurança e realizar investigações forenses.

---
## **Exemplos de logs**

🐧Exemplo de auth.log no Linux
```
Apr  7 10:42:15 ubuntu sshd[12345]: Failed password for invalid user admin from 192.168.1.100 port 54321 ssh2
```
Explicação:
- `Apr 7 10:42:15` — Timestamp
- `ubuntu` — Nome do host
- `sshd[12345]` — Nome do serviço e ID do processo
- `Failed password for invalid user admin` — Tentativa de login falha
- `from 192.168.1.100` — Endereço IP de origem
- `port 54321` — Porta de origem
- `ssh2` — Versão do protocolo

## **Fontes de Logs no Linux:**
- **Logs do Sistema:** Armazenados em `/var/log/`, incluindo arquivos como `syslog` (mensagens do sistema), `auth.log` (tentativas de autenticação) e `kern.log` (logs relacionados ao kernel).
- **Logs de Aplicações:** Logs específicos de aplicações, como Apache (`/var/log/apache2/access.log`) ou MySQL (`/var/log/mysql/error.log`).

### **Fontes de Logs no Windows:**
- **Visualizador de Eventos:** Permite acesso a logs como:
  - **System Logs**: Relacionados a eventos do sistema operacional.
  - **Security Logs**: Relacionados a tentativas de login, alterações de permissões, etc.
  - **Application Logs**: Relacionados a aplicações do sistema.
  - **PowerShell Logs**: Relacionados à execução de comandos PowerShell, incluindo execuções suspeitas.

---
## **Como um Analista de SOC utiliza a Análise de Logs?**
- **Detecção de Incidentes:** Analistas de SOC revisam logs para detectar atividades incomuns ou não autorizadas, como tentativas de login falhas ou processos suspeitos.
- **Forense:** Logs são usados para rastrear as ações realizadas por um invasor durante ou após um incidente.
- **Monitoramento de Segurança:** A análise contínua de logs auxilia na detecção de ameaças em tempo real.
- **Conformidade:** Logs ajudam a manter a conformidade com normas regulatórias (ex: GDPR, HIPAA).

---
## **Ferramentas Populares para Análise de Logs:**
- **ELK Stack (Elasticsearch, Logstash, Kibana):** Conjunto poderoso para coleta, armazenamento e visualização de logs.
- **Splunk:** Ferramenta líder para busca, análise e visualização de dados gerados por máquinas.
- **Graylog:** Solução open-source para gerenciamento de logs.
- **Wazuh:** Plataforma open-source de monitoramento de segurança que se integra bem ao ELK para análise de logs e detecção de ameaças.

---
## **Tarefa de Laboratório: Simulação e Detecção de Eventos do PowerShell no Windows**

## **Configuração do Laboratório**
### **Requisitos:**
- **Sistemas:** Windows 10/11 ou Windows Server 2019/2022, Linux (Ubuntu ou CentOS)
- **Ferramentas:**
  - **Visualizador de Eventos do Windows**
  - **PowerShell (Pré-instalado no Windows)**

---
## **Preparação:**
Para este laboratório, será necessário configurar a coleta de logs tanto em sistemas Windows quanto Linux. Siga os passos abaixo para garantir que tudo esteja pronto:

### **No Windows:**
1. Abra o **Editor de Diretiva de Grupo** (`gpedit.msc`):
   - Navegue até `Configuração do Computador > Modelos Administrativos > Componentes do Windows > Windows PowerShell`.
   - Certifique-se de que as opções **Module Logging**, **Script Block Logging** e **Script Execution** estejam habilitadas.

2. Abra o **Visualizador de Eventos**:
   - Acesse **Applications and Services Logs → Microsoft → Windows → PowerShell → Operational**.

### **Passo 1: Simular um Comando PowerShell Suspeito**
Para simular uma atividade suspeita, abra uma sessão do PowerShell com privilégios elevados e execute o seguinte comando:
```powershell
Get-LocalUser | Select-Object Name, Enabled
```
Esse comando lista todas as contas de usuários locais no sistema, o que pode ser usado por invasores para enumerar usuários após uma exploração.

### **Passo 2: Detectar o Log no Visualizador de Eventos do Windows**
1. Pressione `Win + R`, digite `eventvwr.msc` e pressione Enter.

2. Navegue até:
   `Applications and Services Logs → Microsoft → Windows → PowerShell → Operational.`

3. Clique em "Filtrar Log Atual" e filtre pelo ID de Evento **4104** (que registra a execução de scripts PowerShell).

4. Procure por uma entrada que mostre a execução do comando `Get-LocalUser`.

5. Tire um print da tela com os detalhes do evento.

## **Conclusão:**
- **Entendimento da Análise de Logs:** Logs são cruciais para detectar, investigar e responder a incidentes de segurança. Por meio do Visualizador de Eventos do Windows e dos arquivos de log do Linux, é possível monitorar atividades do sistema e identificar possíveis problemas de segurança.

- **Papel do Analista de SOC:** Analistas de SOC utilizam a análise de logs para detectar ameaças, investigar incidentes e garantir a conformidade dos sistemas.

### **Entrega:**
- **Logs do Windows:** Enviar uma captura de tela do log gerado na máquina Windows.
