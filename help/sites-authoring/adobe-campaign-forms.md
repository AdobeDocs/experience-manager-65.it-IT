---
title: Creare Adobe Campaign Forms in Adobe Experience Manager
description: Adobe Experience Manager consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 1%

---

# Creazione di Adobe Campaign Forms nell’AEM {#creating-adobe-campaign-forms-in-aem}

AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web. Campi specifici possono essere inseriti nei moduli e mappati al database di Adobe Campaign.

Puoi gestire le sottoscrizioni di nuovi contatti, il loro annullamento e i dati del profilo utente, il tutto integrando i relativi dati nel database di Adobe Campaign.

Per utilizzare Adobe Campaign Forms nell’AEM, è necessario seguire questi passaggi, descritti in questo documento:

1. Rendi disponibile un modello.
1. Crea un modulo.
1. Modifica il contenuto del modulo.

Per impostazione predefinita, sono disponibili tre tipi di moduli specifici di Adobe Campaign:

* Salvare un profilo
* Abbonati a un servizio
* Annullare l’abbonamento a un servizio

Questi moduli definiscono un parametro URL che accetta la chiave primaria crittografata di un profilo Adobe Campaign. In base a questo parametro URL, il modulo aggiorna i dati del profilo Adobe Campaign associato.

Anche se questi moduli vengono creati in modo indipendente, in un caso d’uso tipico viene generato un collegamento personalizzato a una pagina di modulo all’interno del contenuto della newsletter, in modo che i destinatari possano aprire il collegamento e apportare modifiche ai dati del loro profilo (sia che si tratti dell’annullamento dell’abbonamento, dell’abbonamento o dell’aggiornamento del profilo).

Il modulo viene aggiornato automaticamente in base all’utente. Per ulteriori informazioni, vedere [Modifica contenuto modulo](#editing-form-content).

## Come rendere disponibile un modello {#making-a-template-available}

Prima di poter creare moduli specifici per Adobe Campaign, è necessario rendere disponibili i diversi modelli nell’applicazione AEM.

A questo scopo, consulta la [documentazione dei modelli](/help/sites-developing/templates.md#template-availability).

## Creazione di un modulo {#creating-a-form}

Adobe Campaign Prima di tutto, verifica che la connessione tra le istanze di authoring e pubblicazione funzioni correttamente. Vedere [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Assicurati che la proprietà **acMapping** nel nodo **jcr:content** della pagina sia impostata su **mapRecipient** o **profile** quando utilizzi rispettivamente Adobe Campaign Classic o Adobe Campaign Standard
>

1. In AEM, in Sites, individua il punto in cui desideri creare una pagina.
1. Crea una pagina e seleziona **Profilo Adobe Campaign Classic** o **Profilo Adobe Campaign Standard**, quindi fai clic su **Avanti**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se il modello desiderato non è disponibile, vedere [Disponibilità modello](/help/sites-developing/templates.md#template-availability).

1. Nel campo **Name**, aggiungi il nome della pagina. Deve essere un nome JCR valido.
1. Nel campo **Titolo** immettere un titolo e fare clic su **Crea**.
1. Apri la pagina e seleziona **Apri proprietà**; in Cloud Service aggiungi la configurazione Adobe Campaign e seleziona il segno di spunta per salvare le modifiche.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Nel componente **Inizio modulo** della pagina selezionare il tipo di modulo: **Sottoscrivi, Annulla sottoscrizione,** o **Salva profilo**. È possibile specificare un solo tipo per modulo. È ora possibile [modificare il contenuto del modulo](#editing-form-content).

## Modifica del contenuto di un modulo {#editing-form-content}

Forms dedicato ad Adobe Campaign dispone di componenti specifici. Questi componenti dispongono di un’opzione che consente di collegare ogni campo del modulo a un campo del database di Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedere [Come rendere disponibile un modello](/help/sites-authoring/adobe-campaign.md).

Questa sezione descrive solo collegamenti specifici ad Adobe Campaign. Per ulteriori informazioni su una panoramica più generale sull&#39;utilizzo dei moduli in Adobe Experience Manager, vedere [Componenti Editmode](/help/sites-authoring/default-components-foundation.md).

1. Seleziona **Apri proprietà** e in Cloud Service aggiungi la configurazione Adobe Campaign e seleziona il segno di spunta per salvare le modifiche.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Nel componente **Inizio modulo** della pagina fare clic sull&#39;icona Configurazione.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Fare clic sulla scheda **Avanzate** e selezionare il tipo di modulo corrispondente - **Sottoscrivi, Annulla sottoscrizione,** o **Salva profilo**, quindi fare clic su **OK.** È possibile avere un solo tipo per modulo.

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: Abbonati ai servizi**: consente di gestire gli abbonamenti di un destinatario in Adobe Campaign.
   * **Adobe Campaign: annulla abbonamento a servizi**: consente di annullare gli abbonamenti di un destinatario in Adobe Campaign.

1. È necessario disporre di un componente **Chiave primaria crittografata** in ogni modulo. Questo componente definisce quale parametro URL viene utilizzato per accettare la chiave primaria crittografata di un profilo Adobe Campaign. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
1. Trascina il componente **Chiave primaria crittografata** nel modulo (ovunque) e fai clic sull&#39;icona **Configurazione**. Nella scheda **Adobe Campaign**, specifica un nome qualsiasi per il parametro URL. Fai clic sul segno di spunta per salvare le modifiche.

   I collegamenti generati a questo modulo devono utilizzare questo parametro URL e assegnargli la chiave primaria crittografata di un profilo Adobe Campaign. La chiave primaria crittografata deve essere correttamente codificata nell&#39;URL (percentuale).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Aggiungere al modulo i componenti necessari, ad esempio un campo di testo, un campo di data, un campo casella di controllo, un campo di opzione e così via. Per ulteriori informazioni su ciascun componente, vedere [Componenti di Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md).
1. Fai clic sull’icona Configurazione per aprire il componente. Ad esempio, nel componente **Campo di testo (Campaign)**, modifica il titolo e il testo.

   Fai clic su **Adobe Campaign** per mappare il campo modulo a una variabile di metadati Adobe Campaign. Quando invii il modulo, il campo mappato viene aggiornato in Adobe Campaign. Nel selettore delle variabili sono disponibili solo i campi con tipi corrispondenti (ad esempio, le variabili stringa per i campi di testo).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >È possibile aggiungere o rimuovere i campi visualizzati nella tabella dei destinatari seguendo le istruzioni disponibili: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Fare clic su **Pagina Publish**. La pagina viene attivata sul sito. Puoi visualizzarlo dalla tua istanza di pubblicazione AEM. È inoltre possibile [testare un modulo](#testing-a-form).

   >[!CAUTION]
   >
   >È necessario fornire autorizzazioni di lettura all’utente anonimo sul servizio cloud per utilizzare i moduli al momento della pubblicazione. Tuttavia, stai attento ai potenziali problemi di sicurezza legati alla fornitura di autorizzazioni di lettura all’utente anonimo e assicurati di attenuarli, ad esempio, configurando il dispatcher.

## Verifica di un modulo {#testing-a-form}

Dopo aver creato un modulo e averne modificato il contenuto, può essere opportuno verificare manualmente il funzionamento previsto.

>[!NOTE]
>
>È necessario disporre di un componente **Chiave primaria crittografata** in ogni modulo. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
>
>Anche se in questa procedura si immette il numero epk manualmente, in pratica, gli utenti riceveranno un collegamento a questa pagina (se annullare l’abbonamento, abbonarsi o aggiornare il profilo) all’interno di una newsletter. In base all’utente, il pk si aggiorna automaticamente.
>
>Per creare il collegamento, si utilizza la variabile **Identificatore risorsa principale**(Adobe Campaign Standard) o **Identificatore crittografato** (Adobe Campaign Classic) (ad esempio, in un componente **Text &amp; Personalization (Campaign)**), che collega all&#39;epk in Adobe Campaign.

A questo scopo, devi ottenere manualmente l’EPK di un profilo Adobe Campaign e quindi aggiungerlo all’URL:

1. Per ottenere la chiave principale crittografata (EPK) di un profilo Adobe Campaign:

   * In Adobe Campaign Standard - Passa a **Profili e tipi di pubblico** > **Profili**, in cui sono elencati i profili esistenti. Accertati che nella tabella sia visualizzato il campo **Identificatore risorsa principale** in una colonna (per configurarlo, tocca o fai clic su **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In Adobe Campaign Classic, vai a **Profili e destinazioni** > **Destinatari**, in cui sono elencati i profili esistenti. Assicurarsi che nella tabella sia visualizzato il campo **Identificatore crittografato** in una colonna (per configurare questo campo, fare clic con il pulsante destro del mouse su una voce e selezionare **Configura elenco...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, aprire la pagina del modulo nell&#39;istanza di pubblicazione e aggiungere l&#39;EPK del passaggio 1 come parametro URL: utilizzare lo stesso nome precedentemente definito nel componente EPK durante la creazione del modulo (ad esempio: `?epk=...`)
1. Il modulo può ora essere utilizzato per modificare i dati e le sottoscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e aver inviato il modulo, puoi verificare in Adobe Campaign che i dati appropriati siano stati aggiornati.

I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.
