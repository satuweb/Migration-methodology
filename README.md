# Migration-methodology

Analisi Design System

Prima di procedere con la costruzione di componenti migratori è necessario e opportuno definire un sistema di progettazione (design system).
Il design system è una raccolta di componenti riutilizzabili, guidati da standard chiari, che possono essere assemblati insieme per creare un numero qualsiasi di applicazioni (effetto “Lego”). 
Progettare componenti perché più facili da usare e più chiari da comprendere, permette di creare un'esperienza utente con una struttura e un significato, rende di fatto coerente il progetto e aumenta la qualità complessiva del prodotto. 
L'approccio al design system deve essere di tipo “Maratona” e non “Sprint”. È un processo lungo ed estremamente impegnativo, ma allo stesso tempo snello e prevedibile in quanto dichiarativo, componibile e testabile riducendo i tempi di progettazione e d'ingegneria; è la rappresentazione di un sistema di concetti, non una semplice pagina web.

Benefits e steps

* 		Check dell’attuale progetto: collezionare tutte le parti e i pezzi dell'interfaccia utente attualmente in produzione, comprenderne i problemi e creare una divergenza di soluzioni.

* 		Creare un linguaggio di visual design: individuare da 1 a 3 colori primari che rappresentano il brand, gradienti di colori primari e contrasti; individuare un font per le intestazioni e uno per il corpo; spaziatura e grandezza; sistema di icone;

* 		Creazione della UI / pattern library: questo passaggio del processo esamina i componenti effettivi dell'interfaccia utente. (Step 1)

* 		Documentare cos'è ogni componente e quando ciascuno deve essere utilizzato (documentazione e standard sono molto importanti all’interno del design system, è il design system!)


In un primo momento, per evitare “incoerenza” di design pattern con il design esistente (ormai assimilato dagli utenti), si procede con la definizione e l’introduzione dei livelli meno “visibili” (padding, margin, typography) per poi seguire con quelli più visibili (pulsanti, icone, layout). 
Esempio di refactoring UI: https://twitter.com/i/moments/994601867987619840

In generale, l’intento è quello di costruire un design system a più livelli partendo da un livello canonico - agnostico (html, css e javascript per le micro-interaction) fino ad arrivare ad un livello specifico per il framework in uso (Ad es. React.js). L'idea è quella di progettare una UI agnostica facilmente convertibile in una forma consumabile da qualsiasi framework in uso.

Lista di alcuni casi di studio di design system https://www.invisionapp.com/inside-design/design-systems/

L’esempio di Atlassian dal quale mi lascerò ispirare: https://atlassian.design/ 


Analisi migrazione

sulla base degli argomenti trattati nella riunione del 2 ottobre in merito alla migrazione del CSS verso nuove tecnologie di sviluppo Frontend ho effettuato un’analisi sulle metodologie di migrazione Frontend da architetture monolitiche ad approccio granulare.

Al termine della ricerca è emersa una nuova metodologia di migrazione denominata “Frankenstein Migration”. Tale approccio consiste nell’iniettare componenti “Aliens” (nuovo progetto di refactoring) all’interno del suo “Host” (progetto esistente) mediante l’utilizzo dei web components e dello shadow DOM. 

In questo modo il componente vien iniettato in un DOM privato affinché moduli di stile e funzionalità javascript della pagina ospitante non creino interferenza con il componente stesso e viceversa. 

Il processo della "Frankenstein Migration”, al contrario di un “re-write” dell’intero progetto, prevede la riscrittura dei servizi/micro servizi con un processo graduale al fine di poter utilizzare sin da subito all’interno dell’Host i primi componenti generati. Una volta conclusa la migrazione di tutti i componenti è possibile “spegnere” l’Host e utilizzare esclusivamente l’Alien (che a questo punto diventerà il nuovo Host) mediante l’aggiornamento del DocumentRoot di Apache sulla cartella dell'Alien.

Di seguito il link all’articolo: https://www.smashingmagazine.com/2019/09/frankenstein-migration-framework-agnostic-approach-part-1/

In accordo con Federico si è pensato di intervenire, in modalità alpha test, sulla pagina “System” (admin -> system) la quale presenta due servizi (System e Runtime) e una serie di micro-servizi (clear cache, Reliable host, Device auth,  ecc..)

Links utili: 

https://www.webcomponents.org/
https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM
