# Cálculo de Tempo em HH:MM:SS no Power BI

Este repositório contém um código DAX utilizado para calcular a soma de tempo em formato `HH:MM:SS` (horas, minutos e segundos) a partir de uma coluna que armazena valores de tempo no Power BI. O cálculo é realizado a partir de uma tabela chamada `BMM01` e uma coluna chamada `QTD`, que contém valores de tempo.

## Objetivo

Este código tem como objetivo somar os valores de tempo (em formato `HH:MM:SS`) presentes na coluna `QTD` da tabela `BMM01`, convertendo os totais para o formato `HH:MM:SS`, ou seja, exibindo o total de horas, minutos e segundos corretamente.

## Como Funciona o Código

O código DAX realiza o seguinte processo para calcular o tempo total:

1. **Converte o tempo (horas, minutos e segundos) para segundos:** A primeira etapa do cálculo consiste em somar os valores de tempo presentes na coluna `QTD`, convertendo cada unidade de tempo para segundos (horas para segundos, minutos para segundos e somando os segundos).

2. **Calcula o total de horas, minutos e segundos:** Após somar todos os segundos, o código converte o total de segundos de volta para horas, minutos e segundos, de forma a obter o total em um formato legível (HH:MM:SS).

3. **Retorna o valor no formato `HH:MM:SS`:** O código formata a saída de horas, minutos e segundos para garantir que cada valor tenha dois dígitos, mesmo que o valor seja menor que 10 (por exemplo, `02:05:03` em vez de `2:5:3`).

## Código DAX

Aqui está o código DAX utilizado para calcular o total de tempo em `HH:MM:SS`:

```DAX
TT HR 1 =  
VAR TOTALSegundos = 
    SUMX(
        BMM01, 
        HOUR(BMM01[QTD]) * 3600 +     -- Converte as horas para segundos
        MINUTE(BMM01[QTD]) * 60 +     -- Converte os minutos para segundos
        SECOND(BMM01[QTD])            -- Soma os segundos
    )
VAR Horas = INT(TOTALSegundos / 3600)  -- Converte os segundos totais para horas
VAR Minutos = INT(MOD(TOTALSegundos, 3600) / 60)  -- Calcula os minutos restantes
VAR Segundos = MOD(TOTALSegundos, 60)  -- Calcula os segundos restantes
RETURN 
    FORMAT(Horas, "00") & ":" & FORMAT(Minutos, "00") & ":" & FORMAT(Segundos, "00")

