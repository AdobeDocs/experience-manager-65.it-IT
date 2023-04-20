---
title: Creazione di Adobe Campaign Forms in AEM
description: AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web. Campi specifici possono essere inseriti nei moduli e mappati al database Adobe Campaign.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Creazione di Adobe Campaign Forms in AEM{#creating-adobe-campaign-forms-in-aem}

AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web. Campi specifici possono essere inseriti nei moduli e mappati al database Adobe Campaign.

Puoi gestire nuovi abbonamenti a contatti, annullamenti di abbonamenti e dati del profilo utente, il tutto integrando i loro dati nel database di Adobe Campaign.

Per utilizzare i moduli Adobe Campaign in AEM, è necessario seguire questi passaggi, descritti in questo documento:

1. Rendi disponibile un modello.
1. Creare un modulo.
1. Modificare il contenuto del modulo.

Per impostazione predefinita sono disponibili tre tipi di moduli specifici per Adobe Campaign:

* Salvare un profilo
* Iscriviti a un servizio
* Annulla l’abbonamento a un servizio

Questi moduli definiscono un parametro URL che accetta la chiave primaria crittografata di un profilo Adobe Campaign. In base a questo parametro URL, il modulo aggiorna i dati del profilo Adobe Campaign associato.

Anche se si creano questi moduli in modo indipendente, in un caso d’uso tipico, si genera un collegamento personalizzato a una pagina del modulo all’interno del contenuto della newsletter, in modo che i destinatari possano aprire il collegamento e apportare modifiche ai dati del profilo (per annullare l’iscrizione, iscriversi o aggiornare il profilo).

Il modulo viene aggiornato automaticamente in base all’utente. Vedi [Modifica del contenuto del modulo](#editing-form-content) per ulteriori informazioni.

## Come rendere disponibile un modello {#making-a-template-available}

Prima di poter creare moduli specifici per Adobe Campaign, è necessario rendere disponibili i diversi modelli nell’applicazione AEM.

A questo scopo, consulta la sezione [Documentazione sui modelli](/help/sites-developing/page-templates-static.md#templateavailability).

Innanzitutto, controlla che la connessione tra le istanze di authoring e pubblicazione e Adobe Campaign funzioni. Vedi [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Assicurati che **acMapping** nella pagina **jcr:content** è impostato su **mapRecipient** o **profilo** quando si utilizza rispettivamente Adobe Campaign 6.1.x o Adobe Campaign Standard

### Creazione di un modulo {#creating-a-form}

1. Inizia da siteadmin.
1. Scorri la struttura ad albero per arrivare alla posizione in cui desideri creare il modulo nel sito web scelto.
1. Seleziona **Nuovo** > **Nuova pagina...**.
1. Seleziona o **Profilo Adobe Campaign (AC 6.1)** o **Profilo Adobe Campaign (ACS)** e immetti le proprietà della pagina.

   >[!NOTE]
   >
   >Se il modello non è disponibile, fai riferimento alla [Rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) sezione .

1. Fai clic su **Crea** per creare il modulo.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   È quindi possibile [modificare e configurare il contenuto del modulo](#editing-form-content).

## Modifica del contenuto del modulo {#editing-form-content}

Forms dedicato ad Adobe Campaign dispone di componenti specifici. Questi componenti dispongono di un’opzione che consente di collegare ogni campo del modulo a un campo del database Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedi [Rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Questa sezione descrive solo i collegamenti specifici ad Adobe Campaign. Per ulteriori informazioni su una panoramica più generale dell’utilizzo dei moduli in Adobe Experience Manager, consulta [Componenti in modalità Modifica](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Individuare il modulo da modificare.
1. Nella casella degli strumenti, seleziona **Pagina** > **Proprietà pagina..** quindi vai al **Cloud Services** scheda della finestra a comparsa.
1. Aggiungi il servizio Adobe Campaign facendo clic su **Aggiungi servizio**, quindi seleziona la configurazione che corrisponde alla tua istanza Adobe Campaign nell’elenco a discesa del servizio. Questa configurazione viene eseguita quando si imposta la connessione tra le istanze. Per ulteriori informazioni, consulta [Collegamento AEM ad Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessario, sblocca la configurazione facendo clic sull’icona a forma di lucchetto per poter aggiungere il servizio Adobe Campaign.

1. Accedere ai parametri generali del modulo utilizzando **Modifica** all’inizio del modulo. La **Modulo** consente di selezionare una pagina di ringraziamento a cui verrà reindirizzato l’utente dopo aver convalidato il modulo.

   La **Avanzate** consente di selezionare il tipo di modulo. La **Opzioni post** Il campo ti offre la possibilità di scegliere tra tre tipi di moduli Adobe Campaign:

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: Iscriviti ai servizi**: consente di gestire gli abbonamenti di un destinatario in Adobe Campaign.
   * **Adobe Campaign: Annulla sottoscrizione a servizi**: consente di annullare gli abbonamenti di un destinatario in Adobe Campaign.

   La **Configurazione azione** consente di specificare se si desidera creare o meno il profilo destinatario nel database Adobe Campaign, se non esiste ancora. Per eseguire questa operazione, controlla il **Crea utente se non esistente** opzione .

1. Aggiungi i componenti selezionati trascinandoli dalla casella degli strumenti e rilasciandoli nel modulo. Per ulteriori informazioni sui componenti specifici di Adobe Campaign disponibili, consulta [Componenti Adobe per moduli](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configura i campi aggiunti facendo doppio clic su di essi. La **Adobe Campaign** consente di collegare il campo a un campo nella tabella dei destinatari di Adobe Campaign. Puoi inoltre specificare se il campo fa parte della chiave di riconciliazione che consente di riconoscere i destinatari già presenti nel database di Adobe Campaign.

   >[!CAUTION]
   >
   >La **Nome elemento** deve essere diverso per ogni campo del modulo. Se necessario, cambialo.
   >
   >Ogni modulo deve contenere un **Chiave principale crittografata** per gestire correttamente i destinatari nel database di Adobe Campaign.

1. Attiva la pagina selezionando **Pagina** > **Attiva pagina** nella cassetta degli attrezzi. La pagina viene attivata sul sito. Puoi visualizzarlo accedendo alla tua istanza di pubblicazione AEM. I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.

## Verifica di un modulo {#testing-a-form}

Dopo aver creato un modulo e modificato il contenuto, potrebbe essere necessario verificare manualmente che il modulo funzioni come previsto.

>[!NOTE]
>
>Devi avere un **Chiave principale crittografata** in ciascun modulo. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
>
>Anche se in questa procedura inserisci manualmente il numero EPK, in pratica gli utenti riceveranno un collegamento a questa pagina (per annullare l’iscrizione, iscriversi o aggiornare il profilo) all’interno di una newsletter. In base all’utente, l’EPK si aggiorna automaticamente.
>
>Per creare il collegamento, utilizza la variabile . **Identificatore risorsa principale**(Adobe Campaign Standard) o **Identificatore crittografato** (Adobe Campaign 6.1) (ad esempio, in un **Testo e personalizzazione (Campaign)** component), che effettua un collegamento all’EPK in Adobe Campaign.

A questo scopo, devi ottenere manualmente l’EPK di un profilo Adobe Campaign e aggiungerlo all’URL:

1. Per ottenere la chiave crittografata principale (EPK) di un profilo Adobe Campaign:

   * In Adobe Campaign Standard - Passa a **Profili e pubblico** > **Profili**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore risorsa principale** Campo di una colonna (configurabile facendo clic o toccando) **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In Adobe Campaign 6.11, vai a **Profili e destinazioni** >  **Destinatari**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore crittografato** Campo di una colonna (configurabile facendo clic con il pulsante destro del mouse su una voce e selezionando **Configura elenco...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, apri la pagina del modulo nell’istanza di pubblicazione e aggiungi l’EPK dal passaggio 1 come parametro URL: utilizzare lo stesso nome precedentemente definito nel componente EPK durante la creazione del modulo (ad esempio: `?epk=...`)
1. Ora è possibile utilizzare il modulo per modificare i dati e le iscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e inviato il modulo, è possibile verificare all’interno di Adobe Campaign che i dati appropriati siano stati aggiornati.

I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.
