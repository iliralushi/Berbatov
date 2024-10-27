I servizi offerti da differenti protocolli h2n possono essere affidabili nella consegna del pacchetto come non possono esserlo.

**Modalità di Trasmissione**
- **Unicast**: Comunicazione fra un singolo mittente ed un singolo ricevente.
- **Multicast**: Comunicazione fra un singolo mittente ed un gruppo di riceventi.
- **Anycast**: Comunicazione fra un singolo mittente ed **ALMENO** un ricevente.
- **Broadcast**: Comunicazione fra un singolo mittente e tutti gli altri nodi.

**Tipi di Collegamento**
- **Collegamento Unicast**: Collegamento punto-punto, costituito da un unico trasmittente dove un estremità viene attaccata in un dispositivo e l'altra in un altro dispositivo.

- **Collegamento Broadcast**: Molti host sono connessi ad uno stesso canale di comunicazione. Quando arriva un informazione ad un host esso verrà trasmesso a tutti gli altri (LAN, WLAN...). 
  
I collegamenti non sottintendono i livelli inferiori. Se un primo livello è un tipo di collegamento unicast ciò non vuol dire che ad un livello inferiore abbiamo un altro collegamento unicast. Il livello fisico e logico son separati.

**Collegamenti Punto-Punto**
- **Half-Duplex**: Collegamento in cui le comunicazioni possono andare in una direzione (A che comunica a B o viceversa, non entrambi).
- **Full-Duplex**: Dato un certo canale di comunicazione possiamo comunicare contemporaneamente in entrambe le direzioni (A può comunicare a B, B può comunicare ad A).

**Collegamenti del Livello H2N**
A livelli diversi il pacchetto assume un nome tecnico diverso. Nel livello H2N e fisico il package viene chiamato **frame** (deriva da framing).
- **Framing**: Una sequenza di dati che è composta da 0 ed 1 che variano nel tempo per sincronizzare i cicli di clock.

**Adattatori per la Comunicazione H2N**
Il protocollo H2N è solitamente implementato all'interno di una **scheda adattatrice** conosciuta anche col nome di Network Interface Card (NIC).

**Network Interface Card**
Dispositivo generalmente costruito da una RAM, un **DSP** (Digital Signal Processor), un'interfaccia bus e un'interfaccia di collegamento alla rete (Connettore RJ45). La NIC è un entità semi-autonoma rispetto al sistema in cui risiede.

**Ethernet**
L'ethernet è stato progettato per funzionare in un solo canale di tipo **bus** a velocità 1/10Mbps.
- **Bus**: Collegamento fisico dove tutte le entità che partecipano in una rete sono collegati (rete condivisa).

Il protocollo Ethernet deve avere una gestione delle collisioni. È pensato per le comunicazioni broadcast dato che ha un sottoprotocollo che le gestisce. **Non è SOLO un protocollo broadcast!**

**ricordarsi di vedere la roba di ethernet non pensato solo al protocollo broadcast balblabla**

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