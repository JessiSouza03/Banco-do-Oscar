# Projeto de Banco de Dados para Oscar

Esta atividade envolve a criação e manipulação de um banco de dados relacionado ao Oscar, com consultas específicas para análise de dados sobre indicados e vencedores do prêmio.

## Estrutura do Banco de Dados

O banco de dados `oscar_database` contém a tabela `filmes` com os seguintes campos:

- `id_registro`: Identificador único do registro
- `ano_filmagem`: Ano de filmagem do filme
- `ano_cerimonia`: Ano da cerimônia do Oscar
- `edicao_cerimonia`: Edição da cerimônia do Oscar
- `categoria`: Categoria do prêmio (ex: Actor, Actress, Best Picture)
- `nome_do_indicado`: Nome do indicado ao prêmio
- `nome_filme`: Nome do filme indicado
- `vencedor`: Indica se o indicado venceu o prêmio (Sim/Não)

## Consultas SQL

Aqui estão as consultas SQL realizadas neste projeto para análise dos dados:

1. **Quantas vezes Natalie Portman foi indicada ao Oscar?**

   ```sql
   SELECT COUNT(*) AS vezes_indicada
   FROM filmes
   WHERE nome_do_indicado = 'Natalie Portman';
   ```
   
2. **Quantos Oscars Natalie Portman ganhou??**
   ```sql
   SELECT COUNT(*) AS oscars_ganhos
   FROM filmes
   WHERE nome_do_indicado = 'Natalie Portman' AND vencedor = 'Sim';
   ```
   
3. **Amy Adams já ganhou algum Oscar??**
   
   ```sql
    SELECT COUNT(*) AS oscars_ganhos
    FROM filmes
    WHERE nome_do_indicado = 'Amy Adams' AND vencedor = 'Sim';
   ```
   
4. **A série de filmes Toy Story ganhou um Oscar em quais anos??**

   ```sql
    SELECT DISTINCT ano_cerimonia
    FROM filmes
    WHERE nome_filme LIKE 'Toy Story%' AND vencedor = 'Sim';
   ```
   
5. **A partir de que ano que a categoria "Actress" deixa de existir?**

   ```sql
    SELECT MIN(ano_cerimonia) AS primeiro_ano_sem_actress
    FROM filmes
    WHERE categoria = 'ACTRESS';
   ```
   
6. **O primeiro Oscar para melhor Atriz foi para quem? Em que ano?**
   
   ```sql
   SELECT nome_do_indicado, MIN(ano_cerimonia) AS primeiro_ano
   FROM filmes
   WHERE categoria = 'ACTRESS' AND vencedor = 'Sim'
   GROUP BY categoria;
   ```
   
7. **Na coluna/campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0.**
   
  ```sql
  UPDATE filmes
  SET vencedor = CASE WHEN vencedor = 'Sim' THEN '1' ELSE '0' END;
  ```
   
8. **Em qual edição do Oscar "Crash" concorreu ao Oscar?**

   ```sql
   SELECT edicao_cerimonia
   FROM filmes
   WHERE nome_filme = 'Crash';
   ```
   
9. **Quantas vezes Natalie Portman foi indicada ao Oscar?**
   ```sql
   SELECT COUNT(*) AS vezes_indicada
   FROM filmes
   WHERE nome_do_indicado = 'Natalie Portman';
   ```
10. **Dê um Oscar para um filme que merece muito, mas não ganhou.**
    
   ```sql
   UPDATE filmes
   SET vencedor = 'Sim'
   WHERE nome_filme = 'E.T. O Extraterrestre';
   ```

11. **Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser.**

   ```sql
    INSERT INTO filmes (ano_filmagem, ano_cerimonia, edicao_cerimonia, categoria, nome_do_indicado, nome_filme, vencedor)
    VALUES
    ('2004', '2024', '95', 'ANIMATED FEATURE', 'Studio Ghibli', 'O Castelo Animado', 'Não'),
    ('2008', '2024', '95', 'ANIMATED FEATURE', 'Studio Ghibli', 'Ponyo: Uma Amizade que Veio do Mar', 'Não'),
    ('2001', '2024', '95', 'ANIMATED FEATURE', 'Studio Ghibli', 'A Viagem de Chihiro', 'Não');
   ```

12. **Oscar de melhor filme, Melhor Atriz e Melhor Diretor no ano em que você nasceu:**

   ```sql
    SELECT nome_filme AS melhor_filme, nome_do_indicado AS melhor_atriz, nome_do_indicado AS melhor_diretor
    FROM filmes
    WHERE ano_cerimonia = 2006>
      AND categoria IN ('BEST PICTURE', 'ACTRESS', 'DIRECTOR')
      AND vencedor = 'Sim';
   ```


