---
title: Creazione di Adobe Campaign Forms nell’AEM
description: AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web. Campi specifici possono essere inseriti nei moduli e mappati al database di Adobe Campaign.
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

# Creazione di Adobe Campaign Forms nell’AEM{#creating-adobe-campaign-forms-in-aem}

AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web. Campi specifici possono essere inseriti nei moduli e mappati al database di Adobe Campaign.

Puoi gestire le sottoscrizioni di nuovi contatti, il loro annullamento e i dati del profilo utente, il tutto integrando i relativi dati nel database di Adobe Campaign.

Per utilizzare Adobe Campaign Forms nell’AEM, è necessario seguire questi passaggi, descritti in questo documento:

1. Rendi disponibile un modello.
1. Creare un modulo.
1. Modifica il contenuto del modulo.

Per impostazione predefinita, sono disponibili tre tipi di moduli specifici di Adobe Campaign:

* Salvare un profilo
* Abbonati a un servizio
* Annullare l’abbonamento a un servizio

Questi moduli definiscono un parametro URL che accetta la chiave primaria crittografata di un profilo Adobe Campaign. In base a questo parametro URL, il modulo aggiorna i dati del profilo Adobe Campaign associato.

Anche se questi moduli vengono creati in modo indipendente, in un caso d’uso tipico viene generato un collegamento personalizzato a una pagina di modulo all’interno del contenuto della newsletter, in modo che i destinatari possano aprire il collegamento e apportare modifiche ai dati del loro profilo (sia che si tratti dell’annullamento dell’abbonamento, dell’abbonamento o dell’aggiornamento del profilo).

Il modulo viene aggiornato automaticamente in base all’utente. Consulta [Modifica del contenuto di un modulo](#editing-form-content) per ulteriori informazioni.

## Come rendere disponibile un modello {#making-a-template-available}

Prima di poter creare moduli specifici per Adobe Campaign, è necessario rendere disponibili i diversi modelli nell’applicazione AEM.

Per eseguire questa operazione, vedere [Documentazione sui modelli](/help/sites-developing/page-templates-static.md#templateavailability).

Adobe Campaign Prima di tutto, verifica che la connessione tra le istanze di authoring e pubblicazione funzioni correttamente. Consulta [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Assicurati che le **acMapping** proprietà nel file della pagina **jcr:content** nodo impostato su **mapRecipient** o **profilo** quando si utilizza rispettivamente Adobe Campaign 6.1.x o Adobe Campaign Standard

### Creazione di un modulo {#creating-a-form}

1. Inizia in siteadmin.
1. Scorrere la struttura ad albero per arrivare al punto in cui si desidera creare il modulo nel sito Web scelto.
1. Seleziona **Nuovo** > **Nuova pagina...**.
1. Seleziona una **Profilo Adobe Campaign (AC 6.1)** o **Profilo Adobe Campaign (ACS)** e immettere le proprietà della pagina.

   >[!NOTE]
   >
   >Se il modello non è disponibile, consulta [Come rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) sezione.

1. Clic **Crea** per creare il modulo.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   Potrai quindi [modificare e configurare il contenuto del modulo](#editing-form-content).

## Modifica del contenuto di un modulo {#editing-form-content}

Forms dedicato ad Adobe Campaign dispone di componenti specifici. Questi componenti dispongono di un’opzione che consente di collegare ogni campo del modulo a un campo del database di Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedi [Come rendere disponibile un modello](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Questa sezione descrive solo collegamenti specifici ad Adobe Campaign. Per ulteriori informazioni su una panoramica più generale dell’utilizzo dei moduli in Adobe Experience Manager, consulta [Componenti modalità di modifica](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Passare al modulo da modificare.
1. Nella casella degli strumenti, seleziona **Pagina** > **Proprietà pagina...** quindi vai al **Cloud Services** della finestra popup.
1. Aggiungi il servizio Adobe Campaign facendo clic su **Aggiungi servizio** e quindi selezionando la configurazione che corrisponde all’istanza di Adobe Campaign nell’elenco a discesa del servizio. Questa configurazione viene eseguita durante la configurazione della connessione tra le istanze. Per ulteriori informazioni, consulta [Collegamento dell’AEM ad Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Se necessario, sblocca la configurazione facendo clic sull’icona del lucchetto per poter aggiungere il servizio Adobe Campaign.

1. Accedere ai parametri generali della maschera utilizzando **Modifica** all&#39;inizio del modulo. Il **Modulo** Questa scheda ti consente di selezionare una pagina di ringraziamento alla quale l’utente verrà reindirizzato dopo aver convalidato il modulo.

   Il **Avanzate** modulo consente di selezionare il tipo di modulo. Il **Opzioni post** Questo campo consente di scegliere tra tre tipi di Adobe Campaign forms:

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: abbonati ai servizi**: consente di gestire gli abbonamenti di un destinatario in Adobe Campaign.
   * **Adobe Campaign: Annulla iscrizione a servizi**: consente di annullare gli abbonamenti di un destinatario in Adobe Campaign.

   Il **Configurazione azione** Questo campo consente di specificare se si desidera o meno creare il profilo del destinatario nel database di Adobe Campaign, se non esiste ancora. A questo scopo, seleziona la **Crea utente se non esistente** opzione.

1. Aggiungere i componenti selezionati trascinandoli dalla casella degli strumenti e rilasciandoli nel modulo. Per ulteriori informazioni sui componenti specifici di Adobe Campaign disponibili, consulta [Adobe componenti modulo](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configura i campi aggiunti facendo doppio clic su di essi. Il **Adobe Campaign** scheda ti consente di collegare il campo a un campo nella tabella dei destinatari di Adobe Campaign. Puoi anche specificare se il campo fa parte della chiave di riconciliazione, che consente di riconoscere i destinatari già presenti nel database di Adobe Campaign.

   >[!CAUTION]
   >
   >Il **Nome elemento** deve essere diverso per ogni campo modulo. Se necessario, modificala.
   >
   >Ogni modulo deve contenere **Chiave principale crittografata** per gestire correttamente i destinatari nel database di Adobe Campaign.

1. Attiva la pagina selezionando **Pagina** > **Attiva pagina** nella casella degli strumenti. La pagina viene attivata sul sito. Puoi visualizzarlo dalla tua istanza di pubblicazione AEM. I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.

## Verifica di un modulo {#testing-a-form}

Dopo aver creato un modulo e averne modificato il contenuto, può essere opportuno verificare manualmente il funzionamento previsto.

>[!NOTE]
>
>Devi avere un **Chiave principale crittografata** in ogni modulo. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
>
>Anche se in questa procedura si immette il numero epk manualmente, in pratica, gli utenti riceveranno un collegamento a questa pagina (se annullare l’abbonamento, abbonarsi o aggiornare il profilo) all’interno di una newsletter. In base all’utente, il pk si aggiorna automaticamente.
>
>Per creare tale collegamento, utilizza la variabile **Identificatore risorsa principale**(Adobe Campaign Standard) oppure **Identificatore crittografato** (Adobe Campaign 6.1) (ad esempio, in un’ **Testo e personalizzazione (Campaign)** ), che si collega al codice epk in Adobe Campaign.

A questo scopo, devi ottenere manualmente l’EPK di un profilo Adobe Campaign e quindi aggiungerlo all’URL:

1. Per ottenere la chiave principale crittografata (EPK) di un profilo Adobe Campaign:

   * In Adobe Campaign Standard: passa a **Profili e tipi di pubblico** > **Profili**, che elenca i profili esistenti. Accertati che nella tabella sia visualizzato **Identificatore risorsa principale** in una colonna (può essere configurato facendo clic o toccando **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In Adobe Campaign 6.11, vai a **Profili e destinazioni** >  **Destinatari**, che elenca i profili esistenti. Accertati che nella tabella sia visualizzato **Identificatore crittografato** in una colonna (può essere configurato facendo clic con il pulsante destro del mouse su una voce e selezionando **Configura elenco...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, apri la pagina del modulo nell’istanza di pubblicazione e aggiungi l’EPK del passaggio 1 come parametro URL: utilizza lo stesso nome precedentemente definito nel componente EPK durante la creazione del modulo (ad esempio: `?epk=...`)
1. Il modulo può ora essere utilizzato per modificare i dati e le sottoscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e aver inviato il modulo, puoi verificare in Adobe Campaign che i dati appropriati siano stati aggiornati.

I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.
