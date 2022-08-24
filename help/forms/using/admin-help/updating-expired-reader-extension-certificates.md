---
title: Aggiornamento dei certificati del servizio di estensione del Reader scaduti
description: Reader documenti estesi non funzionanti, aggiornamento certificati
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---

# Aggiornamento dei certificati del servizio di estensione del Reader scaduti {#Updating-expired-Reader-Extension-service-certificates}

I clienti Adobe Experience Manager Forms (AEM Forms) con licenze Adobe Managed Services o Enterprise Base locale possono utilizzare il servizio di estensione del Reader. Il servizio consente a un’organizzazione di condividere facilmente i documenti PDF interattivi estendendo le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio aggiunge diritti di utilizzo a un documento di PDF e attiva le funzioni solitamente non disponibili quando un documento di PDF viene aperto tramite Adobe Acrobat Reader DC, ad esempio l’aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con documenti abilitati per i diritti. I documenti di PDF a cui sono stati aggiunti i diritti di utilizzo sono denominati documenti abilitati per i diritti. Un utente che apre un documento PDF abilitato per i diritti in Adobe Reader può eseguire le operazioni abilitate per tale documento.

Ad Adobe, sfrutta una PKI (Public Key Infrastructure) per rilasciare certificati digitali da utilizzare per la concessione di licenze e l’abilitazione delle funzioni. L’Adobe ha rilasciato certificati ai sensi dell’autorità di certificazione &quot;Adobe Root CA&quot;, la cui scadenza è prevista per il 7 gennaio 2023. Porterà alla scadenza di tutti i certificati rilasciati in base a questa autorità di certificazione. Una volta scaduto il certificato, tutte le funzioni dipendenti dai certificati non funzionano più. Ad esempio, un documento PDF esteso tramite un lettore che consente l’aggiunta di commenti tramite Adobe Acrobat Reader smette di funzionare per i clienti dopo il 7 gennaio 2023. Per risolvere il problema, l&#39;amministratore del servizio Estensione Reader, utilizzando vecchi certificati, deve ottenere e riapplicare i nuovi certificati rilasciati dal nuovo Adobe Root CA G2 ai propri documenti PDF (il lettore estende i documenti PDF con nuovi certificati).

La scadenza dei certificati ha un impatto sia su AEM Forms su JEE che su AEM Forms sugli stack OSGi. Entrambi gli stack hanno un diverso set di istruzioni. Dopo la riunione [pre-richieste](#Pre-requisites) e [ottenimento di nuovi certificati](#obtain-the-certificates), a seconda della pila, scegli uno dei percorsi seguenti:

* [Aggiornamento dei certificati per un ambiente AEM Forms in JEE](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [Aggiornamento dei certificati per un ambiente AEM Forms in OSGi](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>Il documento utilizza certificati a termine e credenziali in modo intercambiabile.

## Prerequisiti {#Pre-requisites}

L’aggiornamento dei certificati richiede l’utilizzo delle azioni disponibili nella console di amministrazione di AEM Forms e nelle API di estensione di Reader fornite da AEM Forms. Il documento è destinato agli utenti e agli amministratori che conoscono l’utilizzo delle API Forms di Adobe Experience Manager. Prima di iniziare, assicurati che:

* l’utente dispone dei diritti di amministratore nell’ambiente AEM Forms sottostante.
* l&#39;utente ha impostato il [ambiente di sviluppo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) e ha accesso ad esso.
* ottenere i certificati.

### Recuperare i certificati {#obtain-the-certificates}

La credenziale dei diritti viene consegnata come certificato digitale contenente la chiave pubblica, la chiave privata e la password utilizzata per accedere alla credenziale.

Se l’organizzazione acquista una versione di produzione di Estensioni di Reader, la credenziale Diritti di produzione viene consegnata dal sito Web delle licenze Adobe (LWS). Una credenziale dei diritti di produzione è univoca per la tua organizzazione e può abilitare i diritti di utilizzo specifici necessari.

Se hai ottenuto estensioni di Reader tramite un partner o un fornitore di software che ha integrato le estensioni di Reader nel loro software, la credenziale relativa ai diritti viene fornita da quel partner che, a sua volta, riceve tale credenziale da Adobe.

>[!NOTE]
>
>Impossibile utilizzare la credenziale dei diritti per la firma o l&#39;asserzione tipica del documento. Per queste applicazioni è possibile utilizzare un certificato autofirmato o acquisire un certificato di identità da un’autorità di certificazione (CA).

Sono disponibili i seguenti tipi di credenziali dei diritti:

**Valutazione del cliente**: Credenziale con un breve periodo di validità fornito ai clienti che desiderano valutare le estensioni del Reader. I diritti di utilizzo applicati ai documenti che utilizzano questa credenziale scadono alla scadenza della credenziale. Questo tipo di credenziale è valido solo per due o tre mesi.

**Produzione**: Una credenziale con un periodo di validità lungo fornita ai clienti che hanno acquistato il prodotto completo. Le credenziali di produzione sono univoche per ogni cliente, ma possono essere installate su più sistemi.

Se hai già utilizzato dei certificati per l’estensione dei file PDF, scarica un certificato di produzione da [Sito Web Adobe Licensing (LWS)](https://licensing.adobe.com/).

## Aggiornamento e applicazione dei certificati per un ambiente AEM Forms in JEE {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

L’aggiornamento e l’applicazione di nuovi certificati su AEM Forms nello stack JEE richiede l’importazione di nuove credenziali, la rimozione dei diritti di utilizzo dai documenti PDF esistenti e l’applicazione dei diritti di utilizzo. Puoi utilizzare Admin Console per importare le credenziali e le API di AEM Forms Reader Extension per rimuovere e applicare i diritti di utilizzo.

### Importare e configurare le credenziali

È possibile utilizzare le pagine Gestione archivi attendibili per importare una credenziale nuova o sostitutiva. L&#39;archivio fonti attendibili può contenere più di un Reader di credenziali di estensione. È necessario specificare una di queste credenziali come credenziale predefinita delle estensioni di Reader. La credenziale predefinita viene utilizzata quando un utente di Workbench non è in grado di determinare quale credenziale utilizzare durante la creazione del processo. Queste regole si applicano alle credenziali predefinite:

* Se si importa una credenziale Estensioni di Reader e l&#39;archivio attendibilità non contiene altre credenziali delle Estensioni di Reader, questa viene impostata come predefinita.
* Se si importa una credenziale Estensioni Reader con l’opzione Predefinito selezionata, il tipo predefinito viene rimosso da una credenziale predefinita esistente. La credenziale importata diventa l’impostazione predefinita.
* Non è possibile eliminare una credenziale di estensioni di Reader predefinita. Per eliminare la credenziale predefinita, impostare prima un&#39;altra credenziale come predefinita. Fa eccezione il fatto che, se esiste una sola credenziale, è possibile eliminarla anche se è l’impostazione predefinita.
* Non è possibile aggiornare una credenziale di estensioni di Reader predefinita.

Per importare le credenziali:

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio attendibilità > Credenziali locali.
1. Fare clic su Importa e, in Tipo archivio fonti attendibili, selezionare Credenziali estensioni Acrobat Reader DC.
1. (Facoltativo) Per indicare che questa credenziale è la credenziale predefinita da utilizzare con le estensioni Acrobat Reader DC, selezionare Predefinito.
1. Nella casella Alias digitare un identificatore per la credenziale. Questo identificatore viene utilizzato come nome visualizzato per la credenziale nelle estensioni Acrobat Reader DC. Questo alias viene utilizzato anche per accedere alle credenziali a livello di programmazione utilizzando l’SDK per moduli AEM.
1. Fare clic su Scegli file per individuare la credenziale, digitare la password della credenziale, quindi fare clic su OK.

Se viene visualizzato il messaggio di errore &quot;Impossibile importare le credenziali a causa di un formato di file errato o di una password errata&quot;, verificare che la password sia valida.

È inoltre possibile importare ed eliminare le credenziali a livello di programmazione. (Vedi [Programmazione con moduli AEM](../../developing/credentials.md).)

### Rimuovere i diritti di utilizzo dai documenti PDF abilitati per i diritti esistenti

Rimuovere i diritti di utilizzo dai documenti PDF abilitati per i diritti esistenti prima di applicare i diritti di utilizzo con le credenziali più recenti. AEM Forms su JEE fornisce API per rimuovere i diritti di utilizzo. Per istruzioni dettagliate, vedi [Rimozione dei diritti di utilizzo dai documenti PDF](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Per rimuovere i diritti di utilizzo per AEM Forms sui processi JEE sviluppati in Workbench, vedi [Guida di Workbench](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### Applicazione dei diritti di utilizzo ai documenti PDF

Dopo aver importato nuove credenziali e rimosso i diritti di utilizzo dai documenti PDF abilitati per i diritti esistenti, applicare i diritti di utilizzo ai documenti PDF utilizzando le nuove credenziali. Puoi applicare i diritti di utilizzo ai documenti PDF utilizzando l’API client Java e il servizio Web Acrobat Reader DC extensions.  Per maggiori dettagli, vedi [Applicazione dei diritti di utilizzo ai documenti PDF](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## Aggiornamento e applicazione dei certificati per un ambiente AEM Forms in OSGi {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

L’aggiornamento e l’applicazione di nuovi certificati su AEM Forms nello stack OSGi richiede l’importazione di nuove credenziali, la rimozione dei diritti di utilizzo dai documenti PDF esistenti e l’applicazione dei diritti di utilizzo. Puoi utilizzare Admin Console per importare le credenziali e le API di AEM Forms Reader Extension per rimuovere e applicare i diritti di utilizzo.

### Importa credenziali {#Import-credentials}

In un ambiente AEM Forms su OSGi, una credenziale di estensione del Reader è associata a un utente del servizio fd. Prima di aggiungere le credenziali per l&#39;archivio chiavi dell&#39;utente fd, esegui seguenti passaggi per creare un archivio chiavi:

1. Accedi all’istanza di AEM Author come amministratore.
1. Vai a **[!UICONTROL Strumenti]**> **[!UICONTROL Sicurezza]**>**[!UICONTROL Utenti]**.
1. Scorri verso il basso l’elenco degli utenti fino a trovare l’account utente del servizio fd.
1. Fai clic su **[!UICONTROL servizio fd]** utente.
1. Fai clic sulla scheda keystore .
1. Fai clic su **[!UICONTROL Crea KeyStore]**.
1. Impostare la Password di accesso KeyStore e salvare le impostazioni per creare la password KeyStore.

Dopo aver creato l&#39;archivio chiavi, aggiungi le credenziali all&#39;utente del servizio fd. Il video seguente spiega i passaggi:

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

Il seguente comando elenca i dettagli del file pfx. Prima di eseguire il comando, passare alla directory rettangolare contenente il file .pfx.

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

Ad esempio keytool -v -list -storetype pkcs12 -keystore 1005566.pfx dove 1005566.pfx è il nome del mio file pfx

### Rimuovere i diritti di utilizzo dai documenti PDF abilitati per i diritti esistenti

Rimuovere i diritti di utilizzo dai documenti PDF abilitati per i diritti esistenti prima di applicare i diritti di utilizzo con le credenziali più recenti. È possibile rimuovere i diritti di utilizzo di un documento richiamando l&#39;API removeUsageRights dall&#39;interno di docAssuranceServiceAPI. Per informazioni dettagliate, consulta [Rimuovi diritti di utilizzo](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) documento.

### Applicazione dei diritti di utilizzo ai documenti PDF

Per applicare i diritti di utilizzo in un ambiente AEM Forms su OSGi, crea un servizio OSGi personalizzato per i diritti di utilizzo dei documenti. È inoltre possibile creare un servlet con un metodo POST per restituire all’utente l’estensione di PDF del lettore. Per istruzioni dettagliate, vedi [Applicazione delle estensioni del Reader](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## Domande frequenti

**Chi devo contattare se ho ulteriori domande?**

È possibile contattare [Supporto Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=it#support) o aumentare un ticket di supporto.

**Cosa succede se non aggiorno il certificato prima del 7 gennaio 2023?**

Quando si tenta di aprire un Reader di documenti PDF esteso con vecchi certificati, gli utenti ricevono un messaggio di errore e non possono più accedere alle funzioni estese del lettore. Un esempio di errore è .

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**C&#39;è qualche modifica nel nome della nuova descrizione?**

I nuovi certificati di estensione del Reader menzionano G3-P24 come nome del programma nella descrizione. Nei vecchi certificati, il nome del programma P24 è stato indicato nella descrizione.
