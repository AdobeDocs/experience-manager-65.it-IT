---
title: Controllo collegamenti
description: Il controllo collegamenti consente di convalidare i collegamenti interni ed esterni e di riscrivere i collegamenti.
translation-type: tm+mt
source-git-commit: 861cd74e1b2fd3d210647d83dee5d9a6fcead22a
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# Controllo collegamenti {#the-link-checker}

Gli autori dei contenuti non devono preoccuparsi di convalidare ogni collegamento che includono nelle pagine dei contenuti.

Il controllo collegamenti viene eseguito automaticamente per assistere gli autori dei contenuti con i loro collegamenti, compresi:

* Convalida dei collegamenti man mano che vengono aggiunti al contenuto
* Visualizzazione di un elenco di tutti i collegamenti esterni nel contenuto
* Esecuzione delle trasformazioni dei collegamenti

Il controllo collegamenti dispone di diverse opzioni di configurazione [quali la definizione interna della convalida, la possibilità di omettere alcuni collegamenti o pattern di collegamento dalla convalida e la riscrittura delle regole di riscrittura dei collegamenti.](#configuring)

Il controllo collegamenti convalida i collegamenti [interni](#internal) e [esterni.](#external)

>[!NOTE]
>
>Dal momento che il controllo collegamenti controlla i collegamenti di ogni pagina di contenuto, il controllo collegamenti può influire sulle prestazioni sui repository di grandi dimensioni. In questi casi, potrebbe essere necessario [configurare la frequenza con cui il controllo collegamenti esegue](#configuring) o [la disattiva.](#disabling)

## Controllo collegamento interno {#internal}

I collegamenti interni sono collegamenti ad altri contenuti presenti nell&#39;archivio AEM. I collegamenti interni possono essere aggiunti utilizzando il selettore percorso dell’editor Rich Text o utilizzando un componente personalizzato. Esempio:

* La pagina `/content/wknd/us/en/adventures/ski-touring.html`
* Contiene un collegamento a `/content/wknd/us/en/adventures/extreme-ironing.html` in un [componente di testo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

I collegamenti interni vengono convalidati non appena l&#39;autore del contenuto aggiunge dei collegamenti interni a una pagina. Se il collegamento diventa non valido:

* Viene rimosso dall’editore. Il testo del collegamento rimane invariato, ma viene rimosso.
* Viene visualizzato come collegamento interrotto nell’interfaccia di authoring.

![Collegamento interno interrotto durante la creazione di una pagina](assets/link-checker-invalid-link-internal.png)

## Controllo collegamento esterno {#external}

I collegamenti esterni sono collegamenti verso contenuti esterni all’archivio AEM. I collegamenti esterni possono essere aggiunti utilizzando l’editor Rich Text o un componente personalizzato. Esempio:

* La pagina `/content/wknd/us/en/adventures/ski-touring.html`
* Contiene un collegamento a `https://bunwarmerthermalunderwear.com` in un [componente di testo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

I collegamenti esterni sono convalidati per la sintassi e per verificarne la disponibilità. Questo controllo viene eseguito in modo asincrono in un interno configurabile. Se il controllo collegamenti trova un collegamento esterno non valido:

* Viene rimosso dall’editore. Il testo del collegamento rimane invariato, ma viene rimosso.
* Viene visualizzato come collegamento interrotto nell’interfaccia di authoring.

![Collegamento interno interrotto durante la creazione di una pagina](assets/link-checker-invalid-link-external.png)

Inoltre, l&#39;interfaccia [Controllo collegamenti esterni](#external-link-checker) fornisce una panoramica di tutti i collegamenti esterni sulle pagine di contenuto.

### Utilizzo del controllo dei collegamenti esterni {#external-link-checker}

Per utilizzare il controllo collegamenti esterni:

1. Utilizzando **Navigazione**, selezionare **Strumenti**, quindi **Siti**.
1. Selezionare **Controllo collegamenti esterni** e viene visualizzato un elenco di tutti i collegamenti esterni.

![](assets/external-link-checker.png)

Vengono visualizzate le informazioni seguenti:

* **Stato**  - Stato di convalida del collegamento
   * **Valido** : il collegamento esterno è raggiungibile dal controllo collegamenti
   * **In sospeso** : il collegamento esterno è stato aggiunto al contenuto del sito, ma non è ancora stato convalidato dal controllo collegamenti
   * **Non valido** : il collegamento esterno non è raggiungibile dal controllo collegamenti.
* **URL**  - Collegamento esterno
* **Referente** : la pagina del contenuto contenente il collegamento esterno
   * Viene popolato solo [se configurato.](#configuring)
* **Ultimo controllo** : l&#39;ultima volta che il controllo collegamenti convalidava il collegamento esterno
   * La frequenza di controllo dei collegamenti [è configurabile.](#configuring)
* **Ultimo stato**  - L&#39;ultimo codice di stato HTML restituito quando il collegamento controllato per l&#39;ultima volta ha selezionato il collegamento esterno
* **Ultima disponibilità** : ora dell’ultima volta che il collegamento è stato disponibile per il controllo collegamenti
* **Ultimo accesso** : ora dell’ultimo accesso al collegamento da parte del controllo collegamenti

È possibile modificare il contenuto della finestra utilizzando i due pulsanti nella parte superiore dell&#39;elenco di collegamenti:

* **Aggiorna** : per aggiornare il contenuto dell&#39;elenco
* **Check** - Per controllare un singolo collegamento esterno selezionato nell&#39;elenco

### Funzionamento del controllo dei collegamenti esterni {#how-it-works}

Per quanto semplice da usare, il controllo dei collegamenti esterni si basa su una serie di servizi e la comprensione del loro funzionamento consente di comprendere come [configurare il controllo dei collegamenti](#configuring) in base alle proprie esigenze.

1. Ogni volta che un autore salva un collegamento a una pagina, viene attivato un gestore eventi.
1. Il gestore eventi legge tutto il contenuto in `/content` e verifica la presenza di collegamenti nuovi o aggiornati e li aggiunge a una cache per il controllo collegamenti.
1. Il **Day CQ Link Checker Service** viene eseguito su una pianificazione regolare per controllare la sintassi valida delle voci presenti nella cache.
1. I collegamenti convalidati dalla sintassi vengono visualizzati nella finestra [Controllo collegamenti esterni](#external-link-checker). Tuttavia, lo stato sarà **In sospeso**.
1. L&#39;attività **Day CQ Link Checker Task** viene eseguita su base regolare per convalidare i collegamenti effettuando una chiamata di GET.
1. L&#39;attività **Day CQ Link Checker Task** aggiorna quindi le voci nella finestra Controllo collegamenti esterni con i risultati delle chiamate di GET.

## Configurazione del controllo collegamenti {#configuring}

Il controllo collegamenti è disponibile automaticamente in AEM. Esistono tuttavia diverse configurazioni OSGi che possono essere modificate per modificarne il comportamento:

* **Servizio**  di archiviazione informazioni controllo collegamenti giorno CQ - Questo servizio definisce la dimensione della cache del controllo collegamenti nella directory archivio.
* **Day CQ Link Checker Service**  - Questo servizio esegue il controllo asincrono della sintassi dei collegamenti esterni. È possibile definire il periodo di controllo e quali tipi di collegamenti vengono ignorati dal controllo tra le altre opzioni.
* **Day CQ Link Checker Task**  - Questo servizio esegue la convalida GET dei collegamenti esterni. Consente definizioni separate di intervalli per controllare i collegamenti cattivi e buoni tra le altre opzioni.
* **Trasformatore**  controllo collegamento CQ Day - Consente di convertire i collegamenti in base a un set di regole definito dall&#39;utente.

Per ulteriori informazioni su come modificare le impostazioni OSGi, vedere il documento [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).

## Disattivazione del controllo collegamenti {#disabling}

Potete scegliere di disabilitare completamente il controllo collegamenti. A questo scopo:

1. Aprite la console OSGi.
1. Modificare il trasformatore **Day CQ Link Checker**
1. Selezionare le opzioni che si desidera disattivare:
   * **Disattiva controllo** - per disabilitare la convalida dei collegamenti
   * **Disattiva riscrittura**  per disabilitare le trasformazioni dei collegamenti

>[!NOTE]
>
>Se si disabilita il controllo dei collegamenti dopo l&#39;avvio della creazione del contenuto, le voci potrebbero comunque essere visualizzate nella [finestra Controllo collegamenti esterni](#external-link-checker), ma non saranno più aggiornate.
