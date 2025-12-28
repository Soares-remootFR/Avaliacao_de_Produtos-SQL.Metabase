<img width="1269" height="869" alt="Screenshot 2025-11-25 234812" src= https://github.com/Soares-remootFR/Avaliacao_de_Produtos-SQL.Metabase/tree/main/>

📊 Dashboard de Análise de Avaliações de Produtos (SQL)

Este projeto detalha o desenvolvimento de um painel analítico focado no monitoramento de avaliações de produtos (Product Reviews). O objetivo é utilizar a linguagem SQL para estruturar, relacionar e extrair indicadores de qualidade, volume e desempenho do portfólio de produtos.

Através de JOINS entre tabelas relacionais, o dashboard responde a perguntas críticas sobre a satisfação do cliente e a performance por categoria.

📸 Visualização do Painel

O dashboard final consolidado apresenta 6 cards estratégicos de análise.

(Substitua este caminho pelo print do seu dashboard final)

🗂️ Modelagem e Ambiente de Dados

Para a construção das análises, o ambiente foi preparado conectando-se a um banco de dados com duas tabelas principais:

1. Tabela Reviews (Fato)

Registra cada interação de avaliação feita pelo cliente.

  * Dados: ID da avaliação, Nota (Rating), Comentário, Data, ID do Produto.

2. Tabela Products (Dimensão)

Contém as características dos itens vendidos.

  *  Dados: ID do Produto, Título, Categoria, Preço.

Chave de Relacionamento: O vínculo entre as tabelas é feito pelo campo ID do Produto (Foreign Key), permitindo atribuir notas e comentários às categorias e nomes dos produtos.

📈 Detalhamento das Análises (Cards)

Abaixo, a lógica de negócio por trás de cada card e a consulta SQL desenvolvida.

Card 1: Média Geral de Avaliações

Monitora a "nota global" da empresa. Serve como termômetro geral da qualidade percebida.

    SELECT AVG(Rating) AS MediaAvaliacoes 
    FROM Reviews;


Card 2: Média de Avaliações por Categoria

Permite comparar quais segmentos de produtos (ex: Eletrônicos vs. Vestuário) têm melhor aceitação pelo público.

    SELECT 
        P.Category, 
        AVG(R.Rating) AS MediaAvaliacoes 
    FROM Reviews R 
    LEFT JOIN Products P ON R.ProductID = P.ProductID 
    GROUP BY P.Category;


Card 3: Top 10 Produtos (Melhores Avaliados)

Identifica os "campeões" de venda e satisfação. Estes itens são ideais para destaque em vitrines e campanhas de marketing.

    SELECT 
        P.ProductTitle, 
        AVG(R.Rating) AS MediaAvaliacoes 
    FROM Reviews R 
    LEFT JOIN Products P ON R.ProductID = P.ProductID 
    GROUP BY P.ProductID 
    ORDER BY MediaAvaliacoes DESC 
    LIMIT 10;


Card 4: Volume Total de Avaliações

Mede o engajamento bruto. Um volume baixo pode indicar problemas na jornada de pós-venda ou coleta de feedback.

    SELECT COUNT(*) AS TotalAvaliacoes 
    FROM Reviews;


Card 5: Sazonalidade (Avaliações por Mês)

Acompanha a evolução temporal para identificar picos de feedback, geralmente atrelados a grandes eventos (Black Friday, Natal).

    SELECT 
        DATE_FORMAT(R.ReviewDate, '%Y-%m') AS Mes, 
        COUNT(*) AS TotalAvaliacoes 
    FROM Reviews R 
    GROUP BY Mes;


Card 6: Cobertura de Portfólio (Produtos por Categoria)

Verifica a amplitude do feedback. Mostra quantos produtos distintos dentro de uma categoria receberam ao menos uma avaliação.

    SELECT 
        P.Category, 
        COUNT(DISTINCT R.ProductID) AS QtdProdutos 
    FROM Reviews R 
    LEFT JOIN Products P ON R.ProductID = P.ProductID 
    GROUP BY P.Category;


🧠 Valor Estratégico e Tomada de Decisão

A implementação deste dashboard permite à gestão:

  *  Identificar Produtos Problemáticos: Agir rapidamente em itens com média baixa para evitar devoluções (Churn).

  *  Entender a Sazonalidade: Preparar a equipe de suporte para meses com picos históricos de avaliações.

  *  Validar o Mix de Produtos: Analisar se categorias novas estão performando conforme o esperado em comparação com categorias maduras.

🚀 Melhorias Futuras

Para evoluir este projeto, sugere-se:

  *  [ ] Adicionar gráficos de linha para visualizar a tendência da nota média ao longo do tempo.

  *  [ ] Cruzar os dados de avaliações com dados financeiros (Faturamento x Satisfação).

  *  [ ] Implementar filtros dinâmicos por período de tempo no front-end.

👤 Autor

Projeto Desenvolvido por: Fábio R Soares
