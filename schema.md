Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d’Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d’Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.
Utilizzare https://www.diagrams.net/ per la creazione dello schema. Esportare quindi il diagramma in jpg e caricarlo nella repo.


# Table Dipartimenti
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL
- Nome | VARCHAR (50), NOT NULL
- Indirizzo | VARCHAR (50), NOT NULL
- Email | VARCHAR(50), NOT NULL
- Telefono | VARCHAR(20), NOT NULL
- Numero corsi di laurea | SMALLINT, NOT NULL

# Table Corsi di Laurea
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL
- Nome | VARCHAR (50), NOT NULL
- Numero corsi | SMALLINT, NOT NULL
- Codice corso di laurea | VARCHAR(20), NOT NULL
- Tipo | VARCHAR(20), NOT NULL
- Requisiti | VARCHAR(255), DEFAULT(Nessun Requisito Richiesto)
- Note | TEXT, NULL
- Durata | SMALLINT, NULL
- Lingua | VARCHAR(50), DEFAULT(Italiano)

# Table Corsi
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL
- Nome | VARCHAR (50), NOT NULL
- Durata | SMALLINT, NULL
- Esami | SMALLINT, NULL
- Insegnanti | VARCHAR(50), NOT NULL
- Studenti | SMALLINT, NOT NULL
- Note | TEXT, NULL



# Table Insegnanti
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL
- Nome | VARCHAR (50), NOT NULL
- Cognome | VARCHAR (50), NOT NULL
- Anno di nascita | YEAR, NULL
- Email | VARCHAR(50), NOT NULL
- Note | TEXT, NULL
- Lingua | VARCHAR(50), DEFAULT(Italiano)


# Table Esami
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL
- Nome | VARCHAR (50), NOT NULL
- Tipo | VARCHAR(15), NOT NULL
- Codice | VARCHAR(10), NOT NULL
- Durata | SMALLINT, NULL
- obbligatorio | BOOLEAN, DEFAULT(TRUE)
- CFU | SMALLINT, NOT NULL
- Data | DATE, NULL


# Table Studenti
- Id | PK, BIGINT, AUTO_INCREMENT, UNIQUE, NOT NULL
- Nome | VARCHAR (50), NOT NULL
- Cognome | VARCHAR (50), NOT NULL
- Matricola | VARCHAR(10), NOT NULL
- Email | VARCHAR(50), NOT NULL
- Anno di nascita | YEAR, NOT NULL
- Media voti | FLOAT(4,2)
- Fascia reddituale | VARCHAR(20), NULL
- Occupazione | VARCHAR(20), NULL
- Voto diploma | SMALLINT, NOT NULL
- Note | TEXT, NULL


# Relationships 

Dipartimento <oneToMany> Corsi di laurea 
Corso di Laurea <manyToMany> Corsi 
Corso <manyToMany> Insegnanti 
Corso <oneToMany> Esami
Corso <manyToMany> Studenti
Studente <manyToMany> Esami
Insegnante <manyToMany> Esami