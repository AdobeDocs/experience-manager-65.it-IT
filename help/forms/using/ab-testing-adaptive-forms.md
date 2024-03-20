---
title: Creare e gestire test A/B per i moduli adattivi
description: AEM Forms si integra con Adobe Target che consente l’esecuzione di test A/B per i moduli adattivi per migliorare l’esperienza del cliente e i tassi di conversione.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---

# Creare e gestire test A/B per i moduli adattivi{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE Interrotto]{type=negative tooltip="Questa funzione è giunta al termine del ciclo di vita"}

<div class="preview"> La funzione di test A/B per i moduli adattivi ha raggiunto la fine del ciclo di vita e non è più supportata. </div>

## Panoramica {#overview-br}

È probabile che i clienti abbandonino un modulo se l’esperienza che fornisce non è coinvolgente. Se da un lato è frustrante per i clienti, dall’altro può anche aumentare il volume e i costi del supporto per la tua organizzazione. Identificare e fornire la giusta esperienza del cliente che aumenti il tasso di conversione è fondamentale e impegnativo. Adobe Experience Manager Forms è la chiave di questo problema.

AEM Forms si integra con Adobe Target, una soluzione Adobe Experience Cloud, per offrire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Una delle funzionalità principali di Target è il test A/B, che consente di configurare rapidamente test A/B simultanei, presentare contenuti rilevanti agli utenti target e identificare l’esperienza che determina un migliore tasso di conversione.

Con Adobe Experience Manager (AEM) Forms, puoi configurare ed eseguire test A/B sui moduli adattivi in tempo reale. Fornisce inoltre funzionalità di reporting pronte all’uso e personalizzabili per visualizzare le prestazioni in tempo reale delle esperienze dei moduli e identificare quella che massimizza il coinvolgimento e la conversione degli utenti.

## Configurare e integrare Target in AEM Forms {#set-up-and-integrate-target-in-aem-forms}

Prima di iniziare a creare e analizzare test A/B per i moduli adattivi, è necessario configurare il server Target e integrarlo in AEM Forms.

### Configurare Target {#set-up-target}

Per integrare l’AEM con Target, accertati di disporre di un account Adobe Target valido. Quando ti registri a Adobe Target, ricevi un codice cliente. Per collegare AEM a Target sono necessari il codice client, l’e-mail associata all’account Target e la password.

Il codice client identifica l’account cliente Adobe Target e viene utilizzato come sottodominio nell’URL quando si chiama il server Adobe Target. Prima di procedere, accedere a [https://experience.adobe.com/](https://experience.adobe.com/) e, se hai accesso, visualizza [!DNL Adobe Target] opzione in [!UICONTROL Accesso rapido] sezione.

### Integrare un server Target in esecuzione con AEM Forms {#integrate-target-in-aem-forms}

1. Sul server AEM, visitare il sito https://&lt;*nome host*>:&lt;*porta*>/libs/cq/core/content/tools/cloudservices.html.

1. In **Adobe Target** , fare clic su **Mostra configurazioni** e quindi il **+** per aggiungere una configurazione.
Se stai configurando una destinazione per la prima volta, fai clic su **Configura ora.**

1. Nella finestra di dialogo Crea configurazione, specifica un **Titolo** e facoltativamente un **Nome** per la configurazione.

1. Fai clic su **Crea**. Viene visualizzata la finestra di dialogo Modifica componente.
1. Specifica i dettagli dell’account Target, ad esempio codice client, e-mail e password.
1. Seleziona **Rest** dall’elenco a discesa Tipo API.

1. Clic **Connettersi ad Adobe Target** in modo da poter inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio Connessione riuscita. Clic **OK** sul messaggio e quindi **OK** nella finestra di dialogo. L’account Target è configurato.

1. Creare un framework Target come descritto in [Aggiungere un framework](/help/sites-administering/target.md).

1. Vai a https://&lt;*nome host*>:&lt;*porta*>/system/console/configMgr

1. Clic **Configurazione di AEM Forms Target**.
1. Seleziona un **Framework di destinazione**.
1. In **URL di destinazione** , specifica tutti gli URL in cui vengono eseguiti i test A/B. Ad esempio, https://&lt;*nome host*>:&lt;*porta*>/ per AEM Forms Server su OSGi o https://&lt;*nome host*>:&lt;*porta*>/lc/ per AEM Forms Server su JEE.
Considera di voler configurare un URL di Target per un’istanza Publish e che i tuoi clienti possano accedervi utilizzando il nome host o l’indirizzo IP. In questo caso, devi configurare sia come URL di Target, utilizzando il nome host che l’indirizzo IP. Se configuri solo uno degli URL, il test A/B non viene eseguito per i clienti provenienti dall’altro URL. Clic **+** per specificare più URL.

1. Fai clic su **Salva**.

Il server di Target è integrato con AEM Forms. Ora puoi abilitare il test A/B se disponi di una licenza completa per l’utilizzo di Adobe Target.

Se disponi di una licenza completa per l’utilizzo di Adobe Target, avvia il server con i seguenti parametri dopo aver integrato Target con AEM Forms:

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

Se l’istanza AEM è in esecuzione su JBoss®, avviato come servizio da chiavi in mano, in `jboss\bin\standalone.conf.bat` file, aggiungere il parametro -Dabtesting.enabled=true nella voce seguente:

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

Oltre al server JBoss®, è possibile aggiungere l&#39;argomento -Dabtesting.enabled=true jvm nello script di avvio del server per qualsiasi server applicazioni. Ora puoi creare ed eseguire test A/B per i moduli adattivi.

>[!NOTE]
>
>Se aggiorni gli URL di Target configurati in un secondo momento, accertati di aggiornare tutti i test A/B in esecuzione in modo che puntino agli URL correnti. Per informazioni sull’aggiornamento dei test A/B, consulta [Aggiorna test A/B](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).
>

## Creare tipi di pubblico in AEM {#create-audiences-within-aem}

AEM consente di creare un pubblico e di utilizzarlo per un test A/B. Il pubblico creato all’interno dell’AEM è disponibile in AEM Forms. Per creare un pubblico in AEM, effettua le seguenti operazioni:

1. Nell’istanza di authoring, seleziona **Adobe Experience Manager** > **Personalizzazione** > **Tipi di pubblico**.

1. Nella pagina Tipi di pubblico, seleziona **Crea pubblico > Crea pubblico Target**.
1. Nella finestra di dialogo Configurazione di Adobe Target, seleziona una configurazione di Target e fai clic su **Ok**.
1. Nella pagina Crea nuovo pubblico, crea le regole. Le regole ti consentono di categorizzare il pubblico. Ad esempio, puoi categorizzare i tipi di pubblico in base al sistema operativo. Il pubblico A proviene da Windows, mentre il pubblico B proviene da Linux®.

   1. Per categorizzare un pubblico in base a Windows, in #1 regole seleziona la **SO** tipo di attributo. Dall’elenco a discesa When (Quando), seleziona **Windows.**

   1. Per categorizzare il pubblico in base a Linux®, in #2 regole seleziona la **SO** tipo di attributo. Dalla sezione **Quando** a discesa, seleziona **Linux®** e fai clic su **Successivo**.

1. Specifica un nome per il pubblico creato e fai clic su **Salva**.

Puoi selezionare il pubblico quando configuri il test A/B per un modulo, come mostrato di seguito.

## Creare un test A/B per un modulo adattivo {#create-a-b-test}

1. Vai a **Forms e documenti** in https://&lt;*nome host*>:&lt;*porta*>/aem/forms.html/content/dam/formsanddocuments.

1. Passa alla cartella contenente il modulo adattivo.
1. Fai clic su **Seleziona** nella barra degli strumenti e seleziona il modulo adattivo.
1. Clic **Altro** nella barra degli strumenti e seleziona **Configurare il test A/B**. Viene visualizzata la pagina Configura test A/B.

[](assets/ab-test-configure-1.png)

1. Specifica un **Nome attività** test A/B.

1. Dall’elenco a discesa Pubblico, seleziona un pubblico a cui desideri indirizzare diverse esperienze del modulo. Ad esempio: **Visitatori che utilizzano Chrome**. L’elenco dei tipi di pubblico viene popolato dal server di Target configurato.

1. In **Distribuzione delle esperienze** campi per le esperienze A e B, specifica la distribuzione, in termini percentuali, per determinare la distribuzione delle esperienze tra il pubblico totale. Ad esempio, se specifichi 40, 60 per le esperienze A e B, rispettivamente, l’esperienza A viene trasmessa al 40% del pubblico e il restante 60% visualizza l’esperienza B.
1. Clic **Configura**. Viene visualizzata una finestra di dialogo per confermare la creazione del test A/B.
1. Clic **Modifica esperienza B** in modo da poter aprire il modulo adattivo in modalità di modifica. Modifica il modulo creando un’esperienza diversa da quella predefinita. Le possibili varianti consentite nell’Esperienza B sono le modifiche in:

   * CSS o stile
   * Ordine dei campi in pannelli diversi o nello stesso pannello
   * Layout pannello
   * Titoli dei pannelli
   * Descrizione, etichetta e testo della guida di un campo
   * Script che non influiscono sul flusso di invio o lo interrompono
   * Convalide (lato client e lato server)
   * Tema per l’esperienza B. (puoi selezionare un tema alternativo per l’esperienza B)

1. Vai all’interfaccia utente di Forms e Documenti, seleziona il modulo adattivo, fai clic su **Altro**, e seleziona **Avvia test A/B**.

Il test A/B è ora in esecuzione e al pubblico specificato vengono distribuite in modo casuale le esperienze in base alla distribuzione specificata.

## Aggiornare il test A/B {#update-a-b-test}

Puoi aggiornare le distribuzioni di pubblico ed esperienza di un test A/B in esecuzione.

Per aggiornare il test A/B:

1. Nell’interfaccia utente di Forms &amp; Documents, passa alla cartella contenente il modulo adattivo su cui è in esecuzione il test A/B.
1. Seleziona il modulo adattivo.
1. Clic **Altro** e quindi seleziona **Modifica test A/B**. Viene visualizzata la pagina Aggiorna test A/B.

1. Aggiorna le distribuzioni di pubblico ed esperienza in base alle esigenze.
1. Fai clic su **Aggiorna**.

## Visualizzare e analizzare il rapporto sui test A/B {#view-and-analyze-a-b-test-report}

Dopo aver consentito l’esecuzione del test A/B per il periodo desiderato, puoi generare un rapporto e verificare quale esperienza ha prodotto una conversione migliore. Puoi dichiarare vincitrice l’esperienza con prestazioni migliori oppure scegliere di eseguire un altro test A/B.

Per visualizzare e analizzare il rapporto del test A/B:

1. Seleziona il modulo adattivo e fai clic su **Altro** e quindi fare clic su **Rapporto test A/B**. Il report viene visualizzato.

[](assets/ab-test-report-3.png)

1. Analizza il rapporto e verifica di disporre di un numero sufficiente di punti dati per dichiarare vincitrice una delle esperienze con prestazioni migliori. Puoi scegliere di continuare con lo stesso test A/B per più tempo o dichiarare un vincitore e terminare il test A/B.
1. Per dichiarare un vincitore e terminare il test A/B, fai clic sul pulsante **Termina test A/B** nel dashboard di reporting. Viene visualizzata una finestra di dialogo in cui viene richiesto di dichiarare vincitrice una delle due esperienze. Scegli un vincitore e conferma di terminare il test A/B.
In alternativa, è possibile dichiarare un vincitore facendo clic sul pulsante **Dichiara vincitore** per la rispettiva esperienza. Ti chiede di confermare il vincitore. Clic **Sì** per terminare il test A/B.

Se hai scelto l&#39;esperienza A come vincitrice, il test A/B viene terminato e, andando avanti, solo l&#39;esperienza A viene trasmessa al pubblico.
