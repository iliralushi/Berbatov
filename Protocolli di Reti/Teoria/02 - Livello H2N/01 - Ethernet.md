**Scopo Livello H2N**
Nello stack TCP/IP i protocolli H2N sono strettamente dipendenti tra di loro. Il loro scopo è:
- **Interconnessione** tra due o più host;
- **Trasmissione dati** tra host già connessi;
- **Connessione** di un host ad Internet.

**Premessa Protocolli H2N**
I servizi offerti da differenti protocolli H2N possono essere diversi:
- Un protocollo può offrire l'affidabilità nella consegna di un pacchetto e un altro no. Sta al livello network adattarsi ai vari servizi offerti da diversi protocolli H2N e far si che venga compiuto il lavoro.

**Definizioni: Modalità di Trasmissione**
1) **Unicast**: Comunicazione tra un mittente ed un ricevente.
2) **Multicast**: Comunicazione tra un mittente e più riceventi.
3) **Anycast**: Comunicazione tra un mittente ed **almeno un** ricevente.
4) **Broadcast**: Comunicazione tra un mittente e **tutti** i nodi disponibili.

**Definizioni: Tipi di Collegamento**
- **Collegamento Broadcast**: Molti host sono connessi allo stesso canale di comunicazione. Necessario un protocollo che regoli le comunicazioni ed eviti le collisioni possibili; se un informazione arriva ad un host essa verrà trasmessa anche agli altri.
- **Collegamento Unicast**: Costituito da un singolo trasmittente da un estremo del collegamento (mezzo fisico) e da un singolo ricevente dall'altro estremo. Tipico collegamento fra due router o fra un modem e il router dell'ISP.

**Definizioni: Collegamento Unicast**
- **Collegamento Half-Duplex**: Collegamento che permette soltanto ad un estremità di comunicare dato un istante di tempo; A comunica a B o viceversa, non entrambe le cose.
- **Collegamento Full-Duplex**: Collegamento che permette ad entrambe le estremità di comunicare nello stesso istante di tempo. 

**Attenzione**
A distinguere le **modalità di trasmissione** e le **caratteristiche del mezzo trasmissivo**
- Il protocollo H2N può essere progettato per un mezzo trasmissivo che può essere unicast/broadcast, ciò non vuol dire che non possiamo avere diverse modalità di trasmissione (broadcast, unicast, multicast...) 
- I collegamenti quindi non sottointendono i livelli inferiori; un primo livello unicast non prelude il fatto che anche il secondo lo debba essere.

**Livelli Offerti da H2N**
1) **Fisico**: Connessione tra host per mezzi fisici come cavi, modem, fibra ottica...
2) **Data Link**: Gestisce la trasmissione di dati tra due nodi direttamente collegati in LAN.

**Collegamenti Livello H2N**
I collegamenti tra nodi possono essere:
1) Host - Router/Switch
2) Router/Switch - Router/Switch.
3) Host - Host.

**Adattatori Comunicazione H2N**
Il protocollo H2N è implementato all'interno di una scheda adattatrice che tutti i dispositivi possiedono (per poter essere utilizzati in una rete LAN) detta **Network Interface Card**.

**Network Interface Card (NIC)**
È costituito da una RAM, un **Digital Signal Processor** o DSP, un'interfaccia bus/host ed un interfaccia di collegamento alla rete. È un **entità semi-autonoma** rispetto al dispositivo in cui risiede.

**Ethernet**
In origine Ethernet è stato pensato come topologia a **bus** e che fosse in grado di supportare 1-10Mbps. Al giorno d'oggi è utilizzato in topologie a **stella** ed è in grado di supportare GB/s.
- **Bus**: Un bus è un collegamento fisico dove tutti i nodi che partecipano alla rete sono collegati.

**Successo di Ethernet**
1) È relativamente economico
2) Si integra bene con i protocolli IP e TCP/IP
3) Si presta a diverse **topologie** (modi di connettere la rete) e **tecnologie** (tecnologia del mezzo trasmissivo usato per le connessioni).

**Caratteristiche Ethernet**
Il protocollo Ethernet **deve** avere una gestione delle collisioni. È pensato per gli scambi di informazione broadcast dato che un sottoprotocollo gestisce le comunicazioni broadcast, questo **NON** vuol dire che l'Ethernet è un protocollo broadcast dato che **ACCETTA** anche comunicazioni Unicast.

- **Tipo di Collegamento**: Usa un canale di tipo **broadcast**, quindi tutti gli host sono connessi al canale di comunicazione. Quando un host riceve un pacchetto **TUTTE** le interfacce degli host collegati lo ricevono.
- **Modalità di Trasmissione**: Permette comunicazioni **UNICAST** fra host, solo alcuni messaggi "speciali" sono di tipo broadcast, servono per assicurarsi il corretto funzionamento del protocollo.

**Indirizzi MAC**
A livello di Ethernet gli host per comunicare usano un indirizzo hardware detto **indirizzo MAC**. Rappresenta l'indirizzo della **NIC** di un **SINGOLO** host, quindi è **univoco** e **permanente** per ogni entità. È importante che due entità non abbiano lo stesso MAC address quando sono connesse nella stessa rete perchè potremmo avere conflitti:
- Per esempio, possiamo ricevere un pacchetto in due nodi della rete quando era destinato ad un solo host, per esempio.

L'indirizzo è grande 48 bit (6 byte) ed è costituito generalmente da 6 coppie di numeri esadecimali. Esistono anche degli indirizzi speciali come l'indirizzo broadcast.
- Esempio MAC: `81:F4:A3:AA:9C:49`
- Esempio MAC speciale: `FF:FF:FF:FF:FF:FF`(indirizzo broadcast, accettato indipendentemente dall'host perchè è un indirizzo dedicato a lui.)

I primi 3 byte rappresentano il produttore dell'interfaccia di rete. Gli amministratori di rete possono manipolare questi primi 3 byte per modificare l'indirizzo MAC in modo da registrare un produttore diverso.

**Indirizzi Host**
- Ciascun **host** di una LAN ha un **indirizzo IP**.
- Ciascun **NIC** di un entità ha un **indirizzo MAC**

**Utilizzo Indirizzo MAC**
1) Quando un host vuole trasmettere, **inserisce nel frame** l'indirizzo MAC del destinatario e lo invia nella LAN - che è un canale di broadcast.
2) Se l'indirizzo MAC immesso nel frame coincide con l'indirizzo MAC contenuto nella NIC dell'host destinatario allora viene accettato e lo passa **all'SO** dell'host che gestisce gli altri livelli dello stack TCP/IP.
3) Se l'indirizzo MAC immesso nel frame **NON** coincide con l'indirizzo MAC contenuto nella NIC dell'host destinatario allora viene scartato senza coinvolgere l'SO.

**Non Basta l'Indirizzo IP**
Se i NIC usassero indirizzi IP al posto di indirizzi MAC **indipendenti**:
1) Avrebbero un supporto limitato di altri protocolli; supporterebbero solo quello IP.
2) Gli indirizzi IP dovrebbero essere **registrati** nella memoria del NIC, quindi **riconfigurati** ogni volta che l'host cambia rete.

Se i NIC non utilizzassero alcun indirizzo:
1) Ogni frame ricevuto verrebbe passato dal NIC all'host su cui attualmente si trova per verificare se l'indirizzo IP coincide.
2) Gli SO di **TUTTI** gli host compresi nel percorso tra mittente e destinatario verrebbero interrotti; non abbiamo modo di verificare se il frame è destinato a loro o meno.

**Frame Ethernet**
I pacchetti scambiati a livello H2N vengono chiamati **frame**. Tutte le tecnologie Ethernet fanno uso dello stesso standard per il frame trasmesso (**Frame Ethernet**). Il frame è composto da diversi campi.
1) Preambolo - 8 bytes.
2) Indirizzo destinazione - 6 bytes.
3) Indirizzo sorgente - 6 bytes.
4) Tipo - 2 bytes.
5) Dati - 46/1500 bytes.
6) CRC - 4 bytes.

**Preambolo**
Possiamo vedere il campo del preambolo come composto da due parti:
1) I primi 7 byte hanno valore `10101010` e servono per far comunicare correttamente le interfacce dei riceventi a livello fisico e **sincronizzare** i cicli di clock con quelli del mittente.
2) L'ultimo byte ha valore `10101011` e serve per **avvisare** al NIC del ricevente che la fase di sincronizzazione è terminata e che sta arrivando il vero contenuto del frame.

**Indirizzo Destinazione e Sorgente**
Sono due campi che contengono l'indirizzo MAC rispettivamente dell'host che dovrà ricevere il pacchetto e del mittente. Quando un NIC riceve un frame Ethernet con **Indirizzo Destinazione** diverso dal proprio indirizzo MAC allora scarta il pacchetto, altrimenti passa il contenuto del campo dati all'SO dell'host in cui risiede.
- **Modalità Promiscua**: Possiamo dire all'SO di accettare tutto; se essa è attiva non verrà effettuato alcun filtraggio dei frame.

**Tipo**
Il campo tipo permette ad Ethernet di **multiplexare** i protocolli del livello di rete. Serve all'adatattore per capire a quale **protocollo del livello di rete** deve essere inviato il campo dati di ogni frame ricevuto. È molto più **efficiente** rispetto ad analizzare il payload.

**Dati**
Il campo dati contiene i dati reali - l'unità massima trasferibile per Ethernet si chiama **MTU** (Maximum Transfer Unit) ed è di 1500 byte. La dimensione minima è di 46 byte.
- **Stuffing**: Processo che **inserisce byte riempitivi** nel campo dati in caso non si raggiunga la dimensione minima. Questi byte verranno poi scartati alla ricezione del pacchetto.

**Controllo a Ridondanza Ciclica (CRC)**
Il campo CRC è un algoritmo che permette all'adattatore che riceve dati di **rilevare errori nei bit del frame ricevuto.** Quando un host trasmette il frame calcola un campo CRC. Ciò viene svolto anche quando un host riceve il frame.
- Se i CRC coincidono allora il frame è **giusto**, altrimenti si avrà un errore.

**Protocollo Per Risoluzione Indirizzi**
Gli indirizzi IP non sono riconosciuti dall'hardware, se conosciamo direttamente l'indirizzo IP di un host sarebbe impossibile trovare l'indirizzo MAC. Il **protocollo ARP** (Address Resolution Protocol) permette di trovare l'indirizzo MAC di un host della stessa LAN usando l'indirizzo IP - quindi di abilitare la comunicazione tra due host.

**Protocollo ARP**
Utilizza due messaggi di tipo ARP:
1) **Fase di Richiesta**: Viene inviato un pacchetto di nome **ARP Request** che verrà comunicato in broadcast, quindi tutti gli host riceveranno questo pacchetto. Risponde all'ARP Request solo l'host destinatario, ovvero l'host con indirizzo IP combaciante con l'IP contenuto nell'ARP Request.
2) **Fase di Risposta**: Una volta svolta l'ARP Request con successo l'host mittente riceve un **ARP Reply** (in modalità unicast) dall'host destinatario che contiene il suo indirizzo MAC. In questo modo abilitiamo una comunicazione mittente-destinatario.

**Ottimizzazione Prestazioni ARP**
La **Cache ARP** serve per ridurre il carico dei messaggi ARP sulla rete.
- **Ciascun host** memorizza temporaneamente (caching) nell'**ARP Table** la coppia indirizzo IP/MAC una volta trovati. In questo modo non dobbiamo inviare una nuova ARP Request per ogni interazione tra i due host.
- Il mittente inserisce nell'ARP Request la sua coppia indirizzo IP/MAC. In questo modo anche il destinatario può aggiornare la propria ARP Table con la coppia di indirizzi.
- È presente un campo TTL che ci indica quanto tempo una coppia di indirizzi rimarrà nell'ARP Table.

**Funzionamento Protocollo ARP**
1) Controllare se l'indirizzo IP (input dell'ARP Request) è presente nell'ARP Table.
2) Se assente o è scaduto il TTL allora **viene eseguito il protocollo ARP** per trovare nuovamente l'indirizzo IP e di conseguenza trovare l'indirizzo MAC del destinatario.
3) Uso il MAC Address ottenuto dall'ARP Reply come destinazione dei frame da inviare.
4) Il protocollo ARP viene eseguito periodicamente **in parallelo** per verificare le corrispondenze IP/MAC e per aggiornare il TTL delle entries nell'ARP Table.

**Protocollo RARP (Deprecato)**
- Meccanismo analogo al protocollo ARP.
- Funzione opposta. Invece di prendere in input un indirizzo IP prende in input l'indirizzo MAC, quindi restituirà in output l'indirizzo IP associato.

**Protocollo di Accesso Multiplo**
I frame Ethernet vengono trasmessi dagli host sullo stesso segmento di LAN. Esso si trova su un **canale condiviso broadcast** a bitrate elevato (**modello di accesso multiplo**) e la spedizione contemporanea aumenta il rischio di **collisioni**.

È necessario **un protocollo di accesso al mezzo** per coordinare le trasmissioni condivise e fare in modo di evitare le collisioni. Se questo non fosse possibile il protocollo deve gestirle al meglio.

**Protocollo CSMA/CD**
- Protocollo ad **accesso casuale**.
- Protocollo completamente **decentralizzato.**
- Quando un host **deve** trasmettere ascolta il canale.
- Quando un host **trasmette** lo fa alla massima velocità consentita dal canale.
- Quando un host rileva una **collisione** ri-trasmette il frame finchè si ha successo.
- L'host attende un periodo di tempo calcolato semi-casualmente per la ri-trasmissione di un pacchetto in collisione.

**Carrier Sense (CS)**
Ogni host che deve trasmettere ascolta il canale fisico e decide di trasmettere solo se il canale è libero.

**Inter Frame Gap (IFG)**
È l'intervallo di tempo tra due frame consecutivi; precisamente il tempo corrisponde alla lunghezza del pacchetto dati più piccolo. Serve per garantire agli host sulla rete di poter distinguere la fine della trasmissione di un frame dall'inizio della trasmissione successiva.
- Prima di iniziare la trasmissione del primo frame **un host deve aspettare un tempo IFG per assicurarsi che il canale sia libero.**

**Multiple Access (MA)**
Dato che il protocollo è decentralizzato il CS non è abbastanza per regolare le trasmissioni, in questo modo due host possono decidere di trasmettere allo stesso momento. Dato che il segnale impiega un po' di tempo per inviarsi sulla rete l'host può assumere che il mezzo sia libero **anche se un altro host ha iniziato a trasmettere**.

**Collision Detection (CD)**
Se si verifica una **sovrapposizione** di trasmissioni si ha una collisione. Ogni host mentre trasmette ascolta i segnali sulla rete confrontandoli con quelli propri, in questo modo si possono rilevare le collisioni. Una volta rilevata l'host **interrompe la trasmissione**.

**Gestione Delle Collisioni**
1) Ogni host sospende la trasmissione e trasmette un segnale di **JAMMING** (disturbo composto da 48 bit) per avvisare gli altri host che c'è una collisione in corso. Il segnale assicura che gli host sappiano della collisione, anche se di breve durata.
2) Gli host trasmittenti riprovano la trasmissione dopo un ritardo (semi-casuale) generato da un algoritmo di **exponential back-off** e ri-trasmettono fino ad un massimo di 16 volte.

**Binary Exponential Back-Off (BEB)**
- Il ritardo è di `K * 512` intervalli di tempo. K dipende dal numero di collisioni già rilevate.
- La cardinalità dell'insieme da cui vien scelto K cresce **esponenzialmente** con il numero delle collisioni.

**Ethernet Approccio BEB**
- **Prima Collisione**: Sceglie tra l'insieme `{0,1}.`
- **N-esima Collisione**: Sceglie K tra `{0, 1, ... , 2 ^ Collisione - 1}.`
- **Da 10 a 15 Collisioni**: Scegli tra K `{0, ... , 1023}.`
- **16 Collisione**: Rinuncia.

**Attesa Esponenziale BEB**
Lo scopo è di **stimare il livello di carico della rete** per adattare i prossimi tentativi della ri-trasmissione. Tramite l'incremento esponenziale dell'insieme da cui K viene preso l'host **gestisce meglio la ri-trasmissione a seconda della situazione del traffico.**
- **Basso ritardo** se la collisione è leggera, **alto ritardo** se abbiamo un sovraccarico.
 
**Pseudocodice Algoritmo CSMA/CD**

```
A = Controlla il canale.

if (A = libero) then
{
	Trasmetti e controlla il canale;
	
	if (Scopri un'altra trasmissione) then
	{
		Smetti e manda il segnale di jamming;
		Incrementa il numero di collisioni;
		Usa l'algoritmo BEB per calcolare il tempo del ritardo;
		goto A;
	}
	else
	{
		Una volta finita la trasmissione del frame setta n. collisioni = 0;
		Attendi un intervallo pari a IFG;
		goto A;
	}
}
else
{
	Aspetta finchè la trasmissione corrente è finita;
	goto A;
}
```