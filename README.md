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
[![intermedia-2.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_2.png)
### Calcular el total de población de cada continente
SELECT Continent, SUM(Population) AS TotalPopulation
FROM country
GROUP BY Continent;
[![intermedia-3.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_3.png)
### Contar el número de ciudades en cada país
SELECT country.Name, COUNT(city.ID) AS NumberOfCities
FROM country
JOIN city ON country.Code = city.CountryCode
GROUP BY country.Code;
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_4.png)
### Listar los países y su promedio de vida ordenados por el promedio de vida en orden descendente
SELECT Name, LifeExpectancy
FROM country
ORDER BY LifeExpectancy DESC;
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_5.png)
### Selección de ciudades cuya población está entre 500,000 y 1,000,000
SELECT Name, Population
FROM city
WHERE Population BETWEEN 500000 AND 1000000;
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_6.png)
### Listar los idiomas hablados en países donde la población es mayor a 50 millones
SELECT DISTINCT countrylanguage.Language
FROM country
JOIN countrylanguage ON country.Code = countrylanguage.CountryCode
WHERE country.Population > 50000000;
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_7.png)
### Calcular el promedio de población por ciudad en cada país
SELECT country.Name, AVG(city.Population) AS AvgCityPopulation
FROM country
JOIN city ON country.Code = city.CountryCode
GROUP BY country.Code;
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_8.png)
### Seleccionar los países cuya calificación de vida está por encima del promedio mundial
SELECT Name, LifeExpectancy
FROM country
WHERE LifeExpectancy > (SELECT AVG(LifeExpectancy) FROM country);
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_9.png)
### Encontrar los continentes con una calificación de vida superior al promedio de su continente
SELECT Continent
FROM country
GROUP BY Continent
HAVING AVG(LifeExpectancy) > (SELECT AVG(LifeExpectancy) FROM country);
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_10.png)



