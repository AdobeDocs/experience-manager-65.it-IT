---
title: Creazione e gestione di test A/B per i moduli adattivi
seo-title: Creazione e gestione di test A/B per i moduli adattivi
description: ' AEM Forms si integra con  Adobe Target che consente di eseguire test A/B per moduli adattivi per migliorare l''esperienza del cliente e migliorare i tassi di conversione.'
seo-description: ' AEM Forms si integra con  Adobe Target che consente di eseguire test A/B per moduli adattivi per migliorare l''esperienza del cliente e migliorare i tassi di conversione.'
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---


# Creazione e gestione di test A/B per moduli adattivi{#create-and-manage-a-b-test-for-adaptive-forms}

## Panoramica {#overview-br}

È probabile che i clienti abbandonino un modulo se l&#39;esperienza non è coinvolgente. Anche se è frustrante per i clienti, può anche aumentare il volume e i costi del supporto per la vostra organizzazione. È fondamentale e difficile identificare e fornire al cliente la giusta esperienza che aumenta il tasso di conversione.  Adobe Experience Manager Forms è la chiave di questo problema.

 AEM Forms si integra con  Adobe Target, una soluzione Adobe Marketing Cloud, per offrire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Una delle funzionalità chiave dei test A/B di Target è il test A/B che consente di impostare rapidamente test A/B simultanei, presentare contenuti pertinenti a utenti mirati e identificare l&#39;esperienza che determina un migliore tasso di conversione.

Con  AEM Forms, è possibile impostare ed eseguire test A/B sui moduli adattivi in tempo reale. Fornisce inoltre funzionalità di reporting pronte all&#39;uso e personalizzabili per visualizzare le prestazioni in tempo reale delle esperienze del modulo e identificare quella che massimizza il coinvolgimento e la conversione degli utenti.

## Configurare e integrare Target in  AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Prima di iniziare a creare e analizzare test A/B per i moduli adattivi, è necessario configurare il server Target e integrarlo in  AEM Forms.

### Imposta destinazione {#set-up-target}

Per integrare AEM con Target, accertatevi di disporre di un account Adobe Target  valido. Quando vi registrate  Adobe Target, ricevete un codice cliente. Per connettersi a AEM Target è necessario disporre del codice client, dell&#39;e-mail associata all&#39;account Target e della password.

Il Codice client identifica l&#39;account cliente Adobe Target  e viene utilizzato come sottodominio nell&#39;URL quando si chiama il server Adobe Target . Prima di continuare, accertati che le tue credenziali ti consentano di accedere a [https://testandtarget.omniture.com/](https://testandtarget.omniture.com/).

### Integrare Target in  AEM Forms {#integrate-target-in-aem-forms}

Per integrare un server Target in esecuzione con  AEM Forms, effettua i seguenti passaggi:

1. Sul server AEM andare a https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. Nella sezione **Adobe Target**, fare clic su **Mostra configurazioni**, quindi sull&#39;icona **+** per aggiungere una nuova configurazione.
Se state configurando la destinazione per la prima volta, fate clic su **Configura ora.**

1. Nella finestra di dialogo Crea configurazione, specificate un **Titolo** e facoltativamente un **Nome** per la configurazione.

1. Fai clic su **Crea**. Viene visualizzata la finestra di dialogo Modifica componente.
1. Specificate i dettagli dell&#39;account Target, ad esempio codice cliente, e-mail e password.
1. Selezionate **Rest** dall&#39;elenco a discesa Tipo API.

1. Fate clic su **Connetti per  Adobe Target** per inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio Connessione riuscita. Fare clic su **OK** sul messaggio, quindi su **OK** nella finestra di dialogo. L&#39;account Target è configurato.

1. Create un framework Target come descritto in [Add a framework](/help/sites-administering/target.md) (Aggiungi un framework&lt;a1/>).

1. Andate a https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr.

1. Fate clic su **AEM Forms Target Configuration**.
1. Selezionare un **Framework di destinazione**.
1. Nel campo **URL di destinazione**, specificate tutti gli URL in cui verranno eseguiti i test A/B. Ad esempio, https://&lt;*hostname*>:&lt;*port*>/ per  server AEM Forms su OSGi o https://&lt;*hostname*>:&lt;*port*/lc/ per  server AEM Forms su JEE.
Considerate la possibilità di configurare un URL Target per un&#39;istanza di pubblicazione e i vostri clienti potranno accedervi utilizzando il nome host o l&#39;indirizzo IP, dovrete configurare sia come URL Target, utilizzando sia il nome host che l&#39;indirizzo IP. Se configurate solo uno degli URL, il test A/B non verrà eseguito per i clienti che provengono dall&#39;altro URL. Fate clic su **+** per specificare più URL.

1. Fai clic su **Salva**.

Il server di Target è integrato con  AEM Forms. Ora potete abilitare il test A/B se disponete di una licenza completa per utilizzare  Adobe Target.

Se disponete di una licenza completa per utilizzare  Adobe Target, avviate il server con i seguenti parametri dopo aver integrato Target con  AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Se l&#39;istanza AEM è in esecuzione su JBoss, avviata come servizio da chiavi in mano, nel file `jboss\bin\standalone.conf.bat` aggiungere il parametro -Dabtesting.enabled=true nella voce seguente:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Oltre al server jboss, puoi aggiungere -Dabtesting.enabled=vero argomento jvm nello script di avvio del server per qualsiasi server applicazione. È ora possibile creare ed eseguire test A/B per i moduli adattivi.

>[!NOTE]
>
>Se aggiornate successivamente gli URL di Target configurati, accertatevi di aggiornare eventuali test A/B in esecuzione in modo che puntino agli URL correnti. Per informazioni sull&#39;aggiornamento dei test A/B, vedere [Aggiornamento dei test A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).


## Creazione di audience all&#39;interno di AEM {#create-audiences-within-aem}

AEM consente di creare un&#39;audience e di utilizzarla per un test A/B. L&#39;audience creata all&#39;interno AEM è disponibile in  AEM Forms. Per creare audience all&#39;interno di AEM, effettuate le seguenti operazioni:

1. Nell&#39;istanza di creazione, toccare **Adobe Experience Manager** > **Personalizzazione** > **Audiences**.

1. Nella pagina Pubblico, tocca **Crea pubblico > Crea pubblico Target**.
1. Nella finestra di dialogo Configurazione Adobe Target , selezionate una configurazione Target e fate clic su **Ok**.
1. Nella pagina Crea nuovo pubblico, crea le regole. Le regole consentono di classificare l&#39;audience. Ad esempio, si desidera classificare le audience in base al sistema operativo. Il pubblico A viene da Windows, e il pubblico B viene da Linux.

   1. Per classificare l&#39;audience in base a Windows, nella regola n. 1, selezionare il tipo di attributo **OS**. Dall&#39;elenco a discesa Quando, selezionare **Windows.**

   1. Per classificare l&#39;audience in base a Linux, nella regola n. 2, selezionare il tipo di attributo **OS**. Dal menu a discesa **Quando**, selezionare **Linux**, quindi fare clic su **Next**.

1. Specificate un nome per il pubblico creato e fate clic su **Salva**.

È possibile selezionare l&#39;audience quando si configura il test A/B per un modulo, come illustrato di seguito.

## Crea test A/B {#create-a-b-test}

Effettuare le seguenti operazioni per creare un test A/B per un modulo adattivo.

1. Andate a **Forms &amp; Documents** all&#39;indirizzo https://&lt;*hostname*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Passate alla cartella contenente il modulo adattivo.
1. Fare clic sullo strumento **Seleziona** nella barra degli strumenti e selezionare il modulo adattivo.
1. Fare clic su **Altro** nella barra degli strumenti e selezionare **Configura test A/B**. Viene visualizzata la pagina Configura test A/B.

[ ![Pagina di configurazione del test A/B per i moduli adattivi](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. Specificare un **Nome attività** per il test A/B.

1. Dall&#39;elenco a discesa Pubblico, selezionare un&#39;audience a cui distribuire diverse esperienze del modulo. Ad esempio, **Visitatori che utilizzano Chrome**. L&#39;elenco di audience viene popolato dal server di Target configurato.

1. Nei campi **Distribuzione esperienza** per le esperienze A e B, specificate la distribuzione, in termini percentuali, per determinare la distribuzione delle esperienze tra il pubblico totale. Ad esempio, se specificate 40, 60 rispettivamente per le esperienze A e B, l&#39;esperienza A verrà servita al 40% del pubblico e il restante 60% visualizzerà l&#39;esperienza B.
1. Fare clic su **Configura**. Viene visualizzata una finestra di dialogo per confermare la creazione del test A/B.
1. Fate clic su **Modifica esperienza B** per aprire il modulo adattivo in modalità di modifica. Modificare il modulo per creare un&#39;esperienza diversa dall&#39;esperienza predefinita A. Le possibili variazioni consentite nell&#39;Esperienza B sono le modifiche in:

   * CSS o stile
   * Ordine dei campi in diversi pannelli o nello stesso pannello
   * Layout pannello
   * Titoli del pannello
   * Descrizione, etichetta e testo della guida per un campo
   * Script che non influiscono sul flusso di invio o lo interrompono
   * Convalida (lato client e lato server)
   * Tema per l&#39;esperienza B. (Potete selezionare un tema alternativo per l&#39;esperienza B)

1. Passate all&#39;interfaccia utente Forms e Documenti, selezionate il modulo adattivo, fate clic su **Altro**, quindi selezionate **Avvia test A/B**.

Il test A/B è ora in esecuzione e l&#39;audience specificata verrà servita in modo casuale in base alla distribuzione specificata.

## Aggiorna test A/B {#update-a-b-test}

Potete aggiornare le distribuzioni di audience ed esperienze di un test A/B in esecuzione. A questo scopo:

1. Nell’interfaccia utente di Forms e documenti, individuate la cartella che contiene il modulo adattivo sul quale viene eseguito il test A/B.
1. Selezionare il modulo adattivo.
1. Fare clic su **Altro**, quindi selezionare **Modifica test A/B**. Viene visualizzata la pagina Aggiorna test A/B.

1. Aggiornate le distribuzioni di audience ed esperienze, a seconda delle necessità.
1. Fare clic su **Aggiorna**.

## Visualizzare e analizzare il rapporto test A/B {#view-and-analyze-a-b-test-report}

Dopo aver consentito l&#39;esecuzione del test A/B per il periodo desiderato, potete generare un rapporto e verificare quale esperienza ha portato a una conversione migliore. Potete dichiarare vincente l&#39;esperienza con prestazioni migliori o scegliere di eseguire un altro test A/B. Per eseguire questa operazione, effettuare le seguenti operazioni:

1. Selezionate il modulo adattivo, fate clic su **Altro**, quindi fate clic su **A/B Testing Report**. Viene visualizzato il rapporto.

[ ![Report test A/B](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. Analizzare il rapporto e verificare se sono presenti abbastanza punti dati per dichiarare vincente una delle esperienze con prestazioni migliori. Potete scegliere di continuare con lo stesso test A/B per più tempo oppure dichiarare un vincitore e terminare il test A/B.
1. Per dichiarare un vincitore e terminare il test A/B, fate clic sul pulsante **Termina test A/B** nel dashboard di reporting. Viene visualizzata una finestra di dialogo in cui viene richiesto di dichiarare vincente una delle due esperienze. Scegliete un vincitore e confermate la fine del test A/B.
In alternativa, potete prima dichiarare un vincitore facendo clic sul pulsante **Dichiara vincitore** per la relativa esperienza. Viene richiesto di confermare il vincitore. Fare clic su **Sì** per terminare il test A/B.

Se avete scelto l&#39;esperienza A come vincitore, il test A/B verrà messo al termine e, andando avanti, solo l&#39;Esperienza A verrà servita a tutti i tipi di pubblico.
