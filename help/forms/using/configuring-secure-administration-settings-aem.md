---
title: Configurazione delle impostazioni di amministrazione protetta per  AEM Forms su JEE
seo-title: Configurazione delle impostazioni di amministrazione protetta per  AEM Forms su JEE
description: Scoprite come amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono richiesti in un ambiente di produzione  AEM Forms su JEE.
seo-description: Scoprite come amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono richiesti in un ambiente di produzione  AEM Forms su JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---


# Configurazione delle impostazioni di amministrazione protetta per  AEM Forms su JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Scoprite come amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono richiesti in un ambiente di produzione  AEM Forms su JEE.

In genere, gli sviluppatori non utilizzano l&#39;ambiente di produzione per creare e testare le proprie applicazioni. Pertanto, è necessario amministrare gli account utente e i servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono richiesti in un ambiente di produzione.

Questo articolo descrive i metodi per ridurre la superficie di attacco globale attraverso le opzioni di amministrazione fornite da AEM Forms su JEE.

## Disattivazione dell&#39;accesso remoto non essenziale ai servizi {#disabling-non-essential-remote-access-to-services}

Dopo aver installato e configurato  AEM Forms su JEE, molti servizi sono disponibili per la chiamata remota attraverso SOAP e Enterprise JavaBeans™ (EJB). Il termine remoto, in questo caso, si riferisce a qualsiasi chiamante che dispone dell&#39;accesso di rete alle porte SOAP, EJB o Action Message Format (AMF) per il server dell&#39;applicazione.

Sebbene l&#39;AEM Forms  sui servizi JEE richieda il passaggio di credenziali valide per un chiamante autorizzato, è consigliabile consentire l&#39;accesso remoto solo ai servizi che devono essere accessibili in remoto. Per ottenere un&#39;accessibilità limitata, è necessario ridurre al minimo il set di servizi accessibili in remoto per un sistema funzionante e quindi abilitare la chiamata in remoto per i servizi aggiuntivi necessari.

 AEM Forms sui servizi JEE richiede sempre almeno l&#39;accesso SOAP. Tali servizi sono in genere richiesti per l&#39;utilizzo da parte di Workbench ma includono anche i servizi richiamati dall&#39;applicazione Web Workspace.

Completa questa procedura utilizzando la pagina Web Applicazioni e servizi nella console di amministrazione:

1. Accedete alla console di amministrazione digitando il seguente URL in un browser Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Fare clic su **Servizi > Applicazioni e servizi > Preferenze**.
1. Impostate Preferenze per visualizzare fino a 200 servizi e endpoint sulla stessa pagina.
1. Fare clic su **Servizi** > **Applicazioni e servizi** > **Endpoint Management**.
1. Selezionare **EJB** dall&#39;elenco **Provider**, quindi fare clic su **Filtro**.
1. Per disattivare tutti gli endpoint EJB, selezionate la casella di controllo accanto a ciascuno nell&#39;elenco e fate clic su **Disattiva**.
1. Fare clic su **Next** e ripetere il passaggio precedente per tutti gli endpoint EJB. Prima di disattivare gli endpoint, accertatevi che EJB sia elencato nella colonna Provider.
1. Selezionare **SOAP** dall&#39;elenco **Provider**, quindi fare clic su **Filtro**.
1. Per rimuovere gli endpoint SOAP, selezionare la casella di controllo accanto a ciascuno nell&#39;elenco e fare clic su **Remove**. Non rimuovere i seguenti endpoint:

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
   * WorkspaceSingleSignOn
   * ApplicationManager

1. Fare clic su **Next** e ripetere il passaggio precedente per gli endpoint SOAP che non si trovano nell&#39;elenco precedente. Prima di rimuovere gli endpoint, verificate che SOAP sia elencato nella colonna Provider.

## Disattivazione dell&#39;accesso anonimo non essenziale ai servizi {#disabling-non-essential-anonymous-access-to-services}

Alcuni servizi server moduli consentono chiamate non autenticate (anonime) per alcune operazioni. Ciò significa che una o più operazioni esposte dal servizio possono essere invocate come qualsiasi utente autenticato o come nessun utente autenticato.

1. Accedete alla console di amministrazione digitando il seguente URL in un browser Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Fare clic su **Servizi > Applicazioni e servizi > Gestione dei servizi**.
1. Fare clic sul nome del servizio che si desidera disattivare (ad esempio, AuthenticationManagerService).
1. Fare clic sulla scheda **Protezione**, deselezionare **Accesso anonimo consentito** e fare clic su **Salva**.
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
   * TaskManagerConnector
   * TaskManagerQueryService
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Se si desidera esporre uno di questi servizi per la chiamata remota, è consigliabile disattivare l&#39;accesso anonimo per questi servizi. In caso contrario, qualsiasi chiamante con accesso di rete a questo servizio potrebbe richiamare il servizio senza passare credenziali valide.

   L&#39;accesso anonimo deve essere disattivato per tutti i servizi non necessari. Molti servizi interni richiedono l&#39;abilitazione dell&#39;autenticazione anonima perché devono essere richiamati da qualsiasi utente potenzialmente presente nel sistema senza essere preautorizzati.

## Modifica del timeout globale predefinito {#changing-the-default-global-time-out}

Gli utenti finali possono eseguire l&#39;autenticazione per  AEM Forms tramite Workbench,  applicazioni Web AEM Forms o applicazioni personalizzate che richiamano  servizi server AEM Forms. Un’impostazione globale relativa al timeout viene utilizzata per specificare per quanto tempo tali utenti possono interagire con  AEM Forms (utilizzando un’associazione basata su SAML) prima che siano costretti a eseguire nuovamente l’autenticazione. L’impostazione predefinita è due ore. In un ambiente di produzione, il tempo deve essere ridotto al numero minimo di minuti accettabile.

### Limite minimo di tempo per la riautenticazione {#minimize-reauthentication-time-limit}

1. Accedete alla console di amministrazione digitando il seguente URL in un browser Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Fare clic su **Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione**.
1. Fare clic su **Esporta** per generare un file config.xml con le impostazioni AEM Forms  esistenti.
1. Aprite il file XML in un editor e individuate la voce seguente:

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. Modificate il valore in un numero qualsiasi maggiore di 5 (in minuti) e salvate il file.
1. Nella console di amministrazione, andate alla pagina Importa ed esporta file di configurazione.
1. Inserite il percorso del file config.xml modificato oppure fate clic su Sfoglia per individuarlo.
1. Fare clic su **Importa** per caricare il file config.xml modificato, quindi fare clic su **OK**.

