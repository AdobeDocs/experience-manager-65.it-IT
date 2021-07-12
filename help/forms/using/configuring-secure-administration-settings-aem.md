---
title: Configurazione delle impostazioni di amministrazione sicura per AEM Forms su JEE
seo-title: Configurazione delle impostazioni di amministrazione sicura per AEM Forms su JEE
description: Scopri come amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono necessari in un ambiente di produzione di AEM Forms su JEE.
seo-description: Scopri come amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono necessari in un ambiente di produzione di AEM Forms su JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Configurazione delle impostazioni di amministrazione sicura per AEM Forms su JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Scopri come amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono necessari in un ambiente di produzione di AEM Forms su JEE.

In genere, gli sviluppatori non utilizzano l’ambiente di produzione per creare e testare le applicazioni. Pertanto, devi amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono necessari in un ambiente di produzione.

Questo articolo descrive i metodi per ridurre la superficie di attacco complessiva attraverso le opzioni di amministrazione fornite da AEM Forms su JEE.

## Disabilitazione dell’accesso remoto non essenziale ai servizi {#disabling-non-essential-remote-access-to-services}

Dopo l&#39;installazione e la configurazione di AEM Forms su JEE, molti servizi sono disponibili per la chiamata remota tramite SOAP e Enterprise JavaBeans™ (EJB). Il termine remoto, in questo caso, fa riferimento a qualsiasi chiamante con accesso di rete alle porte SOAP, EJB o AMF (Action Message Format) per l&#39;application server.

Anche se i servizi AEM Forms su JEE richiedono la trasmissione di credenziali valide per un chiamante autorizzato, è consigliabile consentire solo l&#39;accesso remoto ai servizi che devono essere accessibili in remoto. Per ottenere un&#39;accessibilità limitata, è necessario ridurre al minimo il set di servizi accessibili in remoto per un sistema funzionante e quindi abilitare la chiamata remota per i servizi aggiuntivi necessari.

AEM Forms sui servizi JEE richiede sempre almeno l’accesso SOAP. Questi servizi sono generalmente necessari per l’utilizzo da parte di Workbench, ma includono anche i servizi chiamati dall’applicazione Web Workspace.

Completa questa procedura utilizzando la pagina web Applicazioni e servizi in Admin Console:

1. Accedi alla console di amministrazione digitando il seguente URL in un browser web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Fai clic su **Servizi > Applicazioni e servizi > Preferenze**.
1. Imposta Preferenze per visualizzare fino a 200 servizi e endpoint sulla stessa pagina.
1. Fai clic su **Servizi** > **Applicazioni e servizi** > **Gestione endpoint**.
1. Seleziona **EJB** dall&#39;elenco **Provider**, quindi fai clic su **Filtro**.
1. Per disabilitare tutti gli endpoint EJB, seleziona la casella di controllo accanto a ciascuno nell&#39;elenco e fai clic su **Disattiva**.
1. Fai clic su **Avanti** e ripeti il passaggio precedente per tutti gli endpoint EJB. Assicurati che EJB sia elencato nella colonna Provider prima di disabilitare gli endpoint .
1. Selezionare **SOAP** dall&#39;elenco **Provider**, quindi fare clic su **Filtro**.
1. Per rimuovere gli endpoint SOAP, selezionare la casella di controllo accanto a ciascuno nell&#39;elenco e fare clic su **Rimuovi**. Non rimuovere i seguenti endpoint:

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * Area di lavoroSingleSignOn
   * ApplicationManager

1. Fare clic su **Successivo** e ripetere il passaggio precedente per gli endpoint SOAP che non si trovano nell&#39;elenco precedente. Prima di rimuovere gli endpoint, verificare che SOAP sia elencato nella colonna Provider.

## Disabilitazione dell’accesso anonimo non essenziale ai servizi {#disabling-non-essential-anonymous-access-to-services}

Alcuni servizi server di Forms consentono chiamate non autenticate (anonime) per alcune operazioni. Ciò significa che una o più operazioni esposte dal servizio possono essere richiamate come qualsiasi utente autenticato o come nessun utente autenticato.

1. Accedi alla console di amministrazione digitando il seguente URL in un browser web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Fai clic su **Servizi > Applicazioni e servizi > Gestione dei servizi**.
1. Fare clic sul nome del servizio che si desidera disattivare (ad esempio, AuthenticationManagerService).
1. Fai clic sulla scheda **Sicurezza**, deseleziona **Accesso anonimo consentito** e fai clic su **Salva**.
1. Completa i passaggi 3 e 4 per i seguenti servizi:

   * AuthenticationManagerService
   * EJB
   * E-mail
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * Remoto
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * ConnettoreGestioneAttività
   * TaskManagerQueryService
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Se desideri esporre uno di questi servizi per la chiamata remota, dovresti anche considerare la possibilità di disabilitare l&#39;accesso anonimo per questi servizi. In caso contrario, qualsiasi chiamante con accesso di rete a questo servizio può richiamare il servizio senza passare credenziali valide.

   L’accesso anonimo deve essere disattivato per tutti i servizi non necessari. Molti servizi interni richiedono l’abilitazione dell’autenticazione anonima perché devono essere richiamati da qualsiasi utente potenzialmente presente nel sistema senza essere preautorizzati.

## Modifica del timeout globale predefinito {#changing-the-default-global-time-out}

Gli utenti finali possono eseguire l’autenticazione in AEM Forms tramite Workbench, le applicazioni web AEM Forms o le applicazioni personalizzate che richiamano i servizi server AEM Forms. Viene utilizzata un’impostazione di timeout globale per specificare per quanto tempo questi utenti possono interagire con AEM Forms (utilizzando un’asserzione basata su SAML) prima di essere costretti a ripetere l’autenticazione. L&#39;impostazione predefinita è di due ore. In un ambiente di produzione, il tempo deve essere ridotto al numero minimo di minuti accettabile.

### Limite minimo di tempo per la riautenticazione {#minimize-reauthentication-time-limit}

1. Accedi alla console di amministrazione digitando il seguente URL in un browser web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Fai clic su **Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione**.
1. Fai clic su **Esporta** per produrre un file config.xml con le impostazioni AEM Forms esistenti.
1. Apri il file XML in un editor e individua la voce seguente:

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. Modifica il valore in un numero maggiore di 5 (in minuti) e salva il file.
1. Nella console di amministrazione, passa alla pagina Importa ed esporta file di configurazione.
1. Immettere il percorso del file config.xml modificato oppure fare clic su Sfoglia per individuarlo.
1. Fai clic su **Importa** per caricare il file config.xml modificato, quindi fai clic su **OK**.
