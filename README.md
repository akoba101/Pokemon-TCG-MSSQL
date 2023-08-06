# Pokemon-TCG-MSSQL
Conversion of the following JSON library to an MS SQL Server database from the following repository:

https://github.com/PokemonTCG/pokemon-tcg-data

# ERD
![image](https://github.com/akoba101/Pokemon-TCG-MSSQL/assets/131304176/aece5de3-cb42-49e8-a349-cf281c75d23d)

# Common Queries
Find info on all cards from a specific pokemon:
```sql
SELECT
  c.ID
  ,c.CardIndex
  ,c.CardName
  ,p.Pokemon
  ,c.LargeImage
FROM Cards c
LEFT JOIN CardPokedexNum cpn
  ON c.ID = cpn.CardID
LEFT JOIN Pokedex p
  ON p.ID = cpn.PokedexID
WHERE p.Pokemon = 'Pikachu'
```
