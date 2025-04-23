# PowerShell para Analistas de Segurança

---

## 1. **Introdução ao PowerShell**
O PowerShell é um shell de linha de comando e linguagem de script poderosa desenvolvida pela Microsoft, projetada especificamente para administração de sistemas. É baseado na plataforma .NET e amplamente utilizado para automatizar tarefas, gerenciar configurações e executar atividades administrativas em sistemas Windows e Linux.

### Por que analistas de segurança devem aprender PowerShell?
- **Automação e Eficiência**: Automatiza tarefas repetitivas como análise de logs, auditorias de sistema e monitoramento de segurança.
- **Resposta a Incidentes**: Coleta rápida de artefatos forenses, investigação de atividades suspeitas e resposta a incidentes.
- **Threat Hunting (Caça a Ameaças)**: Identifica comportamentos anômalos consultando informações do sistema e logs de eventos.
- **Red Team e Blue Team**: Utilizado por atacantes para persistência e movimentação lateral, tornando essencial que defensores compreendam suas capacidades.

---

## 2. **Visão Geral dos Cmdlets, Scripts e Ambiente PowerShell**

### 2.1 **Cmdlets**
- Cmdlets (pronuncia-se "command-lets") são os blocos de construção do PowerShell. São comandos leves que realizam operações específicas.
- **Sintaxe**: `Verbo-Substantivo` (ex.: `Get-Process`, `Set-Item`, `New-User`)
- **Exemplo**:
    ```powershell
    Get-Process          # Lista todos os processos em execução
    Get-Service          # Exibe todos os serviços do sistema
    Get-EventLog -LogName Security  # Recupera logs de eventos de segurança
    ```

### 2.2 **Scripts**
- Scripts são arquivos de texto contendo uma série de comandos PowerShell salvos com a extensão `.ps1` por padrão.
- Permitem a automação de tarefas complexas executando múltiplos cmdlets em sequência.
- **Exemplo de Script (`Get-SystemInfo.ps1`)**:
    ```powershell
    # Obter informações do sistema
    Get-ComputerInfo
    Get-Process | Where-Object {$_.CPU -gt 100}  # Processos com alto uso de CPU
    Get-EventLog -LogName Security -Newest 10
    ```

### 2.3 **O Ambiente PowerShell**
- **Console e ISE**: O PowerShell pode ser executado no console tradicional ou no Ambiente Integrado de Script (ISE - Integrated Script Environment).
- **Módulos**: Pacotes que contêm cmdlets, funções, variáveis e outros recursos.
- **Pipeline (`|`)**: Usado para passar a saída de um cmdlet como entrada para outro.
    ```powershell
    Get-Process | Where-Object {$_.CPU -gt 50} | Select-Object ProcessName, CPU
    ```

---

## 3. **Compreendendo a Execution Policy**
A Execution Policy no PowerShell define as condições sob as quais arquivos de configuração e scripts são carregados e executados.

### Tipos de Execution Policy
1. **Restricted**: Configuração padrão, não permite execução de scripts.
2. **AllSigned**: Apenas scripts assinados por um editor confiável podem ser executados.
3. **RemoteSigned**: Scripts locais são permitidos; os da internet precisam ser assinados.
4. **Unrestricted**: Scripts são executados sem restrições.
5. **Bypass**: Sem restrições; usado para automação.

### Verificando e Definindo Execution Policy
```powershell
Get-ExecutionPolicy        # Verifica a policy atual
Set-ExecutionPolicy RemoteSigned   # Define como RemoteSigned
```

### Boa Prática para Analistas de Segurança
- Sempre defina a política como RemoteSigned ou AllSigned para evitar execução não autorizada de scripts.
- Use Bypass apenas em ambientes controlados, como para scripts de resposta a incidentes.
- Definir politicas mais restritivas não necessáriamente impedem a execução de scripts, mas evita que usuários desavisados carrem um script sem querer.

---

## 4. Casos de Uso para Analistas de Segurança

### 4.1 Resposta a Incidentes
- Coleta de logs e artefatos do sistema para análise forense.
```powershell
Get-EventLog -LogName Security -Newest 100 | Export-Csv C:\Logs\SecurityLogs.csv
```

### 4.2 Threat Hunting
- Identificação de processos suspeitos ou atividade de rede incomum.
```powershell
Get-Process | Where-Object { $_.CPU -gt 80 }
Get-NetTCPConnection | Where-Object { $_.RemotePort -eq 4444 }
```

### 4.3 Avaliação de Vulnerabilidades
- Verificação de patches de segurança ausentes.
```powershell
Get-HotFix | Where-Object { $_.InstalledOn -lt (Get-Date).AddMonths(-6) }
```

### 4.4 Auditorias de Segurança e Conformidade
- Auditoria de contas de usuários e permissões.
```powershell
Get-LocalUser
Get-LocalGroupMember -Group "Administrators"
```

### 4.5 Automação e Scripts
- Automatização de tarefas repetitivas de segurança como limpeza de logs ou verificação de integridade do sistema.
```powershell
Get-EventLog -LogName Application -EntryType Error -Newest 50 | Out-File C:\Logs\ErrorLogs.txt
```

---

## 5. Fundamentos do PowerShell

### 5.1 Comandos Básicos
```powershell
Get-Help Get-Process   # Exibe ajuda para um cmdlet
Get-Command            # Lista todos os cmdlets disponíveis
Get-Module             # Lista todos os módulos importados
```

### 5.2 Variáveis e Tipos de Dados
```powershell
$Name = "Analista de Segurança"
$Number = 42
$Array = @(1, 2, 3, 4)
```

### 5.3 Laços e Condicionais
```powershell
# Estrutura If-Else
$CPUUsage = Get-Process | Where-Object { $_.CPU -gt 80 }
If ($CPUUsage) {
    Write-Host "Uso elevado de CPU detectado"
} Else {
    Write-Host "Uso de CPU normal"
}

# Laço ForEach
$Processes = Get-Process
ForEach ($Process in $Processes) {
    Write-Host $Process.ProcessName
}
```

### 5.4 Funções
```powershell
Function Get-HighCPU {
    Param($Threshold = 50)
    Get-Process | Where-Object { $_.CPU -gt $Threshold }
}
Get-HighCPU -Threshold 80
```

---

## 6. Guia Rápido de Comandos PowerShell para Analistas de Segurança

### 6.1 Informações do Sistema
```powershell
Get-ComputerInfo                    # Informações do sistema
Get-WmiObject Win32_OperatingSystem  # Informações detalhadas do SO
```

### 6.2 Monitoramento de Processos e Serviços
```powershell
Get-Process                         # Lista processos em execução
Get-Service                         # Lista serviços instalados
Stop-Process -Name "notepad"         # Encerra um processo
```

### 6.3 Informações de Rede
```powershell
Get-NetAdapter                      # Informações dos adaptadores de rede
Get-NetTCPConnection                 # Conexões de rede ativas
```

### 6.4 Análise de Logs de Eventos
```powershell
Get-EventLog -LogName Security -Newest 100
Get-WinEvent -LogName Application -MaxEvents 50
```

### 6.5 Gerenciamento de Arquivos e Diretórios
```powershell
Get-ChildItem -Path C:\Logs -Recurse  # Lista todos os arquivos no diretório
Remove-Item -Path C:\Logs\*.log       # Remove todos os arquivos de log
```

### 6.6 Auditoria de Usuários e Permissões
```powershell
Get-LocalUser                        # Lista todos os usuários locais
Get-LocalGroup                       # Lista todos os grupos locais
Get-LocalGroupMember -Group "Admins"  # Lista membros do grupo de administradores
```

---

## 7. Resumo
- O PowerShell é uma ferramenta versátil e poderosa para analistas de segurança.
- Utilize cmdlets para auditorias de sistema, resposta a incidentes e caça a ameaças.
- Use scripts para automatizar tarefas repetitivas de segurança.
- Configure políticas de execução de forma segura (preferencialmente RemoteSigned).
- Sempre revise e compreenda os scripts antes de executá-los para evitar atividades maliciosas.
- Mantenha-se em constante aprendizado para acompanhar as técnicas de atacantes.

~~~~~~

# PowerShell for Security Analysts

---

## 1. **Introduction to PowerShell**
PowerShell is a powerful command-line shell and scripting language developed by Microsoft, designed specifically for system administration. It is built on the .NET framework and is widely used for automating tasks, managing configurations, and performing administrative tasks on both Windows and Linux systems.

### Why Should Security Analysts Learn PowerShell?
- **Automation and Efficiency**: Automate repetitive tasks such as log analysis, system audits, and security monitoring.
- **Incident Response**: Quickly collect forensic artifacts, investigate suspicious activities, and respond to incidents.
- **Threat Hunting**: Identify anomalous behaviors by querying system information and event logs.
- **Red Teaming and Blue Teaming**: Used by attackers for persistence and lateral movement, making it crucial for defenders to understand its capabilities.

---

## 2. **Overview of Cmdlets, Scripts, and the PowerShell Environment**

### 2.1 **Cmdlets**
- Cmdlets (pronounced "command-lets") are the building blocks of PowerShell. They are lightweight commands that perform specific operations.
- **Syntax**: `Verb-Noun` (e.g., `Get-Process`, `Set-Item`, `New-User`)
- **Example**:
    ```powershell
    Get-Process          # Lists all running processes
    Get-Service          # Displays all services on the system
    Get-EventLog -LogName Security  # Retrieves security event logs
    ```

### 2.2 **Scripts**
- Scripts are text files containing a series of PowerShell commands saved with the `.ps1` extension.
- They allow automation of complex tasks by executing multiple cmdlets in sequence.
- **Example Script (`Get-SystemInfo.ps1`)**:
    ```powershell
    # Get System Information
    Get-ComputerInfo
    Get-Process | Where-Object {$_.CPU -gt 100}  # High CPU usage processes
    Get-EventLog -LogName Security -Newest 10
    ```

### 2.3 **The PowerShell Environment**
- **Console and ISE**: PowerShell can be executed from the traditional console or the Integrated Scripting Environment (ISE).
- **Modules**: Packages containing cmdlets, functions, variables, and other resources.
- **Pipeline (`|`)**: Used to pass output from one cmdlet as input to another.
    ```powershell
    Get-Process | Where-Object {$_.CPU -gt 50} | Select-Object ProcessName, CPU
    ```

---

## 3. **Understanding the Execution Policy**
Execution Policy in PowerShell determines the conditions under which PowerShell loads configuration files and runs scripts.

### Types of Execution Policies
1. **Restricted**: Default setting, allows no scripts to run.
2. **AllSigned**: Only scripts signed by a trusted publisher can be run.
3. **RemoteSigned**: Local scripts can run, but scripts downloaded from the internet must be signed.
4. **Unrestricted**: Scripts are allowed to run without restrictions.
5. **Bypass**: No restrictions; used for automation.

### Checking and Setting Execution Policy
```powershell
Get-ExecutionPolicy        # Check current execution policy
Set-ExecutionPolicy RemoteSigned   # Set to RemoteSigned
```

###Best Practice for Security Analysts
- Always set the policy to RemoteSigned or AllSigned to prevent unauthorized scripts from running.
- Use Bypass only in controlled environments, such as for incident response scripts.

## 4. Use Cases for Security Analysts
### 4.1 Incident Response
- Collect logs and system artifacts for forensic analysis.
```powershell
Get-EventLog -LogName Security -Newest 100 | Export-Csv C:\Logs\SecurityLogs.csv
```

### 4.2 Threat Hunting
- Identify suspicious processes or unusual network activity.
```powershell
Get-Process | Where-Object { $_.CPU -gt 80 }
Get-NetTCPConnection | Where-Object { $_.RemotePort -eq 4444 }
```

### 4.3 Vulnerability Assessment
- Check for missing security patches.
```powershell
Get-HotFix | Where-Object { $_.InstalledOn -lt (Get-Date).AddMonths(-6) }
```

### 4.4 Security Audits and Compliance
- Audit user accounts and permissions.
```powershell
Get-LocalUser
Get-LocalGroupMember -Group "Administrators"
```

### 4.5 Automation and Scripting
- Automate repetitive security tasks like log cleanup or system health checks.
```powershell
Get-EventLog -LogName Application -EntryType Error -Newest 50 | Out-File C:\Logs\ErrorLogs.txt
```
## 5. PowerShell Basics
### 5.1 Basic Commands
```powershell
Get-Help Get-Process   # Display help for a cmdlet
Get-Command            # List all available cmdlets
Get-Module             # List all imported modules
```

### 5.2 Variables and Data Types
```powershell
$Name = "Security Analyst"
$Number = 42
$Array = @(1, 2, 3, 4)
```

### 5.3 Loops and Conditionals
```powershell
# If-Else Statement
$CPUUsage = Get-Process | Where-Object { $_.CPU -gt 80 }
If ($CPUUsage) {
    Write-Host "High CPU Usage Detected"
} Else {
    Write-Host "CPU Usage is Normal"
}

# ForEach Loop
$Processes = Get-Process
ForEach ($Process in $Processes) {
    Write-Host $Process.ProcessName
}
```

### 5.4 Functions
```powershell
Function Get-HighCPU {
    Param($Threshold = 50)
    Get-Process | Where-Object { $_.CPU -gt $Threshold }
}
Get-HighCPU -Threshold 80
```

## 6. PowerShell Command Cheatsheet for Security Analysts
### 6.1 System Information
```powershell
Get-ComputerInfo                    # System Information
Get-WmiObject Win32_OperatingSystem  # Detailed OS Information
```

### 6.2 Process and Service Monitoring
```powershell
Get-Process                         # List Running Processes
Get-Service                         # List Installed Services
Stop-Process -Name "notepad"         # Stop a 
```
### 6.3 Network Information
```powershell
Get-NetAdapter                      # Network Adapter Information
Get-NetTCPConnection                 # Active Network Connections
```

### 6.4 Event Log Analysis
```powershell
Get-EventLog -LogName Security -Newest 100
Get-WinEvent -LogName Application -MaxEvents 50
```

### 6.5 File and Directory Management
```powershell
Get-ChildItem -Path C:\Logs -Recurse  # List all files in a directory
Remove-Item -Path C:\Logs\*.log       # Delete all log files
```

### 6.6 User and Permissions Auditing
```powershell
Get-LocalUser                        # List all Local Users
Get-LocalGroup                       # List all Local Groups
Get-LocalGroupMember -Group "Admins"  # List Admin Group Members
```

## 7. Summary
- PowerShell is a versatile and powerful tool for Security Analysts.
- Use cmdlets to perform system audits, incident response, and threat hunting.
- Leverage scripts for automation of repetitive security tasks.
- Set execution policies securely (preferably RemoteSigned).
- Always review and understand scripts before execution to prevent malicious activities.
- Continuously learn and update your PowerShell skills to stay ahead of attackers.

