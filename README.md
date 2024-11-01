# Gráfico para mapeamento de quantidade de ligações atendidas, categorizadas por canal, no primeiro trimestre de 2022
SELECT

    leads_basic_details.lead_id AS lead_basic,
    leads_basic_details.lead_gen_source,
    leads_interaction_details.lead_id AS lead_interaction,
    leads_interaction_details.lead_stage,
    leads_interaction_details.call_done_date,
    leads_interaction_details.call_status,
    
# contagem de ligações por plataforma

    count (lead_gen_source),
    
# filtro de período de mapeamento

    YEAR(leads_interaction_details.call_done_date) AS year,
    
    MONTH(leads_interaction_details.call_done_date) AS month
FROM leads_basic_details

# união das duas bases por meio de uma coluna em comum 

LEFT JOIN leads_interaction_details ON leads_interaction_details.lead_id = leads_basic_details.lead_id

# filtrar os dados no período analisado

WHERE leads_interaction_details.call_done_date BETWEEN '2022-01-01' AND '2022-03-31'

# agrupar os dados pelo mês e ano

group by 

    YEAR(leads_interaction_details.call_done_date),
    MONTH(leads_interaction_details.call_done_date),
    leads_basic_details.lead_id,
    leads_basic_details.lead_gen_source,
    leads_interaction_details.lead_id,
    leads_interaction_details.lead_stage,
    leads_interaction_details.call_done_date,
    leads_interaction_details.call_status

    ---------------------------------------------------------------------------------------------------------------------------------
# Tabela para média porcentual de Watched por idioma

select
    language, AVG(watched_percentage) AS PORCENTAGEM
from leads_demo_watched_details

# Criação de filtro : considerados valores acima de 0.5
where watched_percentage > 0.5

# Agrupamento por idioma
GROUP BY language

# Ordenação decrescente por idioma 
ORDER BY language por idioma

---------------------------------------------------------------------------------------------------------------------------------------------------------
# Gráfico de barras de quantidade por educação, por curso
SELECT
    lead_id, current_education,
# Contagem de quantidade por curso
    COUNT (current_education) as Qtd_por_educação
from leads_basic_details
# Agrupamento e Ordenação
GROUP BY current_education
ORDER BY Qtd_por_educação asc

---------------------------------------------------------------------------------------------------------------------------------------------------
# Cartão foi criado para apresentação da média de idade dos alunos, sendo o resultado desta query:
SELECT 
  ROUND (avg (age),0) as Media
from leads_basic_details
-- avg sendo código para cálculo de média. Neste caso, usamos para cálculo da média de idade dos alunos --

---------------------------------------------------------------------------------------------------------------------------------------------------------
# Gráfico de setores apresentou a quantidade por gênero e, para isso, utilizamos a query a seguir:
SELECT gender, COUNT(*) as Qtd_por_gênero
From leads_basic_details
GROUP BY gender
Order By Qtd_por_genero

-- count para contagem da quantidade por gênero. Então, além da quantidade total de alunos, tempos a categorização e separação por gênero --



