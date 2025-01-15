# soma-de-horas-no-powerbi.
Repositório com código DAX para somar horas no Power BI.

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
