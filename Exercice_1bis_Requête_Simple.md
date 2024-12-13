### **Exercice : Requête simple avec SQL** ### 

Cet exercice est extrait de ce site https://sqlzoo.net/wiki/SELECT_names\. Ci-dessous un extrait de la table "world"

<div align="center">
  <img src="https://github.com/user-attachments/assets/ad71b0fe-f9e0-464e-9fc6-c3beebd292d8" alt="Description de l'image" width="200"/>
</div>

**1.	Find the country that start with Y**\
SELECT name\
FROM world\
WHERE name LIKE 'Y%'

**2.	Find the countries that end with Y**\
SELECT name\
FROM world\
WHERE name LIKE '%Y'

**3.	Find the countries that contain the letter X**\
SELECT name\
FROM world\
WHERE name LIKE '%X%'

**4.	Find the countries that end with land**\
SELECT name\
FROM world\
WHERE name LIKE '%land'

**5.	Find the countries that start with C and end with IA**\
SELECT name\
FROM world\
WHERE name LIKE 'C%_%IA'

**6.	Find the country that has OO in the name**\
SELECT name\
FROM world\
WHERE name LIKE '%oo%'

**7.	Find the countries that have three or more a in the name**\
SELECT name\
FROM world\
WHERE name LIKE '%a%a%a%';

**8.	Find the countries that have "t" as the second character.**\
SELECT name\
FROM world\
WHERE name LIKE '_t%'\
ORDER BY name

**9.	Find the countries that have two "o" characters separated by two others.**\
SELECT name\
FROM world\
WHERE name LIKE '%o__o%'

**10.	Find the countries that have exactly four characters.**\
SELECT name\
FROM world\
WHERE length(name)=4

**11.	Find the country where the name is the capital city.**\
SELECT name\
FROM world\
WHERE name = capital;

**12.	Find the country where the capital is the country plus "City".**\
SELECT name\
FROM world\
WHERE capital = CONCAT(name, ' City')

**13.	Find the capital and the name where the capital includes the name of the country.**\
SELECT capital, name\
FROM world\
WHERE capital LIKE CONCAT('%', name, '%')

**14.	Find the capital and the name where the capital is an extension of name of the country.**\
SELECT capital, name\
FROM world\
WHERE capital LIKE CONCAT(name, '%') AND LENGTH(capital) > LENGTH(name)

**15.	Show the name and the extension where the capital is a proper (non-empty) extension of name of the country.**\
SELECT name, REPLACE(capital, name, '')\
FROM world\
WHERE capital LIKE CONCAT(name, '%')\
AND REPLACE(capital, name, '') <> ''























