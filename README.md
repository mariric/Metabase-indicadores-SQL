# Criação de gráfico para mapeamento de quantidade de ligações atendidas, categorizadas por canal, no primeiro trimestre de 2022
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
