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
A livelli diversi il pacchetto assume un nome diverso. Nel livello H2N e nel livello fisico il package assume il nome di **frame**. I collegamenti tra nodi possono essere:
1) Host - Router/Switch
2) Router/Switch - Router/Switch.
3) Host - Host.

**Adattatori Comunicazione H2N**
Il protocollo H2N è implementato all'interno di una scheda adattatrice che tutti i dispositivi possiedono detta **Network Interface Card** o NIC.

**Network Interface Card**
È costituito da una RAM, un **Digital Signal Processor** o DSP, un'interfaccia bus/host ed un interfaccia di collegamento alla rete. È un **entità semi-autonoma** rispetto al dispositivo in cui risiede.

**Ethernet**
In origine Ethernet è stato pensato come topologia a **bus** e che fosse in grado di supportare 1-10Mbps. Al giorno d'oggi è utilizzato in topologie a **stella** ed è in grado di supportare GB/s.
- **Bus**: Un bus è un collegamento fisico dove tutti i nodi che partecipano alla rete sono collegati.

**Successo di Ethernet**
1) È relativamente economica
2) Si integra bene con i protocolli IP e TCP/IP
3) Si presta a diverse **topologie** (modi di connettere la rete) e **tecnologie**.

**Caratteristiche Ethernet**
Il protocollo Ethernet deve avere una gestione delle collisioni. È pensato per gli scambi di informazione broadcast dato che un sottoprotocollo gestisce le comunicazioni broadcast, questo **NON** vuol dire che l'Ethernet è un protocollo broadcast dato che **ACCETTA** anche comunicazioni Unicast.

- **Tipo di Collegamento**: Usa un canale di tipo **broadcast**, quindi tutti gli host sono connessi ad un canale di comunicazione. Quando un host riceve un pacchetto **TUTTE** le interfacce degli host collegati lo ricevono.
- **Modalità di Trasmissione**: Permette comunicazioni **UNICAST** fra host, solo alcuni messaggi "speciali" sono di tipo broadcast, servono per assicurarsi il corretto funzionamento del protocollo.

**Indirizzi Ethernet: MAC**

**Indirizzi Media Access Control (MAC)**
A livello Ethernet gli host utilizzano un indirizzo MAC. L'indirizzo è prima assegnato alla NIC che ha un indirizzo MAC al suo interno. È **univoco** e **permanente**, quindi è importante che due entità non abbiano lo stesso MAC address se collegati nella stessa rete ed è già assegnato fisicamente nei dispositivi che ne fanno uso. Non è accessibile dall'utente.

È grande 48bit ed è rappresentato solitamente in un formato esadecimale. I primi 3 byte possono essere utilizzati per identificare il produttore dell'interfaccia di rete. Gli amministratori di rete possono modificare l'indirizzo MAC per fare in modo di aver un produttore diverso.
- Es: `81:F4:A3:AA:9C:49.`

Esistono alcuni indirizzi speciali, uno di questi è `FF-FF-FF-FF-FF-FF` ed è chiamato indirizzo di broadcast. Questo è un indirizzo che l'host accetterà indipendentemente perchè è dedicato a lui.

**Frame Ethernet**
- **Preambolo**: Serve per far comunicare correttamente le interfacce a livello fisico. Essa richiede SOLO un preambolo ma non una parte conclusiva. È un campo composto da 8 byte; i primi 7 byte hanno valore `10101010,` l'ultimo byte ha valore `10101011.` Ciò serve per sincronizzare i clock.
- **Indirizzo Destinazione**: È un indirizzo MAC che verrà utilizzato per capire se è il pacchetto è destinato a lei o meno. In caso negativo il pacchetto verrà scartato, altrimenti viene accettato e propagato al SO. È essenziale per ottenere delle performance accettabili. Abbiamo un eccezione, possiamo dire all'SO di accettare tutto (modalità promiscua). Se essa è attiva allora non verrà fatto alcun filtraggio.
- **Indirizzo Sorgente**: È un indirizzo MAC che verrà utilizzato per ricevere il pacchetto.
- **Tipo**: È un campo grosso 2 byte che implementa un concetto di multiplexing. Serve a gestire in modo efficiente la ricezione dei messaggi. Se questo campo non ci fosse dovremmo fare un analisi nel payload, capire cosa c'è dentro il pacchetto e a chi inoltrarlo.
- **Dati**:
- **CRC**: Controllo a Ridondanza Ciclica, è un algoritmo che ha lo scopo di permettere all'adattatore che riceve i dati di rilevare la presenza di un errore nei bit di frame ricevuto. Il frame calcola il CRC in base al contenuto presente nel pacchetto.

**Protocollo ARP**
È un protocollo con cui due host possono comunicare per scambiare un indirizzo MAC. Si compone di due fasi;
1) Fase di richiesta, vede l'invio di un pacchetto che prenderà il nome di ARP Request. Esso verrà comunicato in modo broadcast, quindi a tutti gli host. L'input del protocollo ARP è l'indirizzo IP. Viene inviato l'indirizzo IP, dato che la comunicazione è broadcast tutti ricevono l'IP ed infine risponde l'host che lo contiene. La risposta è unicast, un nodo chiede l'informazione e quindi possiamo fare una comunicazione mittente-destinatario.
2) Fase di risposta