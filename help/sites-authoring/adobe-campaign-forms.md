---
title: Creazione di moduli di Adobe Campaign in AEM
seo-title: Creating Adobe Campaign Forms in AEM
description: AEM consente di creare e utilizzare moduli che interagiscono con Adobe Campaign sul tuo sito web
seo-description: AEM lets you create and use forms that interact with Adobe Campaign on your website
uuid: 61778ea7-c4d7-43ee-905f-f3ecb752aae2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: d53ef3e2-14ca-4444-b563-be67be15c040
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 73%

---

# Creazione di moduli di Adobe Campaign in AEM {#creating-adobe-campaign-forms-in-aem}

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

A questo scopo, consulta la sezione [Documentazione sui modelli](/help/sites-developing/templates.md#template-availability).

## Creazione di un modulo {#creating-a-form}

Innanzitutto, verifica che la connessione tra le istanze di creazione e pubblicazione e Adobe Campaign funzioni correttamente. Consulta [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integrazione con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Verifica che la proprietà **acMapping** sul nodo **jcr:content** della pagina sia impostata su **mapRecipient** o **profilo** quando usi rispettivamente Adobe Campaign Classic o Adobe Campaign Standard.

1. In AEM, in Sites, spostati nella posizione in cui vuoi creare una nuova pagina.
1. Crea una pagina e seleziona **Profilo Adobe Campaign Classic** o **Profilo Adobe Campaign Standard** e fai clic su **Successivo**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se il modello desiderato non è disponibile, vedi [Disponibilità del modello](/help/sites-developing/templates.md#template-availability).

1. Nel campo **Nome**, immetti il nome della pagina. Deve essere un nome JCR valido.
1. Nel campo **Titolo**, inserisci un titolo e fai clic su **Crea**.
1. Apri la pagina e seleziona **Apri proprietà**, in Servizi cloud aggiungi la configurazione Adobe Campaign e fai clic sul segno di spunta per salvare le modifiche.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. Nella pagina, nel componente **Inizio modulo**, seleziona il tipo di modulo, **Sottoscrizione, Cancella sottoscrizione,** o **Salva profilo**. È consentito avere un solo tipo per modulo. Ora puoi [modificare il contenuto del modulo](#editing-form-content).

## Modifica del contenuto del modulo {#editing-form-content}

I moduli dedicati ad Adobe Campaign hanno componenti specifici. Questi componenti dispongono di un’opzione per consentire di collegare ciascun campo del modulo a un campo del database di Adobe Campaign.

>[!NOTE]
>
>Se il modello desiderato non è disponibile, vedi [Rendere disponibile un modello](/help/sites-authoring/adobe-campaign.md).

Questa sezione contiene solo dettagli sui collegamenti specifici a Adobe Campaign. Per ulteriori informazioni su una panoramica più generale dell’utilizzo dei moduli in Adobe Experience Manager, consulta [Componenti in modalità Modifica](/help/sites-authoring/default-components-foundation.md).

1. Seleziona **Apri proprietà**, nei servizi cloud aggiungi la configurazione Adobe Campaign e fai clic sul segno di spunta per salvare le modifiche.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Nella pagina , nella **Inizio modulo** fai clic sull&#39;icona Configurazione .

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Fai clic sul pulsante **Avanzate** e selezionare il tipo di modulo - **Abbonati, Annulla sottoscrizione,** o **Salva profilo** e fai clic su **OK.** È consentito un solo tipo per modulo.

   * **Adobe Campaign: Salva profilo**: consente di creare o aggiornare un destinatario in Adobe Campaign (valore predefinito).
   * **Adobe Campaign: iscrizione a servizi**: consente di gestire le iscrizioni dei destinatari in Adobe Campaign.
   * **Adobe Campaign: Annulla iscrizione a servizi**: consente di annullare le iscrizioni dei destinatari in Adobe Campaign.

1. È necessario disporre di un componente di **Chiave principale crittografata** per ogni modulo. Questo componente definisce quale parametro URL verrà utilizzato per accettare la chiave principale crittografata di un profilo Adobe Campaign. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
1. Trascina il componente **Chiave principale crittografata** al modulo (in un punto qualsiasi), quindi tocca o fai clic sul pulsante **Configurazione** icona. Nella scheda **Adobe Campaign**, specifica un nome per il parametro URL. Tocca o fai clic sul segno di spunta per salvare le modifiche.

   I collegamenti generati a questo modulo devono utilizzare questo parametro URL e assegnargli la chiave principale crittografata di un profilo Adobe Campaign. La chiave principale crittografata deve essere correttamente codificata con l&#39;URL (percentuale).

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Aggiungi i componenti del modulo secondo necessità, ad esempio un campo Testo, un campo Data, un campo Casella di selezione, un campo Opzione e così via. Per ulteriori informazioni su ogni componente vedi [Componenti del modulo Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
1. Fai clic sull&#39;icona Configurazione per aprire il componente. Ad esempio, in **Campo di testo (Campaign)** , modifica il titolo e il testo.

   Fai clic su **Adobe Campaign** per mappare il campo modulo a una variabile di metadati di Adobe Campaign. Quando invii il modulo, il campo mappato viene aggiornato in Adobe Campaign. Nel selezionatore delle variabili sono disponibili solo campi con tipi corrispondenti (ad esempio, le variabili stringa per i campi di testo).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Puoi aggiungere/rimuovere i campi visualizzati nella tabella dei destinatari seguendo le istruzioni riportate di seguito: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Fai clic su **Pubblica pagina**. La pagina viene attivata sul tuo sito. È possibile visualizzarla accedendo al’&#39;istanza di pubblicazione di AEM. Puoi inoltre [verificare il funzionamento di un modulo](#testing-a-form).

   >[!CAUTION]
   >
   >È necessario immettere permessi di lettura per gli utenti anonimi sul servizio cloud per utilizzare i moduli in pubblicazione. Tuttavia, possono esistere potenziali problemi di sicurezza quando si forniscono autorizzazioni di lettura a utenti anonimi, per attenuarli è consigliabile configurare il distributore.

## Test di un modulo {#testing-a-form}

Dopo aver creato un modulo e modificato il suo contenuto, potresti voler verificare che funzioni come previsto.

>[!NOTE]
>
>Devi avere un **Chiave principale crittografata** in ciascun modulo. In Componenti, seleziona Adobe Campaign in modo che siano visibili solo i componenti.
>
>Anche se in questa procedura si inserisce il numero EPK manualmente, in pratica gli utenti otterrebbero un collegamento a questa pagina (che sia per annullare l’iscrizione, iscriversi o aggiornare il profilo) all&#39;interno di una newsletter. In base all&#39;utente, l’EPK si aggiorna automaticamente.
>
>Per creare il collegamento, utilizza la variabile . **Identificatore risorsa principale**(Adobe Campaign Standard) o **Identificatore crittografato** (Adobe Campaign Classic) (ad esempio, in un **Testo e personalizzazione (Campaign)** component), che effettua un collegamento all’EPK in Adobe Campaign.

Per eseguire questa operazione, è necessario ottenere manualmente l&#39;EPK da un profilo Adobe Campaign e aggiungerlo all&#39;URL:

1. Per ottenere la chiave crittografata primaria (EPK) di un profilo Adobe Campaign:

   * In Adobe Campaign Standard - Passa a **Profili e pubblico** > **Profili**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore risorsa principale** Campo di una colonna (configurabile facendo clic o toccando) **Configura elenco**). Copia l’identificatore della risorsa principale del profilo desiderato.
   * In Adobe Campaign Classic, vai a **Profili e destinazioni** >  **Destinatari**, in cui sono elencati i profili esistenti. Assicurati che la tabella visualizzi il **Identificatore crittografato** Campo di una colonna (configurabile facendo clic con il pulsante destro del mouse su una voce e selezionando **Configura elenco...**). Copia l’identificatore crittografato del profilo desiderato.

1. In AEM, apri la pagina del modulo nell’istanza di pubblicazione e aggiungi l’EPK dal passaggio 1 come parametro URL: utilizzare lo stesso nome precedentemente definito nel componente EPK durante la creazione del modulo (ad esempio: `?epk=...`)
1. Ora puoi usare il modulo per modificare i dati e le iscrizioni associati al profilo Adobe Campaign collegato. Dopo aver modificato alcuni campi e inviato il modulo, puoi verificare in Adobe Campaign che siano stati aggiornati i dati relativi.

I dati nel database di Adobe Campaign vengono aggiornati quando viene convalidato un modulo.
