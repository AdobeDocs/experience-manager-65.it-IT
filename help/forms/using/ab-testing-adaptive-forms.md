---
title: Creazione e gestione di test A/B per i moduli adattivi
seo-title: Creazione e gestione di test A/B per i moduli adattivi
description: AEM Forms si integra con Adobe Target e consente di eseguire test A/B per moduli adattivi per migliorare l'esperienza dei clienti e i tassi di conversione.
seo-description: AEM Forms si integra con Adobe Target e consente di eseguire test A/B per moduli adattivi per migliorare l'esperienza dei clienti e i tassi di conversione.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
translation-type: tm+mt
source-git-commit: 3eaace94bc0499aaebfcd389d4dc97b97c7d9160

---


# Creazione e gestione di test A/B per i moduli adattivi{#create-and-manage-a-b-test-for-adaptive-forms}

## Panoramica {#overview-br}

È probabile che i clienti abbandonino un modulo se l&#39;esperienza non è coinvolgente. Anche se è frustrante per i clienti, può anche aumentare il volume e i costi del supporto per la vostra organizzazione. È fondamentale e difficile identificare e fornire al cliente la giusta esperienza che aumenta il tasso di conversione. Adobe Experience Manager Forms è la chiave di questo problema.

AEM Forms si integra con Adobe Target, una soluzione Adobe Marketing Cloud, per offrire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Una delle funzionalità chiave dei test A/B di Target è il test A/B che consente di impostare rapidamente test A/B simultanei, presentare contenuti pertinenti a utenti mirati e identificare l&#39;esperienza che determina un migliore tasso di conversione.

Con AEM Forms, potete impostare ed eseguire test A/B sui moduli adattivi in tempo reale. Fornisce inoltre funzionalità di reporting pronte all&#39;uso e personalizzabili per visualizzare le prestazioni in tempo reale delle esperienze del modulo e identificare quella che massimizza il coinvolgimento e la conversione degli utenti.

## Configurare e integrare Target in AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Prima di iniziare a creare e analizzare test A/B per i moduli adattivi, è necessario configurare il server Target e integrarlo in AEM Forms.

### Impostazione di Target {#set-up-target}

Per integrare AEM con Target, accertati di disporre di un account Adobe Target valido. Quando vi registrate con Adobe Target, riceverete un codice client. Per collegare AEM a Target, è necessario disporre del codice client, dell&#39;e-mail associato all&#39;account Target e della password.

Il Codice client identifica l&#39;account cliente Adobe Target e viene utilizzato come sottodominio nell&#39;URL quando si chiama il server Adobe Target. Prima di continuare, accertatevi che le credenziali vi consentano di accedere a [https://testandtarget.omniture.com/](https://testandtarget.omniture.com/).

### Integrazione di Target in AEM Forms {#integrate-target-in-aem-forms}

Per integrare un server Target in esecuzione con AEM Forms, effettua i seguenti passaggi:

1. Nel server AEM, andate a https://&lt;*hostname*>:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html.

1. Nella sezione **Adobe Target** , fai clic su **Mostra configurazioni** , quindi sull&#39;icona **+** per aggiungere una nuova configurazione.
Se state configurando la destinazione per la prima volta, fate clic su **Configura ora.**

1. Nella finestra di dialogo di configurazione Crea, specificate un **Titolo** ed eventualmente un **Nome** per la configurazione.

1. Fai clic su **Crea**. Viene visualizzata la finestra di dialogo Modifica componente.
1. Specificate i dettagli dell&#39;account Target, ad esempio codice cliente, e-mail e password.
1. Selezionate **Rest** dall&#39;elenco a discesa Tipo API.

1. Fate clic su **Connetti ad Adobe Target** per inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio Connessione riuscita. Fare clic su **OK** sul messaggio, quindi su **OK** nella finestra di dialogo. L&#39;account Target è configurato.

1. Create un framework Target come descritto in [Aggiungi un framework](/help/sites-administering/target.md).

1. Andate a https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr.

1. Fate clic su Configurazione **destinazione** AEM Forms.
1. Selezionate un framework **** Target.
1. Nel campo URL **** Target, specificate tutti gli URL in cui verranno eseguiti i test A/B. Ad esempio, https://&lt;*hostname*>:&lt;*port*>/ per il server AEM Forms su OSGi o https://&lt;*hostname*>:&lt;*port*>/lc/ per il server AEM Forms su JEE.
Considerate la possibilità di configurare un URL Target per un&#39;istanza di pubblicazione e i vostri clienti potranno accedervi utilizzando il nome host o l&#39;indirizzo IP, dovrete configurare sia come URL Target, utilizzando sia il nome host che l&#39;indirizzo IP. Se configurate solo uno degli URL, il test A/B non verrà eseguito per i clienti che provengono dall&#39;altro URL. Fate clic **+** per specificare più URL.

1. Fai clic su **Salva**.

Il server di Target è integrato con AEM Forms. Ora potete abilitare il test A/B se disponete di una licenza completa per utilizzare Adobe Target.

Se disponete di una licenza completa per utilizzare Adobe Target, avviate il server con i seguenti parametri dopo aver integrato Target con AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Se l’istanza AEM è in esecuzione su JBoss, avviata come servizio da chiavi in mano, nel `jboss\bin\standalone.conf.bat` file, aggiungi il parametro -Dabtesting.enabled=true nella voce seguente:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Oltre al server jboss, puoi aggiungere -Dabtesting.enabled=vero argomento jvm nello script di avvio del server per qualsiasi server applicazione. È ora possibile creare ed eseguire test A/B per i moduli adattivi.

>[!NOTE]
>
>Se aggiornate successivamente gli URL di Target configurati, accertatevi di aggiornare eventuali test A/B in esecuzione in modo che puntino agli URL correnti. Per informazioni sull&#39;aggiornamento dei test A/B, vedere [Aggiornamento del test](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)A/B.


## Creazione di audience in AEM {#create-audiences-within-aem}

AEM consente di creare un pubblico e di utilizzarlo per un test A/B. Il pubblico creato in AEM è disponibile in AEM Forms. Per creare audience in AEM, effettuate le seguenti operazioni:

1. Nell’istanza di creazione, tocca **Adobe Experience Manager** > **Personalizzazione** > **Audience**.

1. Nella pagina Audiences (Audience), tocca **Create Audience (Crea pubblico) > Create Target Audience (Crea pubblico Target)**.
1. Nella finestra di dialogo Configurazione Adobe Target, selezionate una configurazione Target e fate clic su **OK**.
1. Nella pagina Crea nuovo pubblico, crea le regole. Le regole consentono di classificare l&#39;audience. Ad esempio, si desidera classificare le audience in base al sistema operativo. Il pubblico A viene da Windows, e il pubblico B viene da Linux.

   1. Per classificare l&#39;audience in base a Windows, nella regola n. 1, selezionate il tipo di attributo **del sistema operativo** . Dal menu a discesa Quando, selezionate **Windows.**

   1. Per classificare il pubblico in base a Linux, nella regola n. 2, selezionate il tipo di attributo **del sistema operativo** . Dal menu a discesa **Quando** , selezionate **Linux** e fate clic su **Avanti**.

1. Specificate un nome per l&#39;audience creata e fate clic su **Salva**.

È possibile selezionare l&#39;audience quando si configura il test A/B per un modulo, come illustrato di seguito.

## Crea test A/B {#create-a-b-test}

Effettuare le seguenti operazioni per creare un test A/B per un modulo adattivo.

1. Per informazioni su **moduli e documenti** , vedere https://&lt;*hostname*>:&lt;*port*>/aem/forms.html/content/dam/formsanddocuments.

1. Passate alla cartella contenente il modulo adattivo.
1. Fare clic sullo strumento **Seleziona** nella barra degli strumenti e selezionare il modulo adattivo.
1. Fate clic su **Altro** nella barra degli strumenti e selezionate **Configura test** A/B. Viene visualizzata la pagina Configura test A/B.

[ Pagina di configurazione del test ![A/B per i moduli adattivi](assets/ab-test-configure.png)](assets/ab-test-configure-1.png)

1. Specificate un Nome **** attività per il test A/B.

1. Dall&#39;elenco a discesa Pubblico, selezionare un&#39;audience a cui distribuire diverse esperienze del modulo. Ad esempio, **Visitatori che utilizzano Chrome**. L&#39;elenco di audience viene compilato dal server di Target configurato.

1. Nei campi Distribuzione **** esperienza per le esperienze A e B, specificate la distribuzione, in termini percentuali, per determinare la distribuzione delle esperienze tra il pubblico totale. Ad esempio, se specificate 40, 60 rispettivamente per le esperienze A e B, l&#39;esperienza A verrà servita al 40% del pubblico e il restante 60% visualizzerà l&#39;esperienza B.
1. Fate clic su **Configura**. Viene visualizzata una finestra di dialogo per confermare la creazione del test A/B.
1. Fate clic su **Modifica esperienza B** per aprire il modulo adattivo in modalità di modifica. Modificare il modulo per creare un&#39;esperienza diversa dall&#39;esperienza predefinita A. Le possibili variazioni consentite nell&#39;Esperienza B sono le modifiche in:

   * CSS o stile
   * Ordine dei campi in diversi pannelli o nello stesso pannello
   * Layout pannello
   * Titoli del pannello
   * Descrizione, etichetta e testo della guida per un campo
   * Script che non influiscono sul flusso di invio o lo interrompono
   * Convalida (lato client e lato server)
   * Tema per l&#39;esperienza B. (Potete selezionare un tema alternativo per l&#39;esperienza B)

1. Passare all’interfaccia utente Moduli e documenti, selezionare il modulo adattivo, fare clic su **Altro** e selezionare **Avvia test** A/B.

Il test A/B è ora in esecuzione e l&#39;audience specificata verrà servita in modo casuale in base alla distribuzione specificata.

## Update A/B test {#update-a-b-test}

Potete aggiornare le distribuzioni di audience ed esperienze di un test A/B in esecuzione. A questo scopo:

1. Nell&#39;interfaccia utente Moduli e documenti, passare alla cartella contenente il modulo adattivo sul quale è in esecuzione il test A/B.
1. Selezionare il modulo adattivo.
1. Fate clic su **Altro** , quindi selezionate **Modifica test** A/B. Viene visualizzata la pagina Aggiorna test A/B.

1. Aggiornate le distribuzioni di audience ed esperienze, a seconda delle necessità.
1. Click **Update**.

## Visualizzare e analizzare il rapporto test A/B {#view-and-analyze-a-b-test-report}

Dopo aver consentito l&#39;esecuzione del test A/B per il periodo desiderato, potete generare un rapporto e verificare quale esperienza ha portato a una conversione migliore. Potete dichiarare vincente l&#39;esperienza con prestazioni migliori o scegliere di eseguire un altro test A/B. Per eseguire questa operazione, effettuare le seguenti operazioni:

1. Selezionate il modulo adattivo, fate clic su **Altro**, quindi fate clic su Rapporto **** test A/B. Viene visualizzato il rapporto.

[ Report test ![A/B](assets/ab-test-report-2.png)](assets/ab-test-report-3.png)

1. Analizzare il rapporto e verificare se sono presenti abbastanza punti dati per dichiarare vincente una delle esperienze con prestazioni migliori. Potete scegliere di continuare con lo stesso test A/B per più tempo oppure dichiarare un vincitore e terminare il test A/B.
1. Per dichiarare un vincitore e terminare il test A/B, fate clic sul pulsante **Termina test** A/B nel dashboard di reporting. Viene visualizzata una finestra di dialogo in cui viene richiesto di dichiarare vincente una delle due esperienze. Scegliete un vincitore e confermate la fine del test A/B.
In alternativa, potete prima dichiarare un vincitore facendo clic sul pulsante **Dichiara vincitore** per la relativa esperienza. Viene richiesto di confermare il vincitore. Fate clic su **Sì** per terminare il test A/B.

Se avete scelto l&#39;esperienza A come vincitore, il test A/B verrà messo al termine e, andando avanti, solo l&#39;Esperienza A verrà servita a tutti i tipi di pubblico.
