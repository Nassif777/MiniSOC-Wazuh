# Investigação 002 — Consulta de usuários com net.exe

## Objetivo

Criar uma regra para identificar quando o comando `net.exe user` fosse executado no Windows.

Esse comando permite consultar contas de usuários locais. Assim como o `whoami.exe`, pode ser utilizado em atividades administrativas ou durante o reconhecimento de um computador.

## Teste realizado

Executei no PowerShell:

```powershell
net.exe user
```

A regra foi configurada para verificar o executável `net.exe` e procurar a palavra `user` na linha de comando.

## Resultado

Após executar o comando, o Wazuh gerou o alerta esperado.

As principais informações registradas foram:

- **Regra:** 100111
- **Severidade:** 5
- **Agente:** Windows-Lab
- **Processo:** `C:\Windows\System32\net.exe`
- **Linha de comando:** `net.exe user`
- **Processo de origem:** `powershell.exe`
- **Evento Sysmon:** ID 1 — Process Create
- **Data:** 19/10/2026
- **Horário do alerta:** 16:29

## Análise

Diferentemente da primeira regra, essa detecção utiliza duas condições.

A primeira verifica se o processo executado é o `net.exe`. A segunda procura a palavra `user` na linha de comando.

Isso permite tornar a detecção mais específica do que simplesmente monitorar qualquer execução do `net.exe`.

Porém, a presença desse comando não significa necessariamente que houve um ataque. A regra também pode detectar atividades legítimas.

## Evidências

- [Alerta no Wazuh](../Evidencias/02-Net-User/02-alerta-net-user.png)
- [Detalhes do processo](../Evidencias/02-Net-User/02-detalhes-net-user.png)
- [Evento registrado pelo Sysmon](../Evidencias/02-Net-User/02-evento-sysmon-net-user.png)
- [Identificação da regra](../Evidencias/02-Net-User/02-identificacao-regra-net-user.png)

## Conclusão

O teste gerou o alerta esperado, confirmando o funcionamento da detecção para o comando utilizado.

Com essa regra, consegui praticar a utilização de mais de uma condição para identificar uma atividade específica.
