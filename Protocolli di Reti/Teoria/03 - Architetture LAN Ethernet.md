**Rete Local Area Network (LAN)**
Una LAN è una rete dove i nodi partecipanti possono comunicare tra loro utilizzando i protocolli di livello H2N direttamente.

**Motivazioni LAN**
Le LAN sono le reti più diffuse perchè sono estremamente versatili, inoltre utilizzano tecnologie e architetture **ben consolidate e poco costose**.

**Back-End LAN + Backbone LAN**
- **Back-End LAN**: LAN che comprendono gli elementi dell'accesso ad Internet. Interconnettono dispositivi in modo da creare un sistema di medie dimensioni.
- **Backbone LAN**: Interconnettono varie back-end LAN in modo da creare reti LAN di dimensione maggiore.

**Topologie per LAN e Interconnessioni di LAN**
A seconda dei contesti e dei protocolli abbiamo diverse tipologie LAN:
- A bus, ad anello, a stella, ad albero...

**Topologia a Bus**
Tutti gli host sono connessi tramite un cavo chiamato **dorsale** o **segmento**. I messaggi sono inviati a tutti gli host come segnali elettrici; vengono accettati dal NIC dell'host se l'indirizzo MAC coincide con l'indirizzo MAC del segnale di partenza.

- Se un host trasmette dati e nessuno li riceve allora l'host **viaggia da un capo all'altro** fino a tornare all'origine. Non potranno essere inviati altri segnali durante questo tempo.
- Il **terminatore** è un dispositivo che viene applicato alle estremità del cavo. Assorbe i dati non ricevuti, quindi pulisce il cavo da dati rimanenti, riprendendo la comunicazione.
- Se il cavo viene tagliato oppure uno dei due host viene scollegato (**comporta non avere più un terminatore)** i dati rimbalzeranno all'infinito, causando una **rete inattiva**.

**Modalità per Trasmissione su Bus**
1) Abbiamo tre host. L'host A si prepara ad inviare il frame. Il destinatario è l'host C.
2) Il frame arriva all'host B, quindi controlla se il frame è destinato a lui, vede che gli indirizzi MAC non coincidono ed ignora il pacchetto.
3) L'host C riceve il frame dato che i MAC coincidono e passa il payload agli stack superiori. Il frame continua a viaggiare fino all'estremo del cavo, dove i suoi dati verranno assorbiti dal terminatore.

**Topologia ad Anello**
Gli host sono connessi tramite un cavo circolare **senza terminatori**. I segnali sono inviati tramite il percorso chiuso e passano per ogni host che svolgono la funzione di **ripetitore**. Il frame viene quindi ri-trasmesso fino ad arrivare al mittente che lo assorbirà.

**Modalità di Trasmissione su Anello**
1) Abbiamo tre host. L'host A si prepara ad inviare il frame. Il destinatario è l'host C.
2) L'host B riceve il frame, dato che non è il destinatario lo inoltra.
3) L'host C riceve il frame, è il destinatario e quindi accetta il payload e rinvia il frame.
4) Il frame ritorna all'host A ed assorbe il frame immesso nella rete.

**Topologia a Stella**
**Un dispositivo di rete speciale** è al mezzo della rete. Gli host verranno connessi tramite dei cavi, uno per host. I messaggi **vengono gestiti interamente dal dispositivo centrale**.
- Al giorno d'oggi le reti Ethernet sono progettate con topologia a stella.
- Se smette di funzionare un cavo che collega l'host al dispositivo centrale allora solo quell'host verrà escluso dalla rete.
- Se smette di funzionare il dispositivo centrale allora la rete si interrompe totalmente.

**Pro + Contro Topologia a Stella**
- **PRO**: Topologia molto più robusta e, a seconda del dispositivo centrale è possibile diminuire le interferenze nella rete.
- **CONTRO**: Il traffico risiede tutto nel dispositivo centrale. Serve un dispositivo con capacità adeguata.

**Internet Come Unica Rete LAN?**
I protocolli di livello H2N sono pensati per essere molto veloci e flessibili. 
Ci sono compromessi tra velocità, flessibilità e **scalabilità**. Le reti LAN peccano sulla scalabilità; se abbiamo un numero elevato di nodi connessi allora le prestazioni delle reti LAN **calano a dismisura**. Non possiamo avere Internet come unica rete LAN.
- **Scalabilità**: Capacità di mantenere le prestazioni all'aumentare del carico di lavoro.

**Dispositivi di Rete**
Abbiamo diversi dispositivi di reti dipendenti da; topologie di interconnessione di host, numero di host collegati, efficienza delle comunicazioni:
- Hub (Livello 1) - Switch (Livello 2&3) - Bridge (Livello 2&3)

**Osservazioni su Termini**
- **Hub**: Indica un dispositivo fisico che implementa la funzionalità di **ripetitore**.
- **Bridge**: Indica le funzionalità che sono implementate su **software**.
- **Switch**: Indica un dispositivo fisico che implementa le funzionalità di tipo **bridge.**
- Hub e Switch sono soluzioni alternative anche se ormai gli hub son **deprecati**.

**Hub**
È un dispositivo di **livello fisico** dotato due o più interfacce. È un **ripetitore** che agisce sui bit singoli dato che è un dispositivo di livello 1.
- Si occupa di ripetere i bit ricevuti su un'interfaccia a tutte le altre.
- Tutti i nodi connessi fanno parte dello stesso **segmento** di LAN. I frame vengono ricevuti da ogni dispositivo, indipendentemente dal destinatario.

**Vantaggi Hub**
- È un dispositivo semplice ed economico, usato nelle LAN con poco traffico.
- Estende la **massima distanza** fra coppie di nodi.
- È **trasparente** quindi l'hub funziona senza modifiche agli adattatori LAN degli host.
- Un guasto su un segmento LAN esclude soltanto l'host in considerazione.

**Svantaggi Hub**
- **Gli hub NON isolano il dominio delle collisioni**. Il traffico inviato da un host può collidere col traffico inviato da un altro host connesso in un qualsiasi segmento della LAN che è collegato all'hub. In pratica, una rete implementata con questo dispositivo si comporta come una **topologia a bus** (con la differenza sui guasti).

**Switch**
È un dispositivo di **livello fisico** che implementa le funzionalità di inoltro dei frame. Ha molte interfacce di rete e viene usato come **centro** nelle topologie a stella. Quando un frame deve essere inoltrato il **bridge** usa il protocollo CSMA/CD per trasmettere.
- Inoltro di frame a livello 2.
- Filtraggio con indirizzi MAC.

**Vantaggi Switch**
- **Isola i domini di collisione** aumentando il traffico totale gestibile. Non impone limiti su numero di host nè sulla copertura geografica.
- Può connettere tipi diversi di Ethernet. È un dispositivo **store-and-forward**.
- È **trasparente** quindi lo switch funziona senza modifiche agli adattatori LAN degli host.
- Abbiamo **accesso dedicato** e tipo di collegamento **full-duplex**.
- ***NB: Dominio Collisioni != Dominio Broadcast***.

**Switching**

![Switching](Switching.jpeg)

**Metodi di Filtraggio & Inoltro**
Gli switch **identificano** gli host collegati a ciascuna interfaccia.
- Usano delle **tabelle di filtraggio** generate automaticamente dallo switch.
- Alla ricezione del frame lo switch **impara** la posizione del mittente e la registra nella tabella di filtraggio.
- Il **record** inserito nelle tabelle comprende; MAC address, interfaccia switch, TTL.
- Il record viene eliminato dalla tabella una volta che si supera il TTL.

**Filtraggio & Inoltro di Frame**
I meccanismi di filtraggio e inoltro diretto consentono l'aumento di **capacità** della rete Eth.
- **Filtraggio**: I frame destinati a host dello stesso segmento **NON** vengono inviati agli altri segmenti della LAN.
- **Inoltro**: Usando un meccanismo di **auto-apprendimento** ottimizziamo l'invio dei frame sfruttando la tabella di filtraggio. Ci consente di memorizzare indirizzi MAC usando le informazioni date da un precedente scambio di frame.

**Auto-Apprendimento**

![[Self-Learn.jpg]]

**FASE 1 - C -> D**
1) C si prepara a mandare il frame a D. C non ha informazioni su D quindi si presta ad inviare il frame ai segmenti 2 e 3 della rete.
2) Usando la tabella lo switch rileva che D si trova nell'interfaccia 2 della rete quindi il segmento 3 scarta automaticamente il frame.
3) Il frame raggiunge D.

**FASE 2 - D -> C**
1) D risponde con un frame dedicato a C. Lo **switch bridge** rileva un frame proveniente dal MAC address di D quindi nota che D è sull'interfaccia 2.
2) Dato che lo switch ha appreso in precedenza l'interfaccia del destinatario (C) il frame viene **inoltrato direttamente nel segmento 1**.
3) Il frame raggiunge C senza fare un check sugli altri segmenti.

**Svantaggi Auto-Apprendimento**
Se un host A **viene spostato di segmento** i frame destinati a lui verranno inoltrati nel segmento sbagliato. Ciò succede finchè:
1) A invia un frame. Verrà aggiornata l'interfaccia nella tabella di filtraggio.
2) Il TTL della entry scade. L'entry viene cancellata, quindi aggiornata.

**Tipi di Instradamento per Switch**
- **Store-And-Forward**: Il frame viene raccolto ed immagazzinato **nella sua totalità** prima di essere inoltrato dallo switch.
- **Cut-Through**: Il frame viene inoltrato nella porta di uscita dallo switch **appena riceve l'indirizzo di destinazione**, non aspetta l'intero frame. È più veloce ma possono verificarsi errori di integrità del pacchetto.

**Bridge**
È un dispositivo di **livello 2**. Controlla gli header dei vari frame e li inoltrano **direttamente** nell'interfaccia nell'host che ha come MAC address quello contenuto nel campo Dest.
- È analogo allo switch, può supportare **più mezzi fisici**.

**Bridging**
- **Bridging Trasparente**: Collega due dispositivi fisici che usano lo stesso **tipo di indirizzamento** di LV2 (MAC, ARP...) senza modificare il frame.
- **Bridging Non Trasparente**: Lo switch implementa logiche per convertire i protocolli di LV2. Le logiche usate dipendono **dai protocolli** da convertire.

**Bridge e Switch**
Lo switch può essere considerato come un tipo particolare di **bridge trasparente** con un numero elevato di porte disponibili;
- Analizza il LV2 dei frame e separa i **domini di collisione**, quindi separa i due mezzi fisici impedendo la collisione di frame tra host.
- Supporta collegamenti fisici a **velocità di trasferimento diverse**.