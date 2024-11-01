ifconfig <nome rete> <ip>/24 - aggiunge indirzzo ip è un comando temporaneo! unap volta spenta la macchina questi ip si cancellano
ifconfig <nome rete> fa vedere dati quali l'indirizzo mac 
ip 
ping - serve per testare l'indirizzo ip se è utilizzato o meno

tcpdump -eni (informazioni in dettaglio su ethernet, interface) <nome interfaccia> - copia del traffico sulle interfacce di rete. Non richiede configurare una rete su un certo server per usare tcpdump, possiamo non configurarla e va uguale. Il comando ifconfig <rete> up attiva l'interfaccia, non la configura, in questo modo possiamo usare tcpdump

FSTP = protocollo eseguito dagli switch per introdurre percorsi ridondanti

per collegare un host con lo switch bisogna usare il cavo dritto

Il file di configurazione da modificare si trova nel path /etc/network/interfaces
Per configurare un interfaccia si usa la parola chiave iface seguito dal nome dell'interfaccia (eth0), dal tipo di configurazione (inet, protocollo ipv4) e da un altra keyword che ci permette di (static/dhcp) inserire il nostro indirizzo ip manualmente. Tutto ciò che vien scritto sotto la linea iface eth0 inet static verrà applicato all'avvio alla rete eth0. Non esistono direttive globali! Quindi se vogliamo applicare una certa direttiva più volte dobbiamo metterla sotto ad ogni interfaccia.

address <indirizzo> = assegna l'indirizzo ip <indirizzo>. Ciò che abbiamo fatto è equivalente alla riga di codice ifconfig <nome rete> <ip>/24.

Se non mettiamo nient'altro fino a questo punto non l'abiliterà al boot. Per attivare una certa configurazione al boot dobbiamo inserire la direttiva auto <nome rete>. Con più interfacce possiamo inserire più direttive nella stessa linea.

ifup attiva un interfaccia. È indipendente da auto, che invece si occupa di avviarlo al boot.
ifdown disattiva una configurazione per una certa interfaccia di rete. Ovviamente deve esistere l'interfaccia indicata.

Se viene chiesta la configurazione a runtime bisogna eseguire il comando ifconfig <rete> per vedere l'indirizzo ip utilizzato attualmente.

ip neigh flush cancella l'hash table

tmux è un software che consente di eseguire tanti terminali all'interno di un terminale singolo.
ctrl+b = modalità comando. la prossima roba eseguita verrà presa come un comando da tmux
" -> split orizzontale
% -> split verticale
c -> nuovo tab
muoversi fra split -> freccie direzionali in modalità comandi
muoversi fra tab -> 0-9
ctrl+d -> uscire da terminale

arping è un software che serve a testare una comunicazione. Cerca di fare un ping usando il protocollo ARP per vedere se l'indirizzo esiste. Funziona soltanto con reti locali. -i serve per forzare l'interfaccia di rete -0 per pingare con l'indirizzo 0.0.0.0.
arping -0i <rete> <ip>

brctl è il comando utilizzato per creare un bridge. brtcl addbr br0 crea il bridge br0
Per aggiungere un interfaccia uso il comando brctl addif <nome bridge> <nome interfaccia>. Il bridge bisogna accenderlo!!! Altrimenti non potrà comunicare con gli altri host. brctl quindi configura il bridge, non lo abilita. Un bridge di base inoltra soltanto pacchetti, non ha indirizzi ip. L'interfaccia virtuale ha una vita propria, bisogna accenderla.

Per configurare un bridge al boot possiamo modificare /etc/network/interfaces e aggiungere: 

auto br0

iface br0 inet static
	bridge_ports <rete1> <reteN>
	address 0.0.0.0

Indirizzo ip 0.0.0.0 = non assegnare un indirizzo ip. Dipende dalla versione del kernel ci vuole come non ci vuole. Assegnazione dummy. Posso ovviamente assegnarli un indirizzo.

Uno dei comandi per vedere le impostazioni di routing è route con il -n per darmi informazioni a basso livello. Per ottenere l'indirizzo di rete a partire dalla netmask bisogna fare l'and tra tutti i bit dell'indirizzo di rete. Se ho l'indiirzzo gateaway un indirizzo ip dummy allora vuol dire che possiamo usare il protocollo H2N. Il primo pacchetto inviato è l'arp request perchè l'host cerca di trovare la regola da utilizzare per trovare quell'indirizzo.

Sysctl è un comando utilizzato per modificare parametri del kernel. È temporaneo, per modificarlo permanentemente usiamo nano /etc/systcl.conf. Il comando -p riconfigura il kernel senza dover riavviare il pc.

