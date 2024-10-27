> Password Moodle:
> dieMiephie3b

**Rete**
Le definizioni di rete sono due:
- **Base**: Due o più nodi connesse tramite collegamenti.
- **Ricorsiva:** Due o più reti connesse tramite nodi.

**Nodo**
I nodi possono essere di più tipi:
- **Host**: Termine astratto per identificare un nodo terminale, ovvero un nodo connesso all'inizio o alla fine di una comunicazione, mittente/destinatario.
- **Switch, Bridge, Router**: Sono esempi di nodi intermedi, ovvero nodi che connettono host ad altri host. Nomi differenti indicano funzionalità differenti.

**Collegamento**
I collegamenti principali sono due:
- **Wired**: Collegamento via cavo.
- **Wireless**: Collegamento senza cavi.

**Astrazione di Reti**
Possiamo usare paradigmi di astrazione grazie alla natura ricorsiva delle reti.
Ciò ci permette di nascondere dettagli futili per focalizzarci sui punti di interesse.
- Essendo ricorsivo, possiamo applicare questo approccio più volte.

**Comunicazione tra Reti**
Data una infrastruttura che comprende varie LAN (reti locali, fanno da host) e WAN (reti geografiche, fanno da reti intermediarie) abbiamo che le reti comunicano in questo modo:
- **Logicamente**: Comunicano soltanto i due host terminali.
- **Effettiva**: Le informazioni attraversano tutti i nodi terminali.

**Problemi delle Reti**
I problemi principali in cui ci possiamo imbattere sono due:
- **Instradamento**: Si verifica quando tutti i percorsi possibili in cui può passare la rete sono chiusi, impedendo la comunicazione.
- **Condivisione delle risorse**: Si verifica quando abbiamo troppe poche risorse in proporzione al carico di dati che dobbiamo trasferire.

**Caratteristiche delle Reti**
1) Host, nodi e collegamenti sono **eterogenei**.
2) La rete cambia nel tempo, che sia nelle tecnologie o negli scopi.
3) La rete, quindi i nodi e i collegamenti son **condivisi**.

**Protocollo**
Un protocollo è un insieme di regole e convenzioni seguite da entità, **dislocate su nodi distinti** in modo da comunicare e svolgere un compito comune. 

Il loro scopo è quello di assicurare che le entità cooperino in modo efficiente per svolgere la realizzazione di servizi di rete, assicurandosi di agire nei limiti del sistema distribuito in uso.
- **Tutte** le comunicazioni sono protocolli.

**Elementi di un Protocollo di Comunicazione**
- **Sintassi**: Insieme e struttura dei comandi e delle risposte, il formato dei messaggi.
- **Semantica**: Significato dei comandi, delle azioni e delle risposte effettuate durante la trasmissione/ricezione dei messaggi.
- **Temporizzazione**: Definizione dell'ordine e i tempi di esecuzione dei comandi, messaggi e risposte.

**Obiettivo Principale delle Reti**
L'obiettivo principale è il trasferimento di un messaggio (che è un insieme di bit) da un capo all'altro garantendo:
1) La massima velocità possibile (**prestazioni**).
2) Il superamento di guasti e malfunzionamenti (**affidabilità**).
3) Più sicurezza possibile nella trasmissione (**sicurezza**).
- In un contesto eterogeneo come quello delle reti è un obiettivo non banale da raggiungere.

**Metodologia per la Comunicazione di Reti**
1) Si divide il problema in sottoproblemi.
2) Si risolvono i sottoproblemi.
3) Si collegano le soluzioni parziali.

**Stack di Protocolli**
Le stack di protocolli sono alla base del sistema di comunicazione di Internet. Sono un insieme di protocolli tra loro cooperanti in cui si può identificare una relazione gerarchica; si usa un architettura a livelli (**layer**).

ESEMPIO:

| <center>Implementazione di logiche applicative specializzate     |
| ---------------------------------------------------------------- |
| <center>**Comunicazione fra applicazione in esecuzione su host** |
| <center>**Comunicazioni fra nodi di reti differenti**            |
| <center>**Comunicazione fra nodi di una stessa rete**            |

**Applicazioni di reti e protocolli**
Ogni layer può offrire delle **alternative** a seconda della necessità.
ESEMPIO:

| <center> Logica applicativa                                              |
| ------------------------------------------------------------------------ |
| <center>**Comunicazione fra applicazioni (affidabili - non affidabili)** |
| <center>**Comunicazioni fra reti**                                       |
| <center>**Comunicazione fra nodi (reti cablate - wireless)**             |

**Modello "A Livelli" di una Stack di Protocolli**
Ad un certo livello ciascun protocollo comprende tre interfacce; due sono interfacce **interne** che comprendono il livello superiore ed inferiore rispetto al nodo attuale, una è un interfaccia
**esterna** che va verso al livello equivalente di **un altro** nodo.

**Comunicazione tra Protocolli**
- **Logicamente**: La comunicazione avviene tra protocolli che si trovano sullo stesso livello.
- **Effettiva**: La comunicazione avviene in modo diretto solo al livello più basso, ovvero comunicano solo mittente e destinatario. Per gli altri livelli la comunicazione è indiretta.

**Multiplexing / Demultiplexing**
I mux/demux vengono utilizzati per la condivisione delle risorse. Sono fondamentali per ottimizzare l'utilizzo dei protocolli di rete.

**Modalità per Trasferire Dati**
Le modalità per trasferire dati sono due; **circuit switching** e **packet switching**.

**Circuit Switching**
Il circuit switching è un paradigma di comunicazione orientato alla connessione. 
Abbiamo un circuito dedicato per ogni comunicazione.
- L'invio di dati richiede di effettuare operazioni aggiuntive.
- Prima dell'invio **viene aperta** una connessione.
- Dopo l'avvio **viene chiusa** una connessione.

Abbiamo un pro e due contro:
- **Pro**: In fase di apertura possiamo verificare se abbiamo abbastanza risorse per comunicare.
- **Contro**: Dobbiamo riservare tutte le nostre risorse all'inizio della comunicazione, inoltre il canale creato occupa una quantità costante di risorse a prescindere del suo utilizzo.

**Packet Switching**
Nel packet switching ogni comunicazione è suddivisa in pacchetti. È la modalità per trasferire dati utilizzata al giorno d'oggi da Internet.
- Ogni pacchetto occupa **tutta** la banda disponibile di un collegamento.
- L'usaggio della banda non è stabilita a priori.
- Le risorse sono utilizzate sulla base della **necessità** e non della **prenotazione**.

Il packet switching usa un principio di multiplexing statistico; pacchetti provenienti da diverse sorgenti son mescolati sullo stesso link senza slot di tempo dedicato a priori, occupando tutta la banda disponibile.

Dato che non abbiamo la certezza di avere risorse disponibili si possono verificare dei conflitti a certi livelli:
- **Locale**: Collisione nelle reti locali con mezzi fisici condivisi.
- **Reti**: Congestione nei buffer dei router.
- **Generale**: Perdita di pacchetti durante le comunicazione.

**Metrica di Prestazione**
La bandwidth è la quantità di dati trasmessi per unità di tempo. Tipicamente abbiamo come:
- **Unità di Tempo**: Secondo.
- **Quantità di Dati Trasmessi**: Multipli di bit.

Metriche tipiche sono:
- Kbps o Kbit/s.
- Mbps o Mbit/s.
- Gbps o Gbit/s.

**Packet Switching vs Circuit Switching**
Abbiamo un link ad 1 Mbps. Ogni utente richiede 0.1 Mbps quando trasmette ed è attivo il 10% del tempo.

- **Circuit switching**: Può contenere al massimo 10 utenti, per ogni connessione occupa la banda richiesta dall'utente.
- **Packet switching**: Può contenere più utenti dato che non riserviamo risorse a priori. Se abbiamo 35 utenti collegati la chance che più di 10 utenti trasmettano packets insieme è bassa, ciò vuol dire che è possibile far comunicare 35 utenti con una minima chance di conflitto.

**Stack di Internet**
La stack di Internet quindi è basata su **stack di protocolli** e paradigma **packet switching**.
- Vi è **indipendenza funzionale tra i vari livelli**; il servizio offerto da un livello è definito in modo indipendente dalle procedure con cui è implementato.
- Il livello N+1 riceve il servizio dal livello N che a sua volta sfrutta il servizio al livello N-1.
- La comunicazione logicamente avviene tra livelli pari, realmente attraversa tutti i livelli sottostanti.

**Protocol Data Unit**
Il protocol data unit (PDU) è ciò che costituisce un pacchetto ed è l'unione di:
- **Protocol Control Information (PCI)**: È l'header di un pacchetto. Contiene i metadati necessari che garantiscono il corretto funzionamento del protocollo.
- **Service Data Unit (SDU)**: È il payload di un pacchetto. Contiene il contenuto informativo scambiato.
- Il PDU a livello N comprende il payload + l'header a livello N.

**Comunicazione e Standard**
La comunicazione tra nodi differenti e basati su piattaforme hardware/software eterogenee necessita di **STANDARD**. L'informatica conosce due modi per arrivare ad uno standard:
- Standard de iure.
- Standard de facto.

**Standard ISO/OSI**
