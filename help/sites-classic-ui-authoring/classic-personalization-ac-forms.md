---
title: Creazione di moduli di Adobe Campaign in AEM
seo-title: Creating Adobe Campaign Forms in AEM
description: AEM consente di creare e utilizzare i moduli che interagiscono con Adobe Campaign sul tuo sito web. Campi specifici possono essere immessi nei moduli e associati al database Adobe Campaign.
seo-description: AEM lets you create and use forms that interact with Adobe Campaign on your website. Specific fields can be inserted into your forms and mapped to the Adobe Campaign database.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 61%

---

# Creazione di moduli di Adobe Campaign in AEM{#creating-adobe-campaign-forms-in-aem}

AEM consente di creare e utilizzare i moduli che interagiscono con Adobe Campaign sul tuo sito web. Campi specifici possono essere immessi nei moduli e associati al database Adobe Campaign.

Puoi gestire nuove iscrizioni di contatti, annullamenti di iscrizioni e i dati del profilo utente, il tutto integrando i dati nel tuo database di Adobe Campaign.

Per utilizzare i moduli di Adobe Campaign in AEM, è necessario seguire questi passaggi, descritti in questo documento:

1. Rendere disponibile un modello.
1. Creare un modulo.
1. Modificare il contenuto del modulo.

Sono disponibili tre tipi di moduli, specifici per Adobe Campaign, per impostazione predefinita:

* Salvare un profilo
* Iscriversi a un servizio
* Annullare l’iscrizione a un servizio

Questi moduli definiscono un parametro URL che accetta la chiave principale crittografata di un profilo Adobe Campaign. In base a questo parametro URL, il modulo aggiorna i dati del profilo Adobe Campaign associato.

Anche se si creano i moduli in modo indipendente, in un caso di utilizzo tipico, generi un collegamento personalizzato a una pagina del modulo all&#39;interno del contenuto della newsletter, in modo che i destinatari possano accedere al collegamento e modificare i dati del proprio profilo (per iscriversi, annullare l’iscrizione o aggiornare il profilo).

Il modulo si aggiorna automaticamente a seconda dell’utente. Per ulteriori informazioni, consulta [Modifica del contenuto del modulo](#editing-form-content).

## Rendere disponibile un modello {#making-a-template-available}

Prima di poter creare i moduli specifici di Adobe Campaign, è necessario rendere disponibili i diversi modelli nell&#39;applicazione AEM.

A questo scopo, consulta la sezione [Documentazione sui modelli](/help/sites-developing/page-templates-static.md#templateavailability).

Innanzitutto, verifica che la connessione tra le istanze di creazione e pubblicazione e Adobe Campaign funzioni correttamente. Consulta [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifica che la proprietà **acMapping** sul nodo **jcr:content** della pagina sia impostato su **mapRecipient** o **profilo** quando usi rispettivamente Adobe Campaign 6.1.x o Adobe Campaign Standard.

### Creazione di un modulo {#creating-a-form}

1. Inizia da siteadmin.
1. Scorri attraverso la struttura a albero per arrivare al punto in cui puoi creare il modulo nel tuo sito web.
1. Seleziona **Nuovo** > **Nuova pagina...**.
1. Seleziona o **Profilo Adobe Campaign (AC 6.1)** o **Profilo Adobe Campaign (ACS)** e immetti le proprietà della pagina.

   >[!NOTE]
   >
   >Se il modello non è disponibile, fai riferimento alla [Rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) sezione .

1. Fai clic su **Crea** per creare il modulo.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Ora puoi [modificare e configurare il contenuto del tuo modulo](#editing-form-content).

## Modifica del contenuto del modulo {#editing-form-content}

I moduli dedicati ad Adobe Campaign hanno componenti specifici. Questi componenti dispongono di un’opzione per consentire di collegare ciascun campo del modulo a un campo del database di Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedi [Rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Questa sezione contiene solo dettagli sui collegamenti specifici a Adobe Campaign. Per ulteriori informazioni su una panoramica più generale dell’utilizzo dei moduli in Adobe Experience Manager, consulta [Componenti in modalità Modifica](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Spostati sul modulo che desideri modificare.
1. Nella casella degli strumenti, seleziona **Pagina** > **Proprietà pagina..** quindi vai al **Cloud Services** scheda della finestra a comparsa.
1. Aggiungi il servizio Adobe Campaign facendo clic su **Aggiungi servizio**, quindi seleziona la configurazione che corrisponde alla tua istanza Adobe Campaign nell’elenco a discesa del servizio. Questa configurazione viene mantenuta quando viene impostata la connessione tra le tue istanze. Per ulteriori informazioni, consulta [Collegamento AEM ad Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessario, sblocca la configurazione facendo clic sull&#39;icona a forma di lucchetto per poter aggiungere il servizio Adobe Campaign.

1. Accedere ai parametri generali del modulo utilizzando **Modifica** all’inizio del modulo. La **Modulo** consente di selezionare una pagina di ringraziamento a cui verrà reindirizzato l’utente dopo aver convalidato il modulo.

   La **Avanzate** consente di selezionare il tipo di modulo. La **Opzioni post** Il campo ti offre la possibilità di scegliere tra tre tipi di moduli Adobe Campaign:

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: iscrizione a servizi**: consente di gestire le iscrizioni dei destinatari in Adobe Campaign.
   * **Adobe Campaign: Annulla iscrizione a servizi**: consente di annullare le iscrizioni dei destinatari in Adobe Campaign.

   La **Configurazione azione** consente di specificare se si desidera creare o meno il profilo destinatario nel database Adobe Campaign, se non esiste ancora. Per eseguire questa operazione, controlla il **Crea utente se non esistente** opzione .

1. Aggiungi i componenti selezionati trascinandoli dalla casella strumenti e rilasciandoli nel modulo. Per ulteriori informazioni sui componenti specifici per Adobe Campaign disponibili, consulta [Componenti Adobe Form](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configura i campi aggiunti selezionandoli con doppio clic. La **Adobe Campaign** consente di collegare il campo a un campo nella tabella dei destinatari di Adobe Campaign. Puoi anche specificare se il campo fa parte della chiave di riconciliazione che consente di essere riconosciuti ai destinatari già presenti nel database di Adobe Campaign.

   >[!CAUTION]
   >
   >La **Nome elemento** deve essere diverso per ogni campo del modulo. Se necessario, modificalo.
   >
   >Ogni modulo deve contenere un **Chiave principale crittografata** per gestire correttamente i destinatari nel database di Adobe Campaign.

1. Attiva la pagina selezionando **Pagina** > **Attiva pagina** nella cassetta degli attrezzi. La pagina viene attivata sul tuo sito. È possibile visualizzarla accedendo al’&#39;istanza di pubblicazione di AEM. I dati nel database di Adobe Campaign vengono aggiornati quando viene convalidato un modulo.

## Test di un modulo {#testing-a-form}

Dopo aver creato un modulo e modificato il suo contenuto, potresti voler verificare che funzioni come previsto.

>[!NOTE]
>
>Devi avere un **Chiave principale crittografata** in ciascun modulo. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
>
>Anche se in questa procedura si inserisce il numero EPK manualmente, in pratica gli utenti otterrebbero un collegamento a questa pagina (che sia per annullare l’iscrizione, iscriversi o aggiornare il profilo) all&#39;interno di una newsletter. In base all&#39;utente, l’EPK si aggiorna automaticamente.
>
>Per creare il collegamento, utilizza la variabile . **Identificatore risorsa principale**(Adobe Campaign Standard) o **Identificatore crittografato** (Adobe Campaign 6.1) (ad esempio, in un **Testo e personalizzazione (Campaign)** component), che effettua un collegamento all’EPK in Adobe Campaign.

Per eseguire questa operazione, è necessario ottenere manualmente l&#39;EPK da un profilo Adobe Campaign e aggiungerlo all&#39;URL:

1. Per ottenere la chiave crittografata primaria (EPK) di un profilo Adobe Campaign:

   * In Adobe Campaign Standard - Passa a **Profili e pubblico** > **Profili**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore risorsa principale** Campo di una colonna (configurabile facendo clic o toccando) **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In Adobe Campaign 6.11, vai a **Profili e destinazioni** >  **Destinatari**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore crittografato** Campo di una colonna (configurabile facendo clic con il pulsante destro del mouse su una voce e selezionando **Configura elenco...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, apri la pagina del modulo nell’istanza di pubblicazione e aggiungi l’EPK dal passaggio 1 come parametro URL: utilizzare lo stesso nome precedentemente definito nel componente EPK durante la creazione del modulo (ad esempio: `?epk=...`)
1. Ora puoi usare il modulo per modificare i dati e le iscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e inviato il modulo, puoi verificare in Adobe Campaign che siano stati aggiornati i dati relativi.

I dati nel database di Adobe Campaign vengono aggiornati quando viene convalidato un modulo.
