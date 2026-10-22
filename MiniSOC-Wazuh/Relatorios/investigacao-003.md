# Investigação 003 — Consulta de rede com ipconfig.exe /all

## Objetivo

Criar uma regra para detectar a execução do `ipconfig.exe` com o parâmetro `/all`.

Esse comando permite visualizar informações detalhadas das interfaces de rede do Windows.

## Teste realizado

Executei no PowerShell:

```powershell
ipconfig.exe /all
```

A regra foi criada para verificar duas condições: o executável `ipconfig.exe` e a presença de `/all` na linha de comando.

## Dificuldades encontradas

Essa foi a regra que exigiu mais ajustes durante o projeto.

Inicialmente, o alerta não estava aparecendo como esperado. Para descobrir o problema, simplifiquei a regra e testei apenas a identificação do `ipconfig.exe`.

Depois que consegui gerar um alerta, adicionei novamente a condição referente ao parâmetro `/all`.

## Resultado

Após os ajustes, o Wazuh apresentou um novo alerta associado à regra 100112.

- **Regra:** 100112
- **Severidade:** 5
- **Agente:** Windows-Lab
- **Processo monitorado:** `ipconfig.exe`
- **Comando testado:** `ipconfig.exe /all`
- **Evento Sysmon:** ID 1 — Process Create
- **Data:** 19/10/2026
- **Novo alerta:** 16:59

O histórico também mostra um alerta anterior, registrado às 16:51, durante a fase de ajustes da regra.

## Análise

Essa detecção mostrou a importância de verificar separadamente as condições de uma regra quando ela não funciona como esperado.

A versão final foi configurada para identificar o `ipconfig.exe` quando a linha de comando contém `/all`.

O teste positivo gerou um alerta, mas não ficou documentada uma validação negativa conclusiva para confirmar que a configuração final ignora todas as execuções sem esse parâmetro.

Em um ambiente real, a execução do comando precisaria ser analisada junto com outros eventos para avaliar se existe algum comportamento suspeito.

## Evidências

- [Histórico dos alertas](../Evidencias/03-Ipconfig/03-historico-alertas-ipconfig.png)
- [Detalhes do comando durante os testes](../Evidencias/03-Ipconfig/03-detalhes-ipconfig.png)
- [Evento registrado pelo Sysmon](../Evidencias/03-Ipconfig/03-evento-sysmon-ipconfig.png)
- [Identificação da regra](../Evidencias/03-Ipconfig/03-identificacao-regra-ipconfig.png)

## Conclusão

Durante essa etapa, tive alguns problemas com a configuração da regra e precisei fazer ajustes até conseguir gerar o alerta esperado. Isso me ajudou a entender melhor como funcionam as condições e as expressões regulares no Wazuh.
