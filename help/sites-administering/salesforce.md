---
title: Integrare con Salesforce
description: Scopri come integrare Adobe Experience Manager (AEM) con Salesforce.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 4%

---


# Integrare con Salesforce {#integrating-with-salesforce}

L’integrazione di Salesforce con Adobe Experience Manager (AEM) fornisce funzionalità di gestione dei lead e utilizza le funzionalità esistenti fornite da Salesforce. Puoi configurare AEM per pubblicare i lead in Salesforce e creare componenti che accedono ai dati direttamente da Salesforce.

L’integrazione bidirezionale ed estensibile tra AEM e Salesforce consente di:

* Organizzazioni che utilizzano e modificano completamente i dati per migliorare l’esperienza del cliente.
* Coinvolgimento dalle attività di marketing alle attività di vendita.
* Organizzazioni per la trasmissione e la ricezione automatica di dati da un datastore Salesforce.

Questo documento descrive quanto segue:

* come configurare Salesforce Cloud Services (configurare AEM per l’integrazione con Salesforce).
* come utilizzare le informazioni sui contatti/lead di Salesforce in ClientContext e per Personalization.
* come utilizzare il modello di flusso di lavoro di Salesforce per pubblicare gli utenti AEM come lead in Salesforce.
* come creare un componente che mostra i dati di Salesforce.

## Configurazione di AEM per l’integrazione con Salesforce {#configuring-aem-to-integrate-with-salesforce}

Per configurare AEM per l’integrazione con Salesforce, devi prima configurare un’applicazione di accesso remoto in Salesforce. Quindi configurare Salesforce Cloud Service in modo che punti a questa applicazione di accesso remoto.

>[!NOTE]
>
>Puoi creare un account sviluppatore gratuito in Salesforce.

Per configurare AEM per l’integrazione con Salesforce:

>[!CAUTION]
>
>Installare il pacchetto di integrazione [Salesforce Force API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=2&package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) prima di continuare con la procedura. Per ulteriori dettagli su come utilizzare i pacchetti, vedere la pagina [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md#package-share).

1. In AEM, passa a **Cloud Services**. In Servizi di terze parti, fare clic su **Configura ora** in **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Crea una configurazione, ad esempio **sviluppatore**.

   >[!NOTE]
   >
   >La nuova configurazione reindirizza a una nuova pagina: **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. Si tratta esattamente dello stesso valore che è necessario specificare nell&#39;URL di richiamata durante la creazione dell&#39;applicazione di accesso remoto in Salesforce. Questi valori devono corrispondere.

1. Accedi al tuo account Salesforce (oppure, se non ne hai uno, creane uno all&#39;indirizzo [https://developer.salesforce.com](https://developer.salesforce.com).)
1. In Salesforce, passa a **Crea** > **App** per accedere a **App collegate** (nelle versioni precedenti di Salesforce, il flusso di lavoro era **Distribuisci** > **Accesso remoto**).
1. Fai clic su **Nuovo** per connettere AEM a Salesforce.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Immetti **Nome app connessa**, **Nome API** e **E-mail contatto**. Selezionare la casella di controllo **Abilita impostazioni OAuth**, immettere l&#39;**URL richiamata** e aggiungere un ambito OAuth (ad esempio, accesso completo). L&#39;URL di callback è simile al seguente: `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   Modifica il nome del server/numero di porta e il nome della pagina in modo che corrispondano alla configurazione.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Fai clic su **Salva** per salvare la configurazione di Salesforce. Salesforce crea una **chiave consumer** e un **segreto consumer** necessari per la configurazione di AEM.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Attendere alcuni minuti (fino a 15 minuti) per l&#39;attivazione dell&#39;applicazione di accesso remoto in Salesforce.

1. In AEM, passa a **Cloud Services** e passa alla configurazione di Salesforce creata in precedenza, ad esempio **sviluppatore**. Fai clic su **Modifica** e immetti la chiave cliente e il segreto cliente da salesforce.com.

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | Url di accesso | Questo è l’endpoint di autorizzazione di Salesforce. Il suo valore è precompilato e serve la maggior parte dei casi. |
   |---|---|
   | Chiave cliente | Immettere il valore ottenuto dalla pagina Registrazione applicazione di accesso remoto in salesforce.com |
   | Segreto cliente | Immettere il valore ottenuto dalla pagina Registrazione applicazione di accesso remoto in salesforce.com |

1. Fare clic su **Connetti a Salesforce** per connettersi. Salesforce richiede di consentire alla configurazione di connettersi a Salesforce.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   In AEM, viene visualizzata una finestra di dialogo di conferma che informa che la connessione è avvenuta correttamente.

1. Passa alla pagina principale del sito Web e fai clic su **Proprietà pagina**. Selezionare quindi **Servizi cloud**, aggiungere **Salesforce** e selezionare la configurazione corretta, ad esempio **sviluppatore**.

   ![chlimage_1-75](assets/chlimage_1-75.png)

   Ora puoi utilizzare il modello di flusso di lavoro per pubblicare i lead in Salesforce e creare componenti che accedono ai dati da Salesforce.

## Esportazione di utenti AEM come lead di Salesforce {#exporting-aem-users-as-salesforce-leads}

Se desideri esportare un utente di AEM come lead di Salesforce, configura il flusso di lavoro per pubblicare i lead in Salesforce.

Per esportare gli utenti di AEM come lead di Salesforce:

1. Passare al flusso di lavoro di Salesforce in `http://localhost:4502/workflow` facendo clic con il pulsante destro del mouse sul flusso di lavoro **Salesforce.com Export** e scegliendo **Start**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Seleziona l&#39;utente AEM che desideri creare come lead come **Payload** per questo flusso di lavoro (home > utenti). Accertati di selezionare il nodo del profilo dell&#39;utente in quanto contiene informazioni come **givenName** e **familyName**, mappate ai campi **FirstName** e **LastName** del lead Salesforce.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Prima di avviare questo flusso di lavoro, è necessario disporre di alcuni campi obbligatori per un nodo lead in AEM prima di poter pubblicare il flusso di lavoro in Salesforce. Si tratta di **givenName**, **familyName**, **company** e **email**. Per visualizzare un elenco completo dei mapping tra l&#39;utente di AEM e il lead di Salesforce, vedere [Configurazione mapping tra l&#39;utente di AEM e il lead di Salesforce.](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. Fai clic su **OK**. Le informazioni utente vengono esportate in salesforce.com. Puoi verificarlo all’indirizzo salesforce.com.

   >[!NOTE]
   >
   >I registri degli errori mostrano se un lead è importato. Per ulteriori informazioni, consulta il registro degli errori.

### Configurazione del flusso di lavoro di esportazione Salesforce.com {#configuring-the-salesforce-com-export-workflow}

Se necessario, configura il flusso di lavoro di esportazione Salesforce.com in modo che corrisponda alla configurazione Salesforce.com corretta o che apporti altre modifiche.

Per configurare il flusso di lavoro di esportazione Salesforce.com:

1. Passa a `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. Apri il passaggio di esportazione Salesforce.com, seleziona la scheda **Argomenti**, seleziona la configurazione corretta e fai clic su **OK**. Inoltre, se si desidera che il flusso di lavoro ricrei un lead eliminato in Salesforce, selezionare la casella di controllo.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Fai clic su **Salva** per salvare le modifiche.

   ![chlimage_1-79](assets/chlimage_1-79.png)

### Mappatura della configurazione tra l’utente di AEM e il lead di Salesforce {#mapping-configuration-between-aem-user-and-salesforce-lead}

Per visualizzare o modificare la configurazione di mappatura corrente tra un utente di AEM e un lead di Salesforce, aprire Gestione configurazione: `https://<hostname>:<port>/system/console/configMgr` e cercare **Configurazione mappatura lead di Salesforce**.

1. Aprire Configuration Manager facendo clic su **Console Web** o accedendo direttamente a `https://<hostname>:<port>/system/console/configMgr.`
1. Cerca **Configurazione mappatura lead Salesforce**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Modifica le mappature in base alle esigenze. La mappatura predefinita segue il pattern **aemUserAttribute=sfLeadAttribute**. Fai clic su **Salva** per salvare le modifiche.

## Configurazione dell’archivio ClientContext di Salesforce {#configuring-salesforce-client-context-store}

L’archivio contestuale del client Salesforce mostra informazioni aggiuntive sull’utente attualmente connesso rispetto a quelle già disponibili in AEM. Estrae queste informazioni aggiuntive da Salesforce a seconda della connessione dell’utente con Salesforce.

A questo scopo, configura quanto segue:

1. Collega un utente AEM con un Salesforce ID tramite il componente Salesforce Connect.
1. Aggiungi i dati del profilo di Salesforce nella pagina di contesto del client in modo da poter configurare le proprietà da visualizzare.
1. (Facoltativo) Crea un segmento che utilizza i dati dell’archivio ClientContext di Salesforce.

### Collegamento di un utente AEM a un Salesforce ID {#linking-an-aem-user-with-a-salesforce-id}

Mappa un utente AEM con un Salesforce ID in modo da poterlo caricare nel contesto client. In uno scenario reale, il collegamento si basa sui dati utente noti con convalida. Per scopi dimostrativi, in questa procedura si utilizza il componente **Salesforce Connect**.

1. Passa a un sito Web in AEM, accedi e trascina il componente **Salesforce Connect** dalla barra laterale.

   >[!NOTE]
   >
   >Se il componente **Salesforce Connect** non è disponibile, passare alla visualizzazione **Progettazione** e selezionarlo per renderlo disponibile nella visualizzazione **Modifica**.

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   Quando trascini il componente nella pagina, viene visualizzato **Link to Salesforce=Off**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >Questo componente è solo a scopo dimostrativo. Per scenari reali, ci sarebbe un altro processo per collegare/abbinare gli utenti con i lead.

1. Dopo aver trascinato il componente sulla pagina, aprilo per configurarlo. Selezionare la configurazione, il tipo di contatto e il lead o il contatto Salesforce, quindi fare clic su **OK**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM collega l’utente con il contatto o il lead di Salesforce.

   ![chlimage_1-83](assets/chlimage_1-83.png)

### Aggiunta di dati Salesforce a ClientContext {#adding-salesforce-data-to-client-context}

Puoi caricare i dati utente da Salesforce in ClientContext da utilizzare per la personalizzazione:

1. Aprire il contesto client che si desidera estendere spostandosi, ad esempio, `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. Trascina il componente **Dati profilo Salesforce** nel contesto client.

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. Apri il componente facendo doppio clic su di esso. Selezionare **Aggiungi elemento** e selezionare una proprietà dall&#39;elenco a discesa. Aggiungi tutte le proprietà desiderate e seleziona **OK**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Ora le proprietà specifiche di Salesforce di Salesforce vengono visualizzate nel contesto client.

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Creazione di un segmento utilizzando i dati dall’archivio ClientContext di Salesforce {#building-a-segment-using-data-from-salesforce-client-context-store}

Puoi creare un segmento che utilizza i dati dell’archivio ClientContext di Salesforce. Per effettuare questo collegamento:

1. Passa alla segmentazione in AEM andando su **Strumenti** > **Segmentazione** oppure andando su [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. Crea o aggiorna un segmento per includere i dati da Salesforce. Per ulteriori informazioni, vedere [Segmentazione](/help/sites-administering/campaign-segmentation.md).

## Ricerca di lead {#searching-leads}

AEM viene fornito con un componente di ricerca di esempio che cerca i lead in Salesforce in base ai criteri specificati. Questo componente mostra come utilizzare l’API REST di Salesforce per cercare oggetti Salesforce. Per attivare una chiamata a salesforce.com, collega una pagina a una configurazione di Salesforce.

>[!NOTE]
>
>Questo è un componente di esempio che mostra come utilizzare l’API REST di Salesforce per eseguire query sugli oggetti Salesforce. Utilizzalo come esempio per creare componenti più complessi in base alle tue esigenze.

Per utilizzare questo componente:

1. Passa alla pagina in cui desideri utilizzare questa configurazione. Apri le proprietà della pagina e seleziona **Servizi cloud.** Fai clic su **Aggiungi servizi**, seleziona **Salesforce** e la configurazione appropriata, quindi fai clic su **OK**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Trascina il componente Salesforce Search nella pagina (se è stato abilitato). Per attivarla, passare alla modalità Progettazione e aggiungerla all&#39;area appropriata).

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. Aprire il componente Ricerca e specificare i parametri di ricerca, quindi fare clic su **OK.**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. In AEM vengono visualizzati i lead specificati nel componente di ricerca che corrispondono ai criteri specificati.

   ![chlimage_1-87](assets/chlimage_1-87.png)
