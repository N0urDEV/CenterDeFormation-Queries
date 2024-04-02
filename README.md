# Database Tables

## Table: catalogue

| Field    | Type | Null | Key | Default | Extra |
|----------|------|------|-----|---------|-------|
| codespec | int  | YES  |     | NULL    |       |
| codeform | int  | YES  |     | NULL    |       |

## Table: etudiant

| Field         | Type        | Null | Key | Default | Extra |
|---------------|-------------|------|-----|---------|-------|
| numCINEtu     | varchar(50) | YES  |     | NULL    |       |
| nomEtu        | varchar(50) | YES  |     | NULL    |       |
| prenomEtu     | varchar(50) | YES  |     | NULL    |       |
| dateNaissance | date        | YES  |     | NULL    |       |
| adressEtu     | varchar(50) | YES  |     | NULL    |       |
| villeEtu      | varchar(50) | YES  |     | NULL    |       |
| niveauEtu     | varchar(50) | YES  |     | NULL    |       |

## Table: formation

| Field     | Type        | Null | Key | Default | Extra |
|-----------|-------------|------|-----|---------|-------|
| codeform  | int         | YES  |     | NULL    |       |
| titreform | varchar(50) | YES  |     | NULL    |       |
| dureeform | int         | YES  |     | NULL    |       |
| prixform  | int         | YES  |     | NULL    |       |

## Table: inscription

| Field          | Type         | Null | Key | Default | Extra |
|----------------|--------------|------|-----|---------|-------|
| codeSess       | int          | YES  |     | NULL    |       |
| numCINEtu      | varchar(40)  | YES  |     | NULL    |       |
| TypeCours      | varchar(25)  | YES  |     | NULL    |       |
| numInscription | varchar(255) | YES  |     | NULL    |       |

## Table: session

| Field     | Type        | Null | Key | Default | Extra |
|-----------|-------------|------|-----|---------|-------|
| codesess  | int         | YES  |     | NULL    |       |
| nomsess   | varchar(50) | YES  |     | NULL    |       |
| datedebut | date        | YES  |     | NULL    |       |
| datefin   | date        | YES  |     | NULL    |       |
| codeform  | int         | YES  |     | NULL    |       |

## Table: specialite

| Field    | Type        | Null | Key | Default | Extra |
|----------|-------------|------|-----|---------|-------|
| codespec | int         | YES  |     | NULL    |       |
| nomspec  | varchar(50) | YES  |     | NULL    |       |
| descspec | varchar(50) | YES  |     | NULL    |       |
| active   | int         | YES  |     | NULL    |       |
