# Pokemon-TCG-MSSQL
Conversion of a JSON library of Pokemon TCG cards to an MS SQL Server 2022 database from the following repository:

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

Find all attributes associated with Cards:
```sql
SELECT DISTINCT
  AttributeType
  ,AttributeValue
FROM CardAttributes
ORDER BY AttributeType, AttributeValue
```

Find info on pokemon of a specific attribute:
```sql
SELECT
  c.ID
  ,c.CardIndex
  ,c.CardName
  ,ca.AttributeValue
  ,c.LargeImage
FROM Cards c
LEFT JOIN CardAttributes ca
  ON c.ID = ca.CardID
WHERE ca.AttributeValue = 'flying'
```

Find highest attack damage per modifier:
```sql
SELECT
  DamageMod
  ,MAX(Damage)
FROM Attacks
GROUP BY DamageMod
ORDER BY DamageMod
```

Find a list of cards where the pokemon has no weaknesses:
```sql
SELECT
  c.ID
  ,c.CardIndex
  ,c.CardName
  ,c.LargeImage
  ,w.id
FROM Cards c
LEFT JOIN Weaknesses w
	ON c.ID = w.CardID
WHERE w.ID IS NULL
AND c.SuperType = 'Pokemon'
```
