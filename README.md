# MySQL Consultas Básicas
En el siguiente taller se realizaron consultas basicas en MySQL Workbench y unas consultar intermedias encontraras evidencia fotografica de las consultas las cuales fueron realizadas en la Base de datos WORLD.
## Consultas intermedias
### Encontrar los 5 países más poblados por continente
SELECT Continent, Name, Population
FROM country
WHERE (Continent, Population) IN (
    SELECT Continent, Population
    FROM (
        SELECT Continent, Name, Population,
               ROW_NUMBER() OVER (PARTITION BY Continent ORDER BY Population DESC) AS RowNum
        FROM country
    ) AS Ranked
    WHERE RowNum <= 5
);
[![intermedia-1.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_1.png)
### Listar países que usan más de un idioma
SELECT country.Name
FROM country
JOIN countrylanguage ON country.Code = countrylanguage.CountryCode
GROUP BY country.Code
HAVING COUNT(countrylanguage.Language) > 1;
[![intermedia-2.png](https://i.postimg.cc/sg85Fnsp/intermedia-2.png)](https://postimg.cc/zyCyKFLB)
### Calcular el total de población de cada continente
SELECT Continent, SUM(Population) AS TotalPopulation
FROM country
GROUP BY Continent;
[![intermedia-3.png](https://i.postimg.cc/Fsry0dTJ/intermedia-3.png)](https://postimg.cc/4n0HgdkJ)
### Contar el número de ciudades en cada país
SELECT country.Name, COUNT(city.ID) AS NumberOfCities
FROM country
JOIN city ON country.Code = city.CountryCode
GROUP BY country.Code;
[![intermedia-4.png](https://i.postimg.cc/2S3nKpRk/intermedia-4.png)](https://postimg.cc/RW53WDZy)
