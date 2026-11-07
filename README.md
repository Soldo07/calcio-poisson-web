# Calcio Poisson

Dashboard personale per analizzare le partite di calcio con un modello statistico di Poisson. Mostra le partite del giorno, stima le probabilità di ogni esito e le confronta con le quote del mercato.

**Apri la pagina:** https://soldo07.github.io/calcio-poisson-web/

Funziona nel browser, senza installare nulla, su iPhone, iPad e computer. Da iPhone e iPad si può aggiungere alla schermata Home (Condividi → Aggiungi a schermata Home) e usare come un'app a schermo intero.

## Cosa mostra

- **Partite del giorno** (ieri, oggi, domani) con orario o minuto di gioco, filtro per i campionati principali e ricerca per squadra.
- **Verdetto**: in cima alla sintesi, lo spunto di valore (l'esito su cui il modello si discosta di più dal mercato) oppure l'esito più probabile quando le quote non sono ancora caricate.
- **Sintesi della partita**: probabilità 1X2, doppia chance, Goal e No Goal, Over e Under, gol attesi per squadra.
- **Punteggi esatti** più probabili, con la quota equa di ciascuno.
- **Quote a confronto**: la quota equa calcolata dal modello accanto a quella del mercato, per vedere dove le due si discostano.
- **Squadre**: rendimento in casa e fuori, gol fatti e subiti a partita, infortunati e squalificati di ciascuna squadra, gialli e rossi attesi con tre linee Over sui cartellini.
- **Confronto con la previsione di API-Football**, quando il servizio la fornisce.
- **Sezione Dati**: quante richieste sono state usate oggi, quante restano e quanto vale la memoria locale.

Campionati nel filtro principale: Serie A, Premier League, La Liga, Bundesliga, Ligue 1, Champions League, Europa League e Conference League. Il filtro "Tutte" mostra ogni partita disponibile.

## Come funziona il modello

1. Per ogni squadra si calcola la forza in attacco e in difesa rispetto alla media del campionato, separando le gare in casa da quelle in trasferta. Se la media del campionato non è disponibile, si usano valori tipici.
2. Le forze vengono avvicinate alla media quando le partite giocate sono poche (fattore di regressione K = 5), così un campione piccolo non produce stime estreme.
3. Da queste si ricavano i gol attesi di ciascuna squadra.
4. Si costruisce una matrice di probabilità da 0 a 10 gol per squadra, con distribuzioni di Poisson e la correzione di Dixon-Coles sui punteggi bassi (0-0, 1-0, 0-1, 1-1), che il Poisson puro tende a sottostimare nei pareggi.
5. Dalla matrice si ottengono tutti i mercati: 1X2, doppia chance, Goal e No Goal, Over e Under, punteggi esatti.

La quota equa è 1 diviso la probabilità. Non include il margine del bookmaker, quindi non è confrontabile alla pari con una quota reale: serve a vedere la differenza, non a prevedere un esito.

## Pensata per l'uso da telefono

- Navigazione con cronologia: il gesto o il tasto Indietro riporta alla lista.
- Gesti: scorrimento di una riga per aprire l'analisi, trascinamento verso il basso per aggiornare, scorrimento laterale per cambiare scheda.
- Su iPad le sezioni sono impilate con una barra di schede fissa; su computer la lista sta a sinistra e l'analisi a destra, con le frecce su e giù per passare da una partita all'altra.
- Tema chiaro e scuro automatico in base al dispositivo.
- Le risposte restano salvate sul dispositivo per un tempo limitato, così si consumano meno richieste e le schermate si aprono subito.

## Note

- Strumento a scopo informativo e di studio: le probabilità sono stime statistiche e non garantiscono alcun risultato. Non è un consiglio di scommessa.
- Il modello non conosce formazioni, squalifiche, motivazioni o condizioni di forma: tratta ogni partita come indipendente dalle altre.
- Dati sulle partite, quote e classifiche forniti da [API-Football](https://www.api-football.com/).
- La pagina è un singolo file HTML, senza servizi di tracciamento. I font sono caricati da Google Fonts.
- Progetto personale di Diego Soldo. Il codice sorgente è conservato in un repository privato.
