# Centre de Formation Exercise

Welcome to the Center of Formation Database repository! This repository contains SQL queries and documentation for a database related to a center of formation. The database includes tables for cataloging courses, managing students, organizing sessions, and more.

## Questions and SQL Queries

### 1. Lister pour chaque formation ses sessions ouvertes. Afficher le Titre de la formation, le nom de la session, la date de début et la date fin.

```sql
SELECT f.titreform, s.nomsess, s.datedebut, s.datefin
FROM formation f
JOIN session s ON f.codeform = s.codeform;
```

### 2. Lister Les étudiants inscrits dans chacune des formations. Ordonner la liste par titre de formation.

```sql
SELECT f.titreform, e.nomEtu, e.prenomEtu
FROM formation f
JOIN inscription i ON f.codeform = i.codeform
JOIN etudiant e ON i.numCINEtu = e.numCINEtu
ORDER BY f.titreform;
```

### 3. Pour la formation web développement, calculer le nombre d’inscriptions distancielles et présentielles.

```sql
SELECT
    (SELECT COUNT(*) FROM inscription WHERE TypeCours = 'Distancielle' AND codeSess IN (SELECT codesess FROM session WHERE codeform = (SELECT codeform FROM formation WHERE titreform = 'web développement'))) AS Inscriptions_distancielles,
    (SELECT COUNT(*) FROM inscription WHERE TypeCours = 'Présentiel' AND codeSess IN (SELECT codesess FROM session WHERE codeform = (SELECT codeform FROM formation WHERE titreform = 'web développement'))) AS Inscriptions_presentielles;
```


### 4. Lister les formations dont le nombre d’inscriptions distancielles est supérieur ou égale à 3. Ordonner la liste par le nombre d’inscription.

```sql
SELECT f.titreform, COUNT(*) AS Nombre_d_inscriptions_distancielles
FROM formation f
JOIN session s ON f.codeform = s.codeform
JOIN inscription i ON s.codesess = i.codeSess
WHERE i.TypeCours = 'Distancielle'
GROUP BY f.titreform
HAVING COUNT(*) >= 3
ORDER BY COUNT(*) DESC;
```

### 5. Lister pour chaque spécialité active, la liste des formations correspondantes : leurs titres, durée et prix. Ordonner la liste par l’ordre alphabétique descendant du nom de la spécialité.

```sql
SELECT sp.nomspec, f.titreform, f.dureeform, f.prixform
FROM specialite sp
JOIN catalogue c ON sp.codespec = c.codespec
JOIN formation f ON c.codeform = f.codeform
WHERE sp.active = 1
ORDER BY sp.nomspec DESC;
```

### 6. Afficher l’union de la liste en N : 4 avec la liste des formations dont le nombre d’inscriptions présentielles est supérieur ou égal à 4.

```sql
(SELECT f.titreform, COUNT(*) AS Nombre_d_inscriptions_distancielles
FROM formation f
JOIN session s ON f.codeform = s.codeform
JOIN inscription i ON s.codesess = i.codeSess
WHERE i.TypeCours = 'Distancielle'
GROUP BY f.titreform
HAVING COUNT(*) >= 3)
UNION
(SELECT f.titreform, COUNT(*) AS Nombre_d_inscriptions_presentielles
FROM formation f
JOIN session s ON f.codeform = s.codeform
JOIN inscription i ON s.codesess = i.codeSess
WHERE i.TypeCours = 'Présentiel'
GROUP BY f.titreform
HAVING COUNT(*) >= 4);
```

### 7. Calculer le total des prix payés par Année et mois de la date début des sessions

```sql
SELECT YEAR(s.datedebut) AS Annee, MONTH(s.datedebut) AS Mois, SUM(f.prixform) AS Total_prix_payes
FROM session s
JOIN formation f ON s.codeform = f.codeform
JOIN inscription i ON s.codesess = i.codeSess
GROUP BY YEAR(s.datedebut), MONTH(s.datedebut);
```
