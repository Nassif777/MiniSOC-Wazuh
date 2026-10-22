# Investigação 001 — Execução do whoami.exe

## Objetivo

Criar uma regra no Wazuh para identificar quando o comando `whoami.exe` fosse executado no Windows.

Esse comando mostra qual usuário está executando um processo. Ele é utilizado normalmente por administradores, mas também pode aparecer durante o reconhecimento de um sistema.

## Teste realizado

No PowerShell do Windows, executei:

```powershell
whoami.exe
```

O Sysmon registrou a criação do processo e o Wazuh recebeu o evento por meio do agente instalado no Windows.

## Resultado

O Wazuh gerou um alerta com as seguintes informações:

- **Regra:** 100110
- **Severidade:** 5
- **Agente:** Windows-Lab
- **Processo:** `C:\Windows\System32\whoami.exe`
- **Processo de origem:** `powershell.exe`
- **Evento Sysmon:** ID 1 — Process Create
- **Data:** 19/10/2026
- **Horário do alerta:** 16:12

O alerta apareceu no Threat Hunting do Wazuh e foi possível consultar os detalhes do processo executado.

## Análise

A regra funcionou como esperado e identificou a execução do comando.

O `whoami.exe` não é malicioso por si só. Para considerar essa atividade suspeita em um ambiente real, seria necessário analisar o contexto da execução, o usuário responsável e outras atividades relacionadas.

Neste caso, o comando foi executado por mim para testar a detecção.

## Evidências

- [Alerta no Wazuh](../Evidencias/01-Whoami/01-alerta-whoami.png)
- [Detalhes do processo](../Evidencias/01-Whoami/01-detalhes-whoami.png)
- [Evento registrado pelo Sysmon](../Evidencias/01-Whoami/01-evento-sysmon-whoami.png)
- [Identificação da regra](../Evidencias/01-Whoami/01-identificacao-regra-whoami.png)

## Conclusão

Consegui detectar a execução do `whoami.exe` utilizando uma regra personalizada no Wazuh.

Esse primeiro teste também ajudou a entender como os eventos do Sysmon são enviados ao servidor e como consultar as informações de um alerta.
