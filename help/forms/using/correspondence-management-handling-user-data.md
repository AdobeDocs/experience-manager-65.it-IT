---
title: Gestione della corrispondenza | Gestione dei dati utente
description: Scopri come gestire la corrispondenza e i dati utente in un ambiente Adobe Experience Manager Forms.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Gestione della corrispondenza | Gestione dei dati utente {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management consente di creare, gestire e snellire la corrispondenza con i clienti in modo sicuro e personalizzato. Offre un’interfaccia utente intuitiva che consente agli utenti aziendali di creare corrispondenze utilizzando blocchi di contenuto ed elementi multimediali preapprovati. Per ulteriori informazioni sulla creazione di corrispondenze, consulta [Crea corrispondenza](/help/forms/using/create-correspondence.md).

Quando un utente aziendale o un agente salva una corrispondenza come bozza o la invia, l’istanza di una lettera viene salvata nel repository dell’AEM. L’istanza della lettera include dati di corrispondenza e metadati.

>[!NOTE]
>
>In AEM 6.5 Forms, la gestione della corrispondenza non è disponibile come strumento preconfigurato. Se esegui l’aggiornamento da una versione precedente di AEM Forms, installa il pacchetto di compatibilità e migra le risorse di gestione della corrispondenza per continuare a utilizzarle in AEM 6.5 Forms. Per ulteriori informazioni, consulta [Pacchetto di compatibilità](/help/forms/using/compatibility-package.md).

## Dati utente e archivi dati {#data}

Gestione della corrispondenza memorizza i dati per le bozze e le lettere inviate nell’archivio AEM solo se l’istanza Publish è configurata per gestire le istanze di lettere. Per ulteriori informazioni sulla configurazione, consulta [Proprietà di configurazione di Gestione corrispondenza](/help/forms/using/cm-configuration-properties.md).

A seconda della persistenza dell’archivio dati configurata per la distribuzione AEM, le bozze e i dati di corrispondenza inviati vengono memorizzati nei seguenti percorsi.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo di persistenza</strong></p> </td>
   <td><p><strong>Archivio dati</strong></p> </td>
   <td><p><strong>Dove si trova</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predefiniti</p> </td>
   <td><p>Archivio AEM dell’istanza di pubblicazione e delle istanze di authoring specificate nella configurazione di replica inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code><br /> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Archivio AEM dell’istanza di authoring di elaborazione remota</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

Nella posizione specificata sopra per l’archivio AEM:

* `[yyyy]/[mm]/[dd]` è la struttura del nodo in base alla data di creazione dell’istanza della lettera
* `[node-id]` è l’ID assegnato alla cartella contenente la lettera
* `[letter-instance-name]` è il nome specificato durante il salvataggio o l&#39;invio di una lettera

Sotto [letter-instance-name] nodo, viene creata la seguente struttura di nodi e i dati per ogni istanza di lettera vengono memorizzati nell’archivio AEM:

| Nodo | Descrizione |
|---|---|
| `extendedProperties` | Memorizza le proprietà dei metadati dell&#39;istanza della lettera. |
| `dataXML` | Memorizza un file dataXML scaricabile contenente i dati di corrispondenza in formato binario. |
| `processedXDP` | Include i dettagli del modello XDP utilizzato per creare la lettera inviata. Questo nodo viene creato solo per le corrispondenze inviate. |
| `submittedLetter` | Memorizza i dati della lettera inviata in formato binario scaricabile. Questo nodo viene creato solo per le corrispondenze inviate. |

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

Puoi accedere ai dati delle bozze e della corrispondenza inviata negli archivi dati configurati e, se necessario, eliminarli.

### Accedere ai dati utente {#access-user-data}

Gestione della corrispondenza fornisce API che è possibile utilizzare per trovare e accedere alle istanze di bozze e lettere inviate. Utilizzando le API, puoi trovare e aprire le istanze di lettere utilizzando l’ID dell’istanza della lettera o l’utente che ha salvato o inviato la corrispondenza. Per ulteriori informazioni, consulta [API per accedere alle istanze delle lettere](/help/forms/using/cm-apis-to-access-letter-instances.md).

In alternativa, puoi passare all’istanza della lettera nell’archivio AEM utilizzando CRXDE Liti. Consulta [Dati utente e archivi dati](/help/forms/using/correspondence-management-handling-user-data.md#data) per informazioni sui dati archiviati e sulla posizione dell&#39;archivio.

### Elimina dati utente {#delete-user-data}

Per trovare un’istanza di lettera contenente i dati di un utente specifico, puoi:

* Utilizza le API di gestione della corrispondenza se è noto il nome dell’istanza della lettera o l’utente che ha salvato la bozza o inviato la corrispondenza
* Utilizza la ricerca nell’archivio AEM utilizzando informazioni personali identificabili come l’ID e-mail o il nome per trovare il nodo in cui sono memorizzate le informazioni

Per eliminare completamente i dati utente dalle bozze e dalle corrispondenze inviate dai sistemi AEM, è necessario eliminare manualmente il nodo dell&#39;istanza della lettera da tutte le istanze AEM applicabili.
