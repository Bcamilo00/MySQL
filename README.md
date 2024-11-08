# MySQL Consultas Básicas
En el siguiente taller se realizaron consultas basicas en MySQL Workbench y unas consultar intermedias encontraras evidencia fotografica de las consultas las cuales fueron realizadas en la Base de datos WORLD.
## Consultas Basicas
### Selección de países en el continente 'Asia'
SELECT Name FROM Country WHERE Continent = 'Asia';
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_1.png)
### Contar el número total de ciudades
SELECT COUNT(*) AS TotalCities FROM City;
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_2.png)
### Listar todos los idiomas únicos en la tabla CountryLanguage
SELECT DISTINCT Language FROM CountryLanguage;
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_3.png)
### Selección de países con población mayor a 100 millones
SELECT Name,population FROM Country WHERE Population > 100000000;
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_4.png)
### Listar nombres de países y continentes ordenados alfabéticamente por nombre de país
SELECT Name, Continent FROM Country ORDER BY Name;
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_5.png)
### Obtener la ciudad con mayor población
SELECT Name FROM City ORDER BY Population DESC LIMIT 1;
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_6.png)
### Selección de países que tienen 'Republic' en su nombre
SELECT Name FROM Country WHERE Name LIKE '%Republic%';
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_7.png)
### Listar los 5 países más poblados
SELECT Name, Population FROM Country ORDER BY Population DESC LIMIT 5;
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_8.png)
### Calcular la población promedio de los países en el continente 'Europe'
SELECT AVG(Population) AS AveragePopulation FROM Country WHERE Continent = 'Europe';
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_9.png)
### Selección de idiomas con más del 10% de la población mundial que los habla
SELECT Language, SUM(Population * Percentage / 100) AS Speakers
FROM countrylanguage
JOIN country ON country.Code = countrylanguage.CountryCode
GROUP BY Language
HAVING SUM(Population * Percentage / 100) > (SELECT SUM(Population) * 0.1 FROM country);
[![](https://github.com/Bcamilo00/MySQL/blob/main/basica_10.png)
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
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_1.png)
### Listar países que usan más de un idioma
SELECT country.Name
FROM country
JOIN countrylanguage ON country.Code = countrylanguage.CountryCode
GROUP BY country.Code
HAVING COUNT(countrylanguage.Language) > 1;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_2.png)
### Calcular el total de población de cada continente
SELECT Continent, SUM(Population) AS TotalPopulation
FROM country
GROUP BY Continent;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_3.png)
### Contar el número de ciudades en cada país
SELECT country.Name, COUNT(city.ID) AS NumberOfCities
FROM country
JOIN city ON country.Code = city.CountryCode
GROUP BY country.Code;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_4.png)
### Listar los países y su promedio de vida ordenados por el promedio de vida en orden descendente
SELECT Name, LifeExpectancy
FROM country
ORDER BY LifeExpectancy DESC;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_5.png)
### Selección de ciudades cuya población está entre 500,000 y 1,000,000
SELECT Name, Population
FROM city
WHERE Population BETWEEN 500000 AND 1000000;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_6.png)
### Listar los idiomas hablados en países donde la población es mayor a 50 millones
SELECT DISTINCT countrylanguage.Language
FROM country
JOIN countrylanguage ON country.Code = countrylanguage.CountryCode
WHERE country.Population > 50000000;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_7.png)
### Calcular el promedio de población por ciudad en cada país
SELECT country.Name, AVG(city.Population) AS AvgCityPopulation
FROM country
JOIN city ON country.Code = city.CountryCode
GROUP BY country.Code;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_8.png)
### Seleccionar los países cuya calificación de vida está por encima del promedio mundial
SELECT Name, LifeExpectancy
FROM country
WHERE LifeExpectancy > (SELECT AVG(LifeExpectancy) FROM country);
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_9.png)
### Encontrar los continentes con una calificación de vida superior al promedio de su continente
SELECT Continent
FROM country
GROUP BY Continent
HAVING AVG(LifeExpectancy) > (SELECT AVG(LifeExpectancy) FROM country);
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/intermedia_10.png)
## Consultas Adicionales
### ¿Cuáles son los nombres de los países del continente 'South America'?
σ Continent= ′SouthAmerica ′(Country)
SELECT Name FROM Country WHERE Continent = 'South America';
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_1.png)
### ¿Cuál es el número total de países en la base de datos?
COUNT(Country.Name)COUNT(Country.Name)
SELECT COUNT(*) AS TotalCountries FROM Country;
[![intermedia-4.png](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_2.png)
### ¿Cuáles son los nombres de las ciudades cuya población supera 1 millón de habitantes?
σ Population>1000000(City)
SELECT Name,population FROM City WHERE Population > 1000000;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_3.png)
### ¿Qué continentes están representados en la base de datos?
π Continent(Country)
SELECT DISTINCT Continent FROM Country;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_4.png)
### ¿Cuál es la población total del continente 'Africa'?
γSUM(Population)(σ Continent= ′Africa ′(Country))
SELECT SUM(Population) AS TotalPopulation FROM Country WHERE Continent = 'Africa';
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_5.png)
### ¿Cuáles son los idiomas oficiales en el país 'India'?
π Language(σCountry.Name= ′India′(CountryLanguage⋈Country))
SELECT Language FROM CountryLanguage JOIN Country ON Country.Code = CountryLanguage.CountryCode WHERE Country.Name = 'India';
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_6.png)
### ¿Cuáles son los países con una esperanza de vida superior a 80 años? 
𝜎LifeExpectancy>80(Country)σ LifeExpectancy>80(Country)
SELECT Name FROM Country WHERE LifeExpectancy > 80;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_7.png)
### ¿Cuántos idiomas se hablan en 'Europe'?
𝛾COUNT(DISTINCT Language)(𝜎Continent=′𝐸𝑢𝑟𝑜𝑝𝑒′(CountryLanguage⋈Country))γ COUNT(DISTINCT Language)(σContinent= ′Europe ′
SELECT COUNT(DISTINCT Language) AS NumberOfLanguages FROM CountryLanguage JOIN Country ON Country.Code = CountryLanguage.CountryCode WHERE Country.Continent = 'Europe';
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_8.png)
### ¿Cuál es el país con el PIB (Producto Interno Bruto) más alto?
TOP(1,ORDER BY GNP DESC(Country))
SELECT Name FROM Country ORDER BY GNP DESC LIMIT 1;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_9.png)
### ¿Cuáles son las ciudades que pertenecen a un país con una población mayor a 50 millones?
π City.Name(City⋈(σPopulation>50000000(Country)))
SELECT City.Name FROM City JOIN Country ON City.CountryCode = Country.Code WHERE Country.Population > 50000000;
[![](https://github.com/Bcamilo00/MySQL/blob/7659c3dd7b831ed5253e5ba3c83522b7350b97af/adicional_10.png)


