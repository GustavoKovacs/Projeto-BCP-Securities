Segue o meu código em SQL para revisão abaixo.

-- 1. Retorne a quantidade de debêntures listadas no dia anterior
SELECT COUNT(*) AS quantidade_debentures
FROM debentures
WHERE data = (SELECT MAX(data) FROM debentures WHERE data < CURRENT_DATE);

-- 2. Retorne a duration média de todas as debêntures em cada um dos últimos 5 dias úteis
WITH base AS (
    SELECT DISTINCT data AS data,
           AVG(duration) AS duration,
           EXTRACT(DAYOFWEEK FROM data) AS diasemana
    FROM your_table_name
    GROUP BY data
)
SELECT *
FROM base
WHERE diasemana != 1 AND diasemana != 7
ORDER BY data DESC
LIMIT 5;

-- 3. Busque os códigos únicos de todas as debêntures da empresa “VALE S/A”
SELECT DISTINCT codigo
FROM debentures
WHERE nome LIKE '%VALE S/A%';
