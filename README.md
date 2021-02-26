# Progetto per l'esame di Sistemi Intelligenti Per Internet

Il progetto prevede lo sviluppo di un Sistema Di Raccomandazione che, a partire da un dataset contenente la lista degli allenamenti effettuati da vari utenti, restituisca la lista di utenti con allenamenti simili ad un dato utente ricevuto in input.

## Dataset utilizzato

Come dataset è stato scelto quello disponibile al seguente link:
* https://sites.google.com/eng.ucsd.edu/fitrec-project/home

Tale dataset contiene una lista di allenamenti effettuati da diversi utenti e, per ogni allenamento, le seguenti info:
* lista delle coordinate rilevate durante l'allenamento;
* timestamp campionati durante l'allenamento;
* frequenza cardiaca campionata durante l'allenamento;
* altitudine rilevata durante l'allenamento;
* sesso dell'utente
* sport (bike o run)
* id utente

## Metodologia utilizzata 

Si tratta di un dataset sparso, nel quale ogni allenamento è completamente scollegato dagli altri. Non è quindi possibile conoscere il gradimento di un utente nei confronti di un allenamento effettuato da un altro utente. Per tale motivo ho quindi escluso l'utilizzo di filtri collaborativi e spostato l'attenzione ai filtri content-based. 

L'obiettivo è quindi quello di cercare di rilevare la somiglianza tra gli allenamenti così da individuare gli utenti simili.

## Revisione del dataset

Per consentire un'analisi più precisa e accurata, ho effettuato una revisione dei dati contenuti nel dataset. Per ogni allenamento ho effettuato le seguenti evoluzioni sui dati presenti:
* rilevazione della distanza totale a partire dalla lista delle coordinate;
* rilevazione del dislivello totale a partire dalla lista delle altitudini;
* rilevazione della frequenza cardiaca media a partire dalla lista dei campioni rilevati durante l'allenamento;
* rilevazione della durata totale a partire dai timestamp campionati durante l'allenamento;
* rilevazione dalla velocità media a partire dalla distanza totale e dalla durata dell'allenamento.

## Approccio tramite TFIDF e Cosine Similarity 

Evoluti i dati del dataset nelle modalità descritte sopra, ho allora creato un nuovo dataset contenente la lista degli utenti con, per ogni utente, i dati di tutti gli allenamenti da lui effettuati. I dati degli allenamenti li ho rielaborati così che rappresentassero un documento testuale in cui, ogni parola/frase, rappresentasse i dati di un singolo allenamento. Ho difatti concatenato, per ogni allenamento, i dati numerici ad esso associati per poi concatenarli con quelli degli altri allenamenti così da ottenenre, per ogni utente, un documento contenente le info di tutti gli allenamenti.

Ho poi utilizzato TF-IDF e la cosine similarity per rilevare la distanza tra i vari utenti così da poter restituire, a partire da un utente, la lista degli utenti ad esso più simili. (i dettaglio del metodo utilizzato e dell'implementazione sono presenti nei commenti nel codice)

## Risultati ottenuti e sviluppi futuri

Per verificare l'efficacia del modello ho quindi creato dei grafici che rappresentassero l'andamento dei dati associati ai vari allenamenti per ogni utente. Essendo i valori di ogni allenamento numerici, ho sommato tali valori così da ottenere un valore numerico per ogni allenamento di ogni utente. Inserendo tali valori in un grafico, ho quindi potuto osservare l'andamento di tali valori per ogni utente riuscendo quindi a profilare, anche graficamente, ogni utente. In sostanza quindi l'i-esimo punto nel grafico rappresenta la somma dei valori individuati per quell'i-esimo allenamento.

Una volta restituita dal sistema la lista degli utenti simili ad un certo utente ho quindi costruito il grafico associato all'utente selezionato stesso e quelli associati agli utenti ad esso simili restituiti dal sistema. Ho notato come i grafici avessero effettivamente un andamento molto simile confermando quindi che il sistema avesse restituito risultati soddisfacenti.

Come sviluppi futuri, magari per il progetto di Machine Learning, potrebbero esserci le seguenti evolutive:
* riduzione del rumore sui dati presenti nel dataset
* data la lista di utenti simili, effettuare una predizione degli allenamenti, appartenenti a tali utenti, nei quali l'utente selzionato per l'analisi possa ottenere risultati migliori (in termini di velocità media, frequenza cardiaca media, tempo totale)