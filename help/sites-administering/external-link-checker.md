---
title: Verifica collegamenti
description: Il Link Checker aiuta a convalidare i collegamenti interni ed esterni e consente la riscrittura dei collegamenti.
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: 0b9de3261d8747f3e7107962b6aea1dbdf9d6773
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Verifica collegamenti {#the-link-checker}

Gli autori dei contenuti non devono preoccuparsi di convalidare ogni collegamento incluso nelle pagine dei contenuti.

Il Link Checker viene eseguito automaticamente per aiutare gli autori di contenuti con i loro collegamenti, tra cui:

* Convalida dei collegamenti durante l’aggiunta al contenuto
* Visualizzazione di un elenco di tutti i collegamenti esterni nel contenuto
* Esecuzione delle trasformazioni dei collegamenti

Il Link Checker ha un certo numero di [opzioni di configurazione](#configuring) ad esempio la definizione della convalida interna, che consente di omettere dalla convalida determinati collegamenti o pattern di collegamento e la riscrittura delle regole di riscrittura dei collegamenti.

Il Link Checker convalida entrambi [collegamenti interni](#internal) e [collegamenti esterni.](#external)

>[!NOTE]
>
>Poiché il Link Checker controlla i collegamenti di ogni pagina di contenuto, il Link Checker può influire sulle prestazioni su archivi di grandi dimensioni. In questi casi, potrebbe essere necessario [configurare la frequenza di esecuzione del Link Checker](#configuring) o [disattivalo.](#disabling)

## Controllo interno dei collegamenti {#internal}

I collegamenti interni sono collegamenti ad altri contenuti nell’archivio AEM. I collegamenti interni possono essere aggiunti utilizzando il selettore di percorsi nell’Editor Rich Text o utilizzando un componente personalizzato. Esempio:

* La tua pagina `/content/wknd/us/en/adventures/ski-touring.html`
* Contiene un collegamento a `/content/wknd/us/en/adventures/extreme-ironing.html` in [Componente testo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

I collegamenti interni vengono convalidati non appena l’autore del contenuto aggiunge un collegamento interno a una pagina. Se il collegamento diventa non valido:

* Viene rimosso dall’editore. Il testo del collegamento rimane, ma il collegamento stesso viene rimosso.
* Viene visualizzato come un collegamento interrotto nell’interfaccia di authoring.

![Collegamento interno interrotto durante la creazione di una pagina](assets/link-checker-invalid-link-internal.png)

## Controllo dei collegamenti esterni {#external}

I collegamenti esterni sono collegamenti a contenuti esterni all’archivio AEM. I collegamenti esterni possono essere aggiunti utilizzando l’editor Rich Text o un componente personalizzato. Esempio:

* La tua pagina `/content/wknd/us/en/adventures/ski-touring.html`
* Contiene un collegamento a `https://bunwarmerthermalunderwear.com` in [Componente testo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

I collegamenti esterni vengono convalidati per la sintassi e controllandone la disponibilità. Questo controllo viene eseguito in modo asincrono in un interno configurabile. Se il Link Checker trova un collegamento esterno non valido:

* Viene rimosso dall’editore. Il testo del collegamento rimane, ma il collegamento stesso viene rimosso.
* Viene visualizzato come un collegamento interrotto nell’interfaccia di authoring.

![Collegamento interno interrotto durante la creazione di una pagina](assets/link-checker-invalid-link-external.png)

Inoltre, il [Verifica collegamenti esterni](#external-link-checker) L’interfaccia fornisce una panoramica di tutti i collegamenti esterni nelle pagine di contenuto.

### Utilizzo del controllo dei collegamenti esterni {#external-link-checker}

Per utilizzare il Verifica collegamenti esterni:

1. Utilizzo **Navigazione**, seleziona **Strumenti**, quindi **Sites**.
1. Seleziona **Verifica collegamenti esterni** e viene visualizzato un elenco di tutti i collegamenti esterni.

![Finestra Verifica collegamenti esterni](assets/external-link-checker.png)

Vengono visualizzate le seguenti informazioni:

* **Stato** - Lo stato di convalida del collegamento può essere uno dei seguenti:
   * **Valido** - Il link esterno è raggiungibile dal Link Checker
   * **In sospeso** - Il collegamento esterno è stato aggiunto al contenuto del sito, ma non è ancora stato convalidato dal Link Checker
   * **Non valido** - Il link esterno non è raggiungibile dal Link Checker
* **URL** - Collegamento esterno
* **Referrer** - La pagina del contenuto contenente il collegamento esterno
   * Viene compilato solo [se configurato.](#configuring)
* **Ultimo controllo** - L’ultima volta che Link Checker ha convalidato il collegamento esterno
   * Con quale frequenza vengono controllati i collegamenti [è configurabile.](#configuring)
* **Ultimo stato** - L’ultimo codice di stato di HTML restituito quando Link Checked ha selezionato l’ultimo collegamento esterno
* **Ultimo disponibile** - Ora dell’ultima disponibilità del collegamento per il Link Checker
* **Ultimo accesso** - ora dell’ultimo accesso alla pagina con il collegamento esterno nell’interfaccia di authoring

È possibile manipolare il contenuto della finestra utilizzando i due pulsanti nella parte superiore dell’elenco dei collegamenti:

* **Aggiorna** - Aggiornare il contenuto dell&#39;elenco
* **Controlla** - Controllare un singolo collegamento esterno selezionato nell&#39;elenco

### Funzionamento del Verifica collegamenti esterni {#how-it-works}

Sebbene facile da usare, il Verifica collegamenti esterni si basa su una serie di servizi e la comprensione del loro funzionamento ti aiuta a capire come [configurare il Link Checker](#configuring) per soddisfare le tue esigenze.

1. Ogni volta che un autore di contenuti salva un collegamento a una pagina, viene attivato un gestore di eventi.
1. Il gestore eventi attraversa tutto il contenuto in `/content` controlla i collegamenti nuovi o aggiornati e li aggiunge a una cache per Link Checker.
1. La **Servizio Day CQ Link Checker** quindi viene eseguito su una pianificazione regolare per controllare le voci nella cache per una sintassi valida.
1. I collegamenti convalidati dalla sintassi vengono quindi visualizzati nella [Verifica collegamenti esterni](#external-link-checker) finestra. Tuttavia, saranno in una **In sospeso** stato.
1. La **Attività Day CQ Link Checker** quindi viene eseguito regolarmente per convalidare i collegamenti effettuando una chiamata GET.
1. La **Attività Day CQ Link Checker** quindi aggiorna le voci nella finestra Verifica collegamenti esterni con i risultati delle chiamate di GET.

## Configurazione del Link Checker {#configuring}

Il Link Checker è disponibile automaticamente in AEM. Tuttavia esistono diverse configurazioni OSGi che possono essere modificate per modificarne il comportamento:

* **Day CQ Link Checker Info Storage Service** - Questo servizio definisce le dimensioni della cache Link Checker nel repository.
* **Servizio Day CQ Link Checker** - Questo servizio esegue il controllo asincrono della sintassi dei collegamenti esterni. È possibile definire il periodo di controllo e quali tipi di collegamenti vengono ignorati dal controllo, tra le altre opzioni.
* **Attività Day CQ Link Checker** - Questo servizio esegue la convalida GET dei collegamenti esterni. Consente definizioni separate di intervalli per controllare i collegamenti errati e buoni tra le altre opzioni.
* **Trasformatore Day CQ Link Checker** - Consente la conversione di collegamenti in base a un set di regole definito dall’utente.

Vedere il documento [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md) per ulteriori informazioni su come modificare le impostazioni OSGi.

## Disabilitazione del Link Checker {#disabling}

Puoi scegliere di disattivare completamente il Link Checker. Per eseguire questa operazione:

1. Apri la console OSGi.
1. Modifica le **Trasformatore Day CQ Link Checker**
1. Seleziona le opzioni che desideri disattivare:
   * **Disattiva controllo** - disabilitare la convalida dei collegamenti
   * **Disattiva riscrittura** - per disabilitare le trasformazioni dei collegamenti

>[!NOTE]
>
>Se disattivi il controllo dei collegamenti dopo aver iniziato a creare il contenuto, potresti comunque visualizzare le voci nel [Finestra Verifica collegamenti esterni](#external-link-checker), ma non verranno più aggiornati.
