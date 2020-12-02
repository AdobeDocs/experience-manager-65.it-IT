---
title: Gestione della corrispondenza | Gestione dei dati utente
seo-title: Gestione della corrispondenza | Gestione dei dati utente
description: Gestione della corrispondenza | Gestione dei dati utente
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---


# Gestione della corrispondenza | Gestione dei dati utente {#correspondence-management-handling-user-data}

 AEM Forms Correspondence Management consente di creare, gestire e semplificare le corrispondenze dei clienti sicure e personalizzate. Offre agli utenti aziendali un&#39;interfaccia utente intuitiva per creare le corrispondenze utilizzando blocchi di contenuto e elementi multimediali già approvati. Per ulteriori informazioni sulla creazione delle corrispondenze, vedere [Crea corrispondenza](/help/forms/using/create-correspondence.md).

Quando un utente aziendale o un agente salva una corrispondenza come bozza o la invia, viene salvata un&#39;istanza di lettera nell&#39;archivio AEM. L’istanza letter include i dati e i metadati della corrispondenza.

>[!NOTE]
>
>AEM 6.5 Forms, la gestione della corrispondenza non è disponibile. Se state effettuando l’aggiornamento da una versione precedente di AEM Forms , installate il pacchetto di compatibilità ed eseguite la migrazione delle risorse di gestione della corrispondenza per continuare a utilizzarle in AEM Forms 6.5. Per ulteriori informazioni, vedere [Pacchetto di compatibilità](/help/forms/using/compatibility-package.md).

## Archivio dati utente {#data}

La gestione della corrispondenza memorizza i dati per le bozze e le lettere inviate AEM repository solo se l&#39;istanza di pubblicazione è configurata per gestire le istanze di lettere. Per ulteriori informazioni sulla configurazione, vedere [Proprietà di configurazione della gestione della corrispondenza](/help/forms/using/cm-configuration-properties.md).

A seconda della persistenza dell&#39;archivio dati configurata per la distribuzione AEM, le bozze e i dati di corrispondenza inviati vengono memorizzati nelle seguenti posizioni.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo di persistenza</strong></p> </td>
   <td><p><strong>Archivio dati</strong></p> </td>
   <td><p><strong>Dove si trova</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predefiniti</p> </td>
   <td><p>AEM archivio delle istanze di pubblicazione e di creazione specificate nella configurazione di replica inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>AEM repository dell'istanza di creazione dell'elaborazione remota</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

Nel percorso AEM repository specificato sopra:

* `[yyyy]/[mm]/[dd]` è la struttura del nodo in base alla data di creazione dell&#39;istanza della lettera
* `[node-id]` è l’ID assegnato alla cartella contenente la lettera
* `[letter-instance-name]` è il nome specificato al momento del salvataggio o dell&#39;invio di una lettera

Sotto il nodo [letter-instance-name] viene creata la seguente struttura di nodi e i dati per ogni istanza di lettera vengono memorizzati nell&#39;archivio AEM:

| Node | Descrizione |
|---|---|
| `extendedProperties` | Memorizza le proprietà dei metadati dell&#39;istanza della lettera. |
| `dataXML` | Memorizza un file dataXML scaricabile contenente i dati di corrispondenza in formato binario. |
| `processedXDP` | Include i dettagli del modello XDP utilizzato per creare la lettera inviata. Questo nodo viene creato solo per le corrispondenze inviate. |
| `submittedLetter` | Memorizza i dati della lettera inviati in formato binario scaricabile. Questo nodo viene creato solo per le corrispondenze inviate. |

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

È possibile accedere ai dati della corrispondenza bozza e inviata negli archivi dati configurati e, se necessario, eliminarli.

### Accesso ai dati utente {#access-user-data}

La gestione della corrispondenza fornisce API che potete utilizzare per trovare e accedere alle istanze di bozza e lettera inviata. Utilizzando le API, potete trovare e aprire le istanze di lettere utilizzando l&#39;ID istanza lettera o l&#39;utente che ha salvato o inviato la corrispondenza. Per ulteriori informazioni, vedere [API per accedere alle istanze di lettere](/help/forms/using/cm-apis-to-access-letter-instances.md).

In alternativa, è possibile passare all&#39;istanza della lettera AEM repository utilizzando CRX DELite. Per informazioni sui dati archiviati e sulla posizione dell&#39;archivio, vedere [Archivio dati utente e data store](/help/forms/using/correspondence-management-handling-user-data.md#data).

### Elimina dati utente {#delete-user-data}

Per trovare un&#39;istanza della lettera contenente i dati di un utente specifico, è possibile:

* Utilizzare le API di gestione della corrispondenza se il nome dell&#39;istanza della lettera o l&#39;utente che ha salvato la bozza o ha inviato la corrispondenza è noto
* Utilizza AEM ricerca nel repository utilizzando informazioni personali come l&#39;ID e-mail o il nome per trovare il nodo in cui sono memorizzate le informazioni

Per eliminare completamente i dati utente dalle corrispondenze bozza e inviate dai sistemi AEM, è necessario eliminare manualmente il nodo dell&#39;istanza della lettera da tutte le istanze AEM applicabili.
