---
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 61%

---
# Linee guida per contribuire alla documentazione di Adobe Experience Manager

## Filosofia della documentazione

Adobe sa che gli utenti di Adobe Experience Manager lavorano in ambienti altamente competitivi per creare esperienze digitali che li distinguano dalla concorrenza. Pertanto, è fondamentale che, quando Adobe offre nuovi strumenti avanzati nell’AEM, questi siano integrati da una documentazione accurata e chiara che consenta al cliente di utilizzare immediatamente il proprio investimento nell’AEM e massimizzare il ROI.

Per la documentazione di AEM, l’obiettivo è renderla disponibile agli utenti della soluzione il prima possibile. Adobe assegna quindi priorità a una documentazione accurata e fruibile, cercando di aggiornarla e migliorarla continuamente.

## Contributi alla documentazione

Al fine di migliorare continuamente la documentazione di AEM, apprezziamo il contributo dell’intera comunità di utenti AEM. I miglioramenti apportati alla documentazione, che derivino da richieste o segnalazioni di problemi, possono essere correzioni, chiarimenti, ampliamenti ed esempi aggiuntivi.

## Standard della documentazione

Mentre Adobe accoglie con favore i contributi alla nostra documentazione, qualsiasi contributo alla documentazione dell’AEM, sotto forma di richiesta o segnalazione di un problema, deve essere conforme ai nostri standard in merito a tali contributi.

I contributi che non soddisfano tali standard possono essere rifiutati.

### Documenta i casi d’uso standard.

La documentazione di AEM riguarda i casi di utilizzo standard. I casi di utilizzo che esulano dall’ambito di installazione e utilizzo standard del prodotto non rientrano nella documentazione di AEM.

### In genere, la documentazione non documenta i bug o le relative soluzioni.

La documentazione di AEM riguarda i casi di utilizzo standard. Per questo motivo, i bug, gli effetti causati dai bug e le soluzioni alternative per i bug di solito non sono documentati.

Fanne eccezione le note sulla versione, in cui possono essere elencati i problemi noti con possibili soluzioni approvate dal team AEM Product Management.

### I contributi alla documentazione non devono essere usati per rispondere a domande tecniche.

È gradita come contributo qualsiasi idea che punti al miglioramento della documentazione di AEM. Tuttavia, commenti, problemi e richieste sono intesi solo come *contributi*. Non hanno l’obiettivo di rispondere a domande su come usare AEM, come implementare un progetto AEM o risolvere problemi tecnici.

Eventuali domande sull’utilizzo di AEM o su errori tecnici possono essere segnalate attraverso il normale processo di assistenza tramite il [portale di assistenza Experience Manager](https://experienceleague.adobe.com/it?support-solution=Experience+Manager&lang=it#support) o discusse nella [community di Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=it&lang=it).

***I contributi alla documentazione di AEM non sostituiscono l’Assistenza clienti di Adobe***. Pertanto, verranno rifiutati tutti i contributi che richiedono risposte a domande correlate al supporto.

### I contributi devono fare riferimento in modo chiaro alle pagine della documentazione interessate.

Se apri una segnalazione per suggerire miglioramenti alla documentazione, devi includere i collegamenti alle pagine interessate. Se si crea un problema utilizzando **Modifica questa pagina** su una pagina della documentazione, il problema viene creato automaticamente con un collegamento alla pagina.

Ciò non si applica alle richieste pull, che per loro natura fanno riferimento alle pagine interessate.

## Linee guida per la documentazione

Chiediamo che qualsiasi contributo alla nostra documentazione segua determinate linee guida di stile.

L’adesione a queste linee guida semplifica la revisione del contributo proposto e ne velocizza quindi l’integrazione nella documentazione.

### Lingua e stile

#### Lingua

* La documentazione di AEM è creata e mantenuta in inglese americano.
* Usa frasi quanto più semplici possibile.
* Usa un linguaggio chiaro e conciso.

Ricorda che i lettori della documentazione dell’AEM sono di tutto il mondo e non ci si può aspettare che siano di madrelingua inglese o che parlino inglese correntemente. Evita i colloquialismi e usa un linguaggio chiaro e semplice.

#### Segui il Manuale di stile di Microsoft®

[Manuale di stile di Microsoft®](https://learn.microsoft.com/en-us/style-guide/welcome/) è una guida di stile per la documentazione disponibile gratuitamente, specifica per la documentazione di software. La documentazione AEM segue questa guida quando possibile.

### Formattazione

| Elemento | Stile |
|---|---|
| Elemento o opzione dell’interfaccia utente | **grassetto** |
| Nome file, percorso, input utente, valori di parametri | `monospaced` |
| Codice, riga di comando | ```Code Block``` |

### Schermate

Le schermate devono essere utilizzate con cautela e solo quando una descrizione testuale è insufficiente.

Non utilizzare marcatori o altre annotazioni nelle schermate (come riquadri rossi, frecce o testo). In questo modo le schermate possono essere riutilizzate o replicate più facilmente nelle versioni localizzate della documentazione.

### Riferimenti a specifiche versioni

È meglio evitare, quando possibile, riferimenti diretti a una versione specifica nel contenuto della documentazione. In tal modo la documentazione sarà più flessibile e potrà essere estesa anche a versioni future.

### Utilizzo di Day, AEM, CQ, CRX

La prima volta che viene citato in un articolo, il prodotto deve sempre essere indicato con il suo nome completo **Adobe Experience Manager**; successivamente può essere usato **AEM**.

Non utilizzare Day, Day Software, CQ e CRX, salvo se inevitabile ad esempio nei nomi delle classi o se si fa riferimento alla storia dell’AEM.