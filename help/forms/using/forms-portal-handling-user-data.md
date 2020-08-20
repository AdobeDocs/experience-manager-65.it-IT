---
title: Forms Portal | Gestione dei dati utente
seo-title: Forms Portal | Gestione dei dati utente
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# Forms Portal | Gestione dei dati utente {#forms-portal-handling-user-data}

[!DNL AEM Forms] Portal fornisce componenti che è possibile utilizzare per elencare moduli adattivi, moduli HTML5 e altre risorse Forms sulla [!DNL AEM Sites] pagina. Inoltre, è possibile configurarlo per visualizzare le bozze e i moduli adattivi inviati e i moduli HTML5 per un utente connesso. Per ulteriori informazioni sul portale dei moduli, vedere [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md).

Quando un utente connesso salva un modulo adattivo come bozza o lo invia, viene visualizzato nelle schede Bozze e Invii del portale dei moduli. I dati per le bozze o i moduli inviati vengono memorizzati nell&#39;archivio dati configurato per AEM distribuzione. Le bozze e gli invii di utenti anonimi non vengono visualizzati nella pagina del portale dei moduli; tuttavia, i dati vengono memorizzati nell&#39;archivio dati configurato. Per ulteriori informazioni, consultate [Configurazione dei servizi di archiviazione per bozze e invii](/help/forms/using/configuring-draft-submission-storage.md).

## Archivio dati utente e data {#user-data-and-data-stores}

Il portale Forms memorizza i dati per i moduli bozza e inviati nei seguenti scenari:

* L&#39;azione di invio configurata nel modulo adattivo è Azione **di invio** Forms Portal.
* Per le azioni di invio diverse da **Forms Portal Submit Action**, l&#39;opzione **[!UICONTROL Memorizza dati nel portale]** dei moduli è abilitata nelle proprietà **[!UICONTROL Invia]** del contenitore di moduli adattivi.

Per ogni bozza e modulo inviato per utenti anonimi e connessi, il portale dei moduli memorizza i dati seguenti:

* Metadati del modulo quali il nome del modulo, il percorso del modulo, l&#39;ID bozza o di invio, il percorso degli allegati e l&#39;ID dei dati utente
* Allegato modulo come byte di dati
* Dati modulo come byte di dati

A seconda della persistenza dell&#39;archivio dati configurato, le bozze e i dati dei moduli inviati vengono memorizzati nelle seguenti posizioni.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo di persistenza</strong></p> </td>
   <td><p><strong>Archivio dati</strong></p> </td>
   <td><p><strong>Dove si trova</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predefiniti</p> </td>
   <td><p>AEM archivio delle istanze di creazione e pubblicazione</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>AEM archivio dell'autore e delle istanze AEM remote</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Database</p> </td>
   <td><p>AEM archivio dell'istanza di creazione e delle tabelle di database</p> </td>
   <td>Tabelle di database <code>data</code>, <code>metadata</code>e <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

È possibile accedere ai dati delle bozze e dei moduli inviati per gli utenti registrati e anonimi negli archivi dati configurati, nonché, se necessario, eliminarli.

### Istanze AEM {#aem-instances}

Tutte le bozze e i dati dei moduli inviati nelle istanze AEM (autore, pubblicazione o remoto) per gli utenti connessi e anonimi sono memorizzati nel `/content/forms/fp/` nodo dell&#39;archivio AEM applicabile. Ogni volta che un utente connesso o anonimo salva una bozza o invia un modulo, una `draft ID` o `submission ID`, una `user data ID`, e un collegamento casuale `ID` per ciascun allegato (se applicabile) viene generato, associato alla relativa bozza o invio.

#### Accesso ai dati utente {#access-user-data}

Quando un utente connesso salva una bozza o invia un modulo, viene creato un nodo figlio con il relativo ID utente. Ad esempio, le bozze e i dati di invio per Sarah Rose il cui ID utente è `srose` memorizzato nel `/content/forms/fp/srose/` nodo AEM repository. All&#39;interno del nodo ID utente, i dati sono organizzati in una struttura gerarchica.

Nella tabella seguente è illustrato come i dati per tutte le bozze `srose` vengono memorizzati AEM repository.

>[!NOTE]
>
>Una struttura esatta come `drafts` viene replicata per i moduli inviati `srose` sotto il `/content/forms/fp/srose/submit/` nodo.
>
>Tutte le bozze e gli invii degli `anonymous` utenti sono memorizzati sotto il `/content/forms/fp/anonymous/` nodo, che organizza le bozze e gli invii per tutti gli utenti anonimi sotto i `draft` nodi e `submit` .

| Node | Descrizione |
|---|---|
| `/content/forms/fp/srose/drafts` | Dati nodo contenitore per tutte le bozze dell&#39;utente |
| `/content/forms/fp/srose/drafts/attachments/` | Organizza tutti gli allegati per l&#39;utente in base all&#39;ID bozza |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contiene un allegato per l&#39;ID selezionato in formato binario |
| `/content/forms/fp/srose/drafts/metadata/` | Organizza i metadati del modulo per l&#39;utente in base all&#39;ID bozza |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contiene i metadati del modulo per l&#39;ID bozza selezionato |
| `/content/forms/fp/srose/drafts/data/` | Organizza i dati dei moduli per l&#39;utente in base all&#39;ID dei dati utente |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contiene i dati del modulo per l&#39;ID dati utente selezionato in formato binario |

#### Eliminare i dati utente {#delete-user-data}

Per eliminare completamente i dati utente da bozze e invii per un utente connesso AEM sistemi, è necessario eliminare completamente il `user ID` nodo di un utente specifico dal nodo di creazione. È necessario eliminare manualmente i dati da tutte le istanze AEM applicabili.

Le bozze e i dati di invio per tutti gli utenti anonimi sono memorizzati all&#39;interno dei nodi comuni `drafts` e `submit` sotto `/content/forms/fp/anonymous`. Non esiste un metodo per trovare i dati per un utente anonimo specifico, a meno che non siano note alcune informazioni identificabili. In questo caso, è possibile cercare le informazioni che identificano l&#39;utente anonimo in AEM repository ed eliminare manualmente il nodo che lo contiene da tutte le istanze AEM applicabili per rimuovere i dati dal sistema AEM. Tuttavia, per eliminare i dati per tutti gli utenti anonimi, è possibile eliminare il `anonymous` nodo per rimuovere le bozze e i dati di invio per tutti gli utenti anonimi.

### Database {#database}

Se AEM è configurato per memorizzare i dati in un database, i dati di bozza e invio del portale dei moduli vengono memorizzati nelle seguenti tabelle di database per gli utenti anonimi e connessi:

* data
* metadata
* metadata aggiuntivi

#### Accesso ai dati utente {#access-user-data-1}

Per accedere alle bozze e ai dati di invio di utenti registrati e anonimi nelle tabelle del database, eseguire il seguente comando del database. Nella query, sostituire `logged-in user` con l&#39;ID utente di cui si desidera accedere ai dati o con `anonymous` per gli utenti anonimi.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Eliminare i dati utente {#delete-user-data-1}

Per eliminare le bozze e i dati di invio per un utente connesso dalle tabelle del database, eseguire il seguente comando del database. Nella query, sostituire `logged-in user` con l’ID utente i cui dati si desidera eliminare o con `anonymous` per gli utenti anonimi. Per eliminare dal database i dati per un utente anonimo specifico, è necessario reperirli utilizzando alcune informazioni identificabili ed eliminarli dalle tabelle del database contenenti le informazioni.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

