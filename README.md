# SQL-Projects
Nesse repositório você vai encontrar projetos relacionados à BI que desenvolvi enquanto atuava como Estagiário de Supply Chain em uma Startup que atuava no mercado de segurança em São Paulo, por meio de um Aplicativo.
Abaixo alguns exemplos.

<img width="891" alt="image" src="https://github.com/AlessandroMacabu/SQL-Projects/assets/132486411/995b81c9-590b-4eeb-becf-b22a3d68a36c">
<img width="824" alt="image" src="https://github.com/AlessandroMacabu/SQL-Projects/assets/132486411/b563b4be-f107-4233-bcfb-0c6f246a0b54">



SELECT
  u.phone as embaixador_phone,
  u.name as embaixador_name,
  u.user_id as embaixador_user_id,
  u.pix_key,
  COALESCE(total_events, 0) events,
  COALESCE(aus.event_price, 0) total_price
FROM dim_users u
--APROVED UGC SUBMISSIONS:
LEFT JOIN (
    SELECT
      count(e.event_id) total_events,
	  sum(2.5) as event_price, -- R$2,50 é o preço por evento
      s.creator_user_id as author_id
    FROM fact_submissions s
    LEFT JOIN dim_events e on e.event_id = s.event_id
    WHERE e.deleted_at is null
    AND s.status_id = 4
    
    AND e.created_at >= date_trunc('week', now() - (INTERVAL '1 week'))
    AND e.created_at < date_trunc('week', now()) 
    GROUP BY 3
    ) aus on aus.author_id = u.user_id
AND u.user_type_id = 6
WHERE u.user_type_id = 6
order by total_price desc



<img width="948" alt="image" src="https://github.com/AlessandroMacabu/SQL-Projects/assets/132486411/c12bc974-a800-44d5-9c1d-e40ea0f755b5">
<img width="953" alt="image" src="https://github.com/AlessandroMacabu/SQL-Projects/assets/132486411/27f77914-7739-45fb-92fd-98840ac1a724">



