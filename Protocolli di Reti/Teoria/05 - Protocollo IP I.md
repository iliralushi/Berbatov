Possiamo usare il protocollo IP per identificare reti intere invece di singoli indirizzi

3 classi utilizzabili per indirizzo di host
- Classe a = 1 byte di netid
- Classe b = 2 byte di netid
- Classe c = 3 byte di netid

La notazione classless (CIDR, classless inter-domain routing) è la notazione più usata al giorno d'oggi. Usiamo la solita notazione dotted e lo separiamo con uno slash ed un numero per indicare quanto è grande il nostro netid. Elimina l'usaggio delle classi prestabilite e forza un tipo di classe. Il valore n è la netmask dell'indirizzo di rete (netmask in formato compresso).

Esistono indirizzi IP speciali che non possiamo assegnare altri sono indirizzi che possiamo assegnare per alcuni ruoli specifici.
- Network address: un indirizzo ip in cui il campo relativo all'hostid è uguale a 0. Sono tutti indirizzi che non possiamo assegnare ad host perchè sono tutti gli indirizzi dedicati a rappresentare delle reti già assegnate.
- Directed broadcast address: è un indirizzo di broadcast che rappresenta l'indirizzo di brodacast per una specifico indirizzo ip. Mettiamo tutti i bit a 1 dell'hostid. Permette il broadcast a tutti gli host di una certa rete, anche non solo fisica.
- Limited broadcast address: tutti i bit sono uguali ad uno. Subnet mask. Rimane sempre nella rete fisica, non inoltreranno mai un packet broadcast fatto in questa maniera. 255.255.255.255, possiamo lavorare solo sulla singola rete fisica.
- Nessun indirizzo IP: tutti i bit sono uguali a zero (0.0.0.0). Indirizzo IP che ha come valore null.
- Loopback address (localhost): 127.0.0.1, è un indirizzo software che serve per relegare se stessi. Questo non è un indirizzo ma è una rete.

La formula per calcolare il numero di indirizzi possibili è $2$ ^ $(num bit - bit netmask)$

Il subnetting è la scomposizione di una rete in più reti. A partire da un indirizzo ip ne dobbiamo creare un altro a patto che stia all'interno della rete. Per creare un altra rete da una rete principale assegnamo due subnetid differenti. Con due reti una sarà a 0 e l'altro a 1. Ogni volta che spezzo la rete perdo qualche indirizzo assegnato.

In una suddivisione di reti non bisogna mai creare sovrapposizioni.

**Routing**
Ogni host e ogni router hanno una tabella di routing. Ogni nodo della rete ip deve sapere come aggiungere qualsiasi destinazione di quella rete ip. Il percorso dei pacchetti viene selezionato hop-by-hop. La tabella è composta da due colonne; la destinazione che dice dove andrà a finire i nostri dati ed il metodo utilizzato (h2n, ip...) che stabilisce il protocollo utilizzato.

4 componenti fondamentali nell'architettura di un router:
- Una porta di ingresso; c'è una parte dove arriva il cavo fisico, una parte che analizza il frame ethernet e una coda (buffer) dove il pacchetto viene memorizzato in attesa dello switcher fino a poi inviare il pacchetto. Il riempimento di questa coda può causare dei problemi; la memoria può riempirsi, finisce la memoria e avremo una perdita di pacchetti. Oltre al caso estremo se un pacchetto rimane troppo nella coda avremo comunque un aumento della latenza, quindi dobbiamo avere una logica di routing efficiente.
- Un commutator; la logica dell'invio del pacchetto. Possiamo avere una comunicazione di tipo arp dove tutto è condiviso, tipo bus, oppure di tipo mesh dove possiamo far comunicare una qualsiasi porta di ingresso con una qualsiasi porta di uscita.
- Un processore di routing che decide come azionare questa logica. Abbiamo una coda in uscita che si riempie quando la velocità con cui inseriamo i pacchetti è più lenta del numero di pacchetti in uscita. Quando una coda si riempie diciamo che abbiamo una congestione, quindi un riempimento del buffer. La coda è una coda first in first out. 

In teoria le logiche di progettazione del router dovrebbero essere compliant al net neutrality.

**Indirizzi IP pubblici**
Un indirizzo IP pubblico è un indirizzo IP che possiamo utilizzare nella rete globale, quindi un indirizzo che possiamo utilizzare per comunicare direttamente. 

La IANA (Internet assigned numbers authority) è un organizzazione che si occupa di assegnare gli indirizzi IP. Serve un organizzazione centralizzata perchè gli indirizzi IP sono relativamente pochi, quindi per non causare conflitto abbiamo un organizzazione centralizzata che risolve questo problema.

La ICAAN gestisce l'assegnazione degli indirizzi IP e non solo. Non ci affidiamo direttamente a IANA/ICAAN ma a delle organizzazioni intermedie; ne abbiamo una per ogni continente. 

In Europa abbiamo RIPE.
Per comunicare su internet noi non comunichiamo direttamente con RIPE ma con un ISP (internet service provider). ICAAN si occupa di gestire tutti gli indirizzi IP; RIPE ha un certo range di indirizzi e a sua volta gli ISP prenderanno un altro numero di indirizzi. Dipende dalla grandezza dell'ISP, può essere locale come può essere mondiale.

GARR comunica con RIPE ed è un organizzazione italiana che riceve indirizzi da RIPE e gestisce le reti/indirizzi IP dedicati alla ricerca/università. Unimore per esempio ha come IP 155.185.0.0/16.

**Indirizzi privati (non routable)**
Gli indirizzi privati sono gli indirizzi che non possiamo esporre pubblicamente, quindi usare globalmente.

La funzionalità di NAT è una funzionalità tale per cui il router di bordo di questa rete ha disposizione di indirizzi IP e ogni volta che questo router vuole comunicare con l'esterno si occupa di sostituire i pacchetti IP da privati a pubblici. Fa in modo di non far andare mai l'IP privato sulla rete globale, viene quindi sostituito da un altro IP pubblico. Per gestire correttamente il multiplexing tra tanti host dobbiamo sfruttare il livello 4. Il NAT è un protocollo di livello 3 di base, nel suo uso più comune è di livello 3 e 4.

Un router normale inoltra i pacchetti così come sono se non siamo in presenza di NATting. Presi due host uno con indirizzo 1.1.1.1 e uno con 2.2.2.2 e un router che a destra avrà 1.1.1.254 e a sinistra 2.2.2.254. A destra l'indirizzo di sorgente sarà 1.1.1.1 e di destinazione 2.2.2.2. Ciò avverrà anche nell'altra metà.

Il NATting è positivo perchè con un IP privato il resto del mondo non può accedere.

Quando configuriamo una rete con IP privati dobbiamo usare un indirizzo IP non routable. Abbiamo un intervallo di indirizzi per classi:
- 10.0.0.0 - 10.255.255.255 indirizzi di classe A (10.0.0.0/8)
- 172.16.0.0 - 172.31.255.255 indirizzi di classe B (172.16.0.0/12)
- 192.168.0.0 - 192.168.255.255 indirizzi di classe C (192.168.0.0/16)

Gli indirizzi privati possono essere solo all'interno di questo range.

La rete locale è la rete H2N, la rete privata è una rete che indica una rete non routable ma anche loro possono avere tante reti LAN, quindi non hanno bisogno di comunicare con NATting che lo abbiamo una volta che usciamo dalla rete locale.

**Datagram IPV4**
Tutto il traffico di internet consiste in pacchetti, ciascun pacchetto è lungo fino a 64kb.
Il pacchetto è allineato a 4 byte:
- Vers: primi 4 bit, questo campo identifica la versione del protocollo.
- Hlen: questo campo contiene la dimensione dell'header. Esprime il numero di word (parole) dell'header. Il campo sarà grande hlen * 4 byte. L'header ip è grande 20 byte in ipv4.
- Type of service (service type): è un intero byte, son dei tipi di flag che comunicano il tipo di priorità che il pacchetto che stiamo trasferendo ha (de iure). Adesso il campo serve per gestire delle classi di traffico.
- Total length: Sono 16 bit, questo campo definisce il numero di **byte** che può contenere un pacchetto. Se abbiamo 16 bit riusciamo a rappresentare un massimo di 64kb, il dato detto precedentemente.
- Identification: È un campo che serve ad identificare i pacchetti ip.
- Flags: Sono legati al controllo della frammentazione (flag to not fragment).
- Fragmented offset: Identificativo che stabilisce in quale posizione è il singolo frammento all'interno di uno stesso identificativo. Il campo si chiama offset perchè inseriamo l'offset del frammento del pacchetto intero, è una posizione. Ogni frammento ha un header ip indipendente.
- Time to live: Non esprime un tempo ma esprime quanti router potrà ancora attraversare il pacchetto. Quando un host h1 invia un pacchetto imposta un campo ttl iniziale dove il valore dipende dal sistema operativo. Ogni volta che il pacchetto ip arriva ad un router il router decrementa di 1 il ttl, se il nuovo valore del ttl = 0 allora il pacchetto vien droppato altrimenti viene inoltrato. Se un pacchetto percorre un ciclo/percorre un percorso molto lungo questo campo permette di droppare il pacchetto in questo caso. La logica di ttl può essere legata anche a logiche di segnalazione (pacchetti di segnalazione vedremo + avanti)
- Protocol: Questo è un campo che ci da l'informazione sul protocollo IP utilizzato nel payload.
- Header checksum: Questo è un campo che è legato alla logica di integrità. Serve quindi a verificare l'integrità dell'header del pacchetto. Non garantiamo quindi l'integrità sui dati, un pacchetto IP può avere come un payload modificato mentre è in transito. Se abbiamo NATting allora il checksum va ricalcolato altrimenti da errore di integrità.
- Source ip address (32 bit): 
- Destination ip address (32 bit):

Parliamo di frammentazione quando spezziamo un pacchetto IP in tanti pacchetti H2N. Se il campo fragmented offset è presente indica il numero di pacchetti H2N in cui è stato suddiviso il nostro pacchetto originale.

**Vari scenari di frammentazione**
- Frammentazione locale: Abbiamo un host che crea un pacchetto grande. Vuole trasportarlo al livello inferiore di trasporto. Arriva al livello IP e deve frammentare il pacchetto in tanti sottopacchetti (dipende dalla dimensione dell'MTU) prima di arrivare al livello H2N.
- Comunicazione di rete: Abbiamo una rete composta da tante reti locali diverse. Ciascuna rete locale può avere un MTU differente. C'è un problema di frammentazione lato router se l'MTU di ingresso è maggiore dell'MTU in uscita (pacchetto di 1.5kb vs mtu di 600byte). Aggiungiamo complessità sul router perchè deve gestire la frammentazione. Chi gestisce la frammentazione è l'host finale. Al giorno d'oggi sia in IPV4 sia in IPV6 h1 invia un pacchetto troppo grosso e il router invece di frammentare il pacchetto manda un flag all'host dicendo che non può frammentarlo, quindi il pacchetto viene rinviato all'host e il pacchetto verrà frammentato localmente.

Path MTU discovery = min(mtu) - il valore minimo di MTU di tutte le reti che attraverseremo.