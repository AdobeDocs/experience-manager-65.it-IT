---
title: Creazione di moduli di Adobe Campaign in AEM
seo-title: Creazione di moduli di Adobe Campaign in AEM
description: AEM consente di creare e utilizzare i moduli che interagiscono con Adobe Campaign sul tuo sito web. Campi specifici possono essere immessi nei moduli e associati al database Adobe Campaign.
seo-description: AEM consente di creare e utilizzare i moduli che interagiscono con Adobe Campaign sul tuo sito web. Campi specifici possono essere immessi nei moduli e associati al database Adobe Campaign.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 62%

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

A tale scopo, consultare la [Documentazione sui modelli](/help/sites-developing/page-templates-static.md#templateavailability).

Innanzitutto, verifica che la connessione tra le istanze di creazione e pubblicazione e Adobe Campaign funzioni correttamente. Consulta [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifica che la proprietà **acMapping** sul nodo **jcr:content** della pagina sia impostato su **mapRecipient** o **profilo** quando usi rispettivamente Adobe Campaign 6.1.x o Adobe Campaign Standard.


### Creazione di un modulo {#creating-a-form}

1. Inizia da siteadmin.
1. Scorri attraverso la struttura a albero per arrivare al punto in cui puoi creare il modulo nel tuo sito web.
1. Selezionare **Nuova** > **Nuova pagina...**.
1. Selezionare il modello **profilo Adobe Campaign (AC 6.1)** o **profilo Adobe Campaign (ACS)** e immettere le proprietà della pagina.

   >[!NOTE]
   >
   >Se il modello non è disponibile, fare riferimento alla sezione [Rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

1. Fare clic su **Crea** per creare il modulo.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Ora puoi [modificare e configurare il contenuto del tuo modulo](#editing-form-content).

## Modifica del contenuto del modulo  {#editing-form-content}

I moduli dedicati ad Adobe Campaign hanno componenti specifici. Questi componenti dispongono di un’opzione per consentire di collegare ciascun campo del modulo a un campo del database di Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedere [Come rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Questa sezione contiene solo dettagli sui collegamenti specifici a Adobe Campaign. Per ulteriori informazioni su una panoramica più generale dell&#39;uso dei moduli in Adobe Experience Manager, vedere [Componenti Editmode](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Spostati sul modulo che desideri modificare.
1. Nella casella degli strumenti, selezionare **Pagina** > **Proprietà pagina...** quindi passare alla scheda **Cloud Services** della finestra a comparsa.
1. Aggiungi il servizio Adobe Campaign  facendo clic su **Aggiungi servizio**, quindi selezionando la configurazione che corrisponde all&#39;istanza Adobe Campaign  nell&#39;elenco a discesa del servizio. Questa configurazione viene mantenuta quando viene impostata la connessione tra le tue istanze. Per ulteriori informazioni, vedere [Collegamento AEM a  Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessario, sblocca la configurazione facendo clic sull&#39;icona a forma di lucchetto per poter aggiungere il servizio Adobe Campaign.

1. Accedere ai parametri generali del modulo utilizzando il pulsante **Modifica** disponibile all&#39;inizio del modulo. La scheda **Modulo** consente di selezionare una pagina di ringraziamento alla quale verrà reindirizzato l&#39;utente dopo aver convalidato il modulo.

   Il modulo **Advanced** consente di selezionare il tipo di modulo. Il campo **Opzioni post** consente di scegliere tra tre tipi di moduli Adobe Campaign :

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: iscrizione a servizi**: consente di gestire le iscrizioni dei destinatari in Adobe Campaign.
   * **Adobe Campaign: Annulla iscrizione a servizi**: consente di annullare le iscrizioni dei destinatari in Adobe Campaign.

   Il campo **Configurazione azione** consente di specificare se creare o meno il profilo del destinatario nel database Adobe Campaign , se ancora non esiste. A questo scopo, selezionare l&#39;opzione **Crea utente se non esistente**.

1. Aggiungi i componenti selezionati trascinandoli dalla casella strumenti e rilasciandoli nel modulo. Per ulteriori informazioni sui componenti specifici per Adobe Campaign disponibili, consulta [Componenti Adobe Form](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configura i campi aggiunti selezionandoli con doppio clic. La scheda **Adobe Campaign** consente di collegare il campo a un campo nella  tabella dei destinatari Adobe Campaign. Puoi anche specificare se il campo fa parte della chiave di riconciliazione che consente di essere riconosciuti ai destinatari già presenti nel database di Adobe Campaign.

   >[!CAUTION]
   >
   >Il **Nome elemento** deve essere diverso per ciascun campo modulo. Se necessario, modificalo.
   >
   >Ogni modulo deve contenere un componente **Chiave primaria crittografata** per gestire correttamente i destinatari nel database Adobe Campaign .

1. Attivare la pagina selezionando **Page** > **Activate Page** (Attiva pagina) nella casella degli strumenti. La pagina viene attivata sul tuo sito. È possibile visualizzarla accedendo al’&#39;istanza di pubblicazione di AEM. I dati nel database di Adobe Campaign vengono aggiornati quando viene convalidato un modulo.

## Test di un modulo  {#testing-a-form}

Dopo aver creato un modulo e modificato il suo contenuto, potresti voler verificare che funzioni come previsto.

>[!NOTE]
>
>È necessario disporre di un componente **Chiave primaria crittografata** su ciascun modulo. In Componenti  Adobe Campaign, in modo che solo tali componenti siano visibili.
>
>Anche se in questa procedura si inserisce il numero EPK manualmente, in pratica gli utenti otterrebbero un collegamento a questa pagina (che sia per annullare l’iscrizione, iscriversi o aggiornare il profilo) all&#39;interno di una newsletter. In base all&#39;utente, l’EPK si aggiorna automaticamente.
>
>Per creare tale collegamento, è possibile utilizzare la variabile **Identificatore risorsa principale**( Adobe Campaign Standard) o **Identificatore crittografato** ( Adobe Campaign 6.1) (ad esempio, in un componente **Testo e personalizzazione (Campaign)**), che si collega all&#39;epk in  Adobe Campaign.

Per eseguire questa operazione, è necessario ottenere manualmente l&#39;EPK da un profilo Adobe Campaign e aggiungerlo all&#39;URL:

1. Per ottenere la chiave crittografata primaria (EPK) di un profilo Adobe Campaign:

   * In  Adobe Campaign Standard - Passare a **Profili e pubblico** > **Profili**, in cui sono elencati i profili esistenti. Assicurarsi che la tabella visualizzi il campo **Identificatore risorsa principale** in una colonna (per configurarlo, fare clic o toccare **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In  Adobe Campaign 6.11, andate a **Profili e destinazioni** > **Destinatari**, in cui sono elencati i profili esistenti. Assicurarsi che la tabella visualizzi il campo **Identificatore crittografato** in una colonna (è possibile configurare facendo clic con il pulsante destro del mouse su una voce e selezionando l&#39;elenco **Configura...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, aprite la pagina del modulo nell’istanza di pubblicazione e aggiungete l’EPK dal passaggio 1 come parametro URL: durante la creazione del modulo, usate lo stesso nome definito in precedenza nel componente EPK (ad esempio: `?epk=...`)
1. Ora puoi usare il modulo per modificare i dati e le iscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e inviato il modulo, puoi verificare in Adobe Campaign che siano stati aggiornati i dati relativi.

I dati nel database di Adobe Campaign vengono aggiornati quando viene convalidato un modulo.
