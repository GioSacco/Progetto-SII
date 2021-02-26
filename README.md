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

## Trasformazione 