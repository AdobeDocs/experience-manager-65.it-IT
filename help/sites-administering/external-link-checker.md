---
title: Verifica collegamenti
description: Verifica collegamenti consente di convalidare sia i collegamenti interni che quelli esterni e di riscriverli.
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: 0b9de3261d8747f3e7107962b6aea1dbdf9d6773
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Verifica collegamenti {#the-link-checker}

Gli autori dei contenuti non devono preoccuparsi di convalidare ogni collegamento incluso nelle pagine dei contenuti.

Il Link Checker viene eseguito automaticamente per aiutare gli autori di contenuti con i loro collegamenti, tra cui:

* Convalida dei collegamenti quando vengono aggiunti al contenuto
* Visualizzazione di un elenco di tutti i collegamenti esterni nel contenuto
* Esecuzione delle trasformazioni dei collegamenti

Il Link Checker include [opzioni di configurazione](#configuring) ad esempio la definizione della convalida interna, che consente di omettere dalla convalida alcuni collegamenti o modelli di collegamento e la riscrittura delle regole di riscrittura dei collegamenti.

Verifica collegamenti convalida entrambi [collegamenti interni](#internal) e [collegamenti esterni.](#external)

>[!NOTE]
>
>Poiché il Link Checker controlla i collegamenti di ogni pagina di contenuto, può influire sulle prestazioni di archivi di grandi dimensioni. In questi casi, potrebbe essere necessario [configurare la frequenza di esecuzione di Verifica collegamenti](#configuring) o [disattivala.](#disabling)

## Verifica dei collegamenti interni {#internal}

I collegamenti interni sono collegamenti ad altri contenuti nel tuo archivio AEM. È possibile aggiungere collegamenti interni utilizzando il selettore di percorsi dell’editor Rich Text o utilizzando un componente personalizzato. Ad esempio:

* La tua pagina `/content/wknd/us/en/adventures/ski-touring.html`
* Contiene un collegamento a `/content/wknd/us/en/adventures/extreme-ironing.html` in un [Componente Testo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

I collegamenti interni vengono convalidati non appena l’autore di contenuto aggiunge un collegamento interno a una pagina. Se il collegamento non è più valido:

* Viene rimosso dall’editore. Il testo del collegamento rimane, ma il collegamento stesso viene rimosso.
* Viene visualizzato come collegamento interrotto nell’interfaccia di authoring.

![Collegamento interno interrotto durante la creazione di una pagina](assets/link-checker-invalid-link-internal.png)

## Verifica collegamenti esterni {#external}

I collegamenti esterni sono collegamenti a contenuti esterni all’archivio AEM. È possibile aggiungere collegamenti esterni utilizzando l’editor Rich Text o un componente personalizzato. Ad esempio:

* La tua pagina `/content/wknd/us/en/adventures/ski-touring.html`
* Contiene un collegamento a `https://bunwarmerthermalunderwear.com` in un [Componente Testo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

I collegamenti esterni vengono convalidati per la sintassi e verificandone la disponibilità. Questo controllo viene eseguito in modo asincrono in un ambiente interno configurabile. Se Verifica collegamenti rileva un collegamento esterno non valido:

* Viene rimosso dall’editore. Il testo del collegamento rimane, ma il collegamento stesso viene rimosso.
* Viene visualizzato come collegamento interrotto nell’interfaccia di authoring.

![Collegamento interno interrotto durante la creazione di una pagina](assets/link-checker-invalid-link-external.png)

Inoltre, la [Verifica collegamenti esterni](#external-link-checker) L&#39;interfaccia di fornisce una panoramica di tutti i collegamenti esterni presenti nelle pagine dei contenuti.

### Utilizzo di Verifica collegamenti esterni {#external-link-checker}

Per utilizzare Verifica collegamenti esterni:

1. Utilizzo di **Navigazione**, seleziona **Strumenti**, quindi **Sites**.
1. Seleziona **Verifica collegamenti esterni** e viene visualizzato un elenco di tutti i collegamenti esterni.

![Finestra Verifica collegamenti esterni](assets/external-link-checker.png)

Vengono visualizzate le seguenti informazioni:

* **Stato** - lo stato di convalida del collegamento, che può essere uno dei seguenti:
   * **Valido** - Il collegamento esterno è raggiungibile tramite Verifica collegamenti
   * **In sospeso** - Il collegamento esterno è stato aggiunto al contenuto del sito, ma non è ancora stato convalidato da Verifica collegamenti
   * **Non valido** - Il Link esterno non è raggiungibile tramite Verifica collegamenti
* **URL** - Il collegamento esterno
* **Referrer** - La pagina di contenuto che contiene il collegamento esterno
   * Questo è popolato solo [se configurato.](#configuring)
* **Ultimo controllo** - L’ultima volta che il Link Checker ha convalidato il collegamento esterno
   * Frequenza di controllo dei collegamenti [è configurabile.](#configuring)
* **Ultimo stato** - L’ultimo codice di stato del HTML restituito quando il collegamento Controllato per ultimo ha controllato il collegamento esterno
* **Ultimo disponibile** - Ora dall&#39;ultima volta che il collegamento è stato disponibile per Verifica collegamenti
* **Ultimo accesso** - ora dell’ultimo accesso alla pagina con il collegamento esterno nell’interfaccia di authoring

Puoi modificare il contenuto della finestra utilizzando i due pulsanti nella parte superiore dell’elenco dei collegamenti:

* **Aggiorna** - Per aggiornare il contenuto dell&#39;elenco
* **Verifica** - Per selezionare un singolo collegamento esterno selezionato nell&#39;elenco

### Funzionamento di Verifica collegamenti esterni {#how-it-works}

Sebbene sia facile da usare, Verifica collegamenti esterni si basa su una serie di servizi e comprendere come funzionano consente di comprendere come [configurare Verifica collegamenti](#configuring) per soddisfare le tue esigenze.

1. Ogni volta che un autore di contenuti salva un collegamento a una pagina, viene attivato un gestore eventi.
1. Il gestore eventi analizza tutto il contenuto in `/content` e verifica la presenza di collegamenti nuovi o aggiornati e li aggiunge a una cache per il Link Checker.
1. Il **Servizio Day CQ Link Checker** viene quindi eseguito con una pianificazione regolare per verificare la validità della sintassi delle voci nella cache.
1. I collegamenti convalidati dalla sintassi vengono quindi visualizzati nel [Verifica collegamenti esterni](#external-link-checker) finestra. Tuttavia, si troveranno in un **In sospeso** stato.
1. Il **Attività Day CQ Link Checker** viene quindi eseguito regolarmente per convalidare i collegamenti effettuando una chiamata GET.
1. Il **Attività Day CQ Link Checker** aggiorna quindi le voci nella finestra Verifica collegamenti esterni con i risultati delle chiamate di GET.

## Configurazione di Verifica collegamenti {#configuring}

Il Link Checker è disponibile automaticamente come strumento pronto all’uso in AEM. Tuttavia, esistono diverse configurazioni OSGi che possono essere modificate per modificarne il comportamento:

* **Day CQ Link Checker Info Servizio di archiviazione** - Questo servizio definisce le dimensioni della cache di Verifica collegamenti nell’archivio.
* **Servizio Day CQ Link Checker** : questo servizio esegue il controllo asincrono della sintassi dei collegamenti esterni. È possibile definire il periodo di controllo e quali tipi di collegamenti vengono ignorati dallo strumento di controllo, tra le altre opzioni.
* **Attività Day CQ Link Checker** - Questo servizio esegue la convalida GET dei collegamenti esterni. Consente definizioni separate degli intervalli per verificare collegamenti errati e validi tra le altre opzioni.
* **Day CQ Link Checker Transformer** : consente di convertire i collegamenti in base a un set di regole definito dall’utente.

Consulta il documento [Impostazioni configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md) per ulteriori dettagli su come modificare le impostazioni OSGi.

## Disattivazione di Verifica collegamenti {#disabling}

Puoi scegliere di disabilitare completamente Verifica collegamenti. Per eseguire questa operazione:

1. Apri la console OSGi.
1. Modifica il **Day CQ Link Checker Transformer**
1. Selezionare le opzioni che si desidera disattivare:
   * **Disattiva controllo** - per disattivare la convalida dei collegamenti
   * **Disattiva riscrittura** - per disattivare le trasformazioni dei collegamenti

>[!NOTE]
>
>Se disattivi il controllo dei collegamenti dopo aver iniziato a creare i contenuti, è possibile che vengano ancora visualizzate le voci in [Finestra Verifica collegamenti esterni](#external-link-checker), ma non verranno più aggiornati.
