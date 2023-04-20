---
title: Creare Adobe Campaign Forms in Adobe Experience Manager
description: Adobe Experience Manager consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul sito web
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# Creazione di Adobe Campaign Forms in AEM {#creating-adobe-campaign-forms-in-aem}

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

A questo scopo, consulta la sezione [Documentazione sui modelli](/help/sites-developing/templates.md#template-availability).

## Creazione di un modulo {#creating-a-form}

Innanzitutto, controlla che la connessione tra le istanze di authoring e pubblicazione e Adobe Campaign funzioni. Vedi [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Assicurati che **acMapping** nella pagina **jcr:content** è impostato su **mapRecipient** o **profilo** quando si utilizzano rispettivamente Adobe Campaign Classic o Adobe Campaign Standard

1. In AEM, in Sites, individua il punto in cui desideri creare una nuova pagina.
1. Crea una pagina e seleziona **Profilo Adobe Campaign Classic** o **Profilo Adobe Campaign Standard** e fai clic su **Successivo**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se il modello desiderato non è disponibile, vedi [Disponibilità del modello](/help/sites-developing/templates.md#template-availability).

1. In **Nome** aggiungi il nome della pagina. Deve essere un nome JCR valido.
1. In **Titolo** campo , immetti un titolo e fai clic su **Crea**.
1. Apri la pagina e seleziona **Apri proprietà** e in Cloud Services aggiungi la configurazione Adobe Campaign e seleziona il segno di spunta per salvare le modifiche.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Nella pagina , nella **Inizio modulo** , seleziona il tipo di modulo - **Abbonati, Annulla sottoscrizione,** o **Salva profilo**. È disponibile un solo tipo per modulo. Ora puoi [modificare il contenuto del modulo](#editing-form-content).

## Modifica del contenuto del modulo {#editing-form-content}

Forms dedicato ad Adobe Campaign dispone di componenti specifici. Questi componenti dispongono di un’opzione che consente di collegare ogni campo del modulo a un campo del database Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedi [Rendere disponibile un modello](/help/sites-authoring/adobe-campaign.md).

Questa sezione descrive solo i collegamenti specifici ad Adobe Campaign. Per ulteriori informazioni su una panoramica più generale dell’utilizzo dei moduli in Adobe Experience Manager, consulta [Componenti in modalità Modifica](/help/sites-authoring/default-components-foundation.md).

1. Seleziona **Apri proprietà** e in Cloud Services aggiungi la configurazione Adobe Campaign e seleziona il segno di spunta per salvare le modifiche.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Nella pagina , nella **Inizio modulo** fai clic sull&#39;icona Configurazione .

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Fai clic sul pulsante **Avanzate** e selezionare il tipo di modulo - **Abbonati, Annulla sottoscrizione,** o **Salva profilo** e fai clic su **OK.** È disponibile un solo tipo per modulo.

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: Iscriviti ai servizi**: consente di gestire gli abbonamenti di un destinatario in Adobe Campaign.
   * **Adobe Campaign: Annulla sottoscrizione a servizi**: consente di annullare gli abbonamenti di un destinatario in Adobe Campaign.

1. Devi avere un **Chiave principale crittografata** in ciascun modulo. Questo componente definisce quale parametro URL verrà utilizzato per accettare la chiave primaria crittografata di un profilo Adobe Campaign. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
1. Trascina il componente **Chiave principale crittografata** al modulo (in un punto qualsiasi), quindi tocca o fai clic sul pulsante **Configurazione** icona. In **Adobe Campaign** , specifica un nome per il parametro URL. Tocca o fai clic sul segno di spunta per salvare le modifiche.

   I collegamenti generati a questo modulo devono utilizzare questo parametro URL e assegnargli la chiave primaria crittografata di un profilo Adobe Campaign. La chiave primaria crittografata deve essere correttamente codificata in URL (percentuale).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Aggiungi i componenti necessari al modulo, ad esempio un campo di testo, un campo data, un campo casella di controllo, un campo opzione e così via. Vedi [Componenti per moduli di Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) per ulteriori informazioni su ciascun componente.
1. Fai clic sull’icona Configurazione per aprire il componente. Ad esempio, in **Campo di testo (Campaign)** , modifica il titolo e il testo.

   Fai clic su **Adobe Campaign** mappare il campo modulo a una variabile di metadati Adobe Campaign. Quando si invia il modulo, il campo mappato viene aggiornato in Adobe Campaign. Nel selettore delle variabili sono disponibili solo i campi con tipi corrispondenti (ad esempio, le variabili stringa per i campi di testo).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Puoi aggiungere/rimuovere i campi visualizzati nella tabella dei destinatari seguendo le istruzioni riportate di seguito: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Fai clic su **Pubblica pagina**. La pagina viene attivata sul sito. Puoi visualizzarlo accedendo alla tua istanza di pubblicazione AEM. È inoltre possibile [verifica di un modulo](#testing-a-form).

   >[!CAUTION]
   >
   >È necessario fornire autorizzazioni di lettura all’utente anonimo sul servizio cloud per utilizzare i moduli al momento della pubblicazione. Tuttavia, tieni presente i potenziali problemi di sicurezza relativi alla fornitura di autorizzazioni di lettura all’utente anonimo e assicurati di attenuarli, ad esempio, configurando il dispatcher.

## Verifica di un modulo {#testing-a-form}

Dopo aver creato un modulo e modificato il contenuto, potrebbe essere necessario verificare manualmente che il modulo funzioni come previsto.

>[!NOTE]
>
>Devi avere un **Chiave principale crittografata** in ciascun modulo. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
>
>Anche se in questa procedura inserisci manualmente il numero EPK, in pratica gli utenti riceveranno un collegamento a questa pagina (per annullare l’iscrizione, iscriversi o aggiornare il profilo) all’interno di una newsletter. In base all’utente, l’EPK si aggiorna automaticamente.
>
>Per creare il collegamento, utilizza la variabile . **Identificatore risorsa principale**(Adobe Campaign Standard) o **Identificatore crittografato** (Adobe Campaign Classic) (ad esempio, in un **Testo e personalizzazione (Campaign)** component), che effettua un collegamento all’EPK in Adobe Campaign.

A questo scopo, devi ottenere manualmente l’EPK di un profilo Adobe Campaign e aggiungerlo all’URL:

1. Per ottenere la chiave crittografata principale (EPK) di un profilo Adobe Campaign:

   * In Adobe Campaign Standard - Passa a **Profili e pubblico** > **Profili**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore risorsa principale** Campo di una colonna (configurabile facendo clic o toccando) **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In Adobe Campaign Classic, vai a **Profili e destinazioni** >  **Destinatari**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore crittografato** Campo di una colonna (configurabile facendo clic con il pulsante destro del mouse su una voce e selezionando **Configura elenco...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, apri la pagina del modulo nell’istanza di pubblicazione e aggiungi l’EPK dal passaggio 1 come parametro URL: utilizzare lo stesso nome precedentemente definito nel componente EPK durante la creazione del modulo (ad esempio: `?epk=...`)
1. Ora è possibile utilizzare il modulo per modificare i dati e le iscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e inviato il modulo, è possibile verificare all’interno di Adobe Campaign che i dati appropriati siano stati aggiornati.

I dati nel database di Adobe Campaign vengono aggiornati dopo la convalida di un modulo.
