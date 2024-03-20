---
title: Configurazione delle impostazioni di amministrazione protetta per AEM Forms su JEE
description: Scopri come amministrare account utente e servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono necessari in un ambiente di produzione di AEM Forms su JEE.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Configurazione delle impostazioni di amministrazione protetta per AEM Forms su JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Scopri come amministrare account utente e servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono necessari in un ambiente di produzione di AEM Forms su JEE.

In genere, gli sviluppatori non utilizzano l’ambiente di produzione per generare e testare le applicazioni. Pertanto, devi amministrare account utente e servizi che, sebbene richiesti in un ambiente di sviluppo privato, non sono necessari in un ambiente di produzione.

Questo articolo descrive i metodi per ridurre la superficie di attacco complessiva tramite le opzioni di amministrazione fornite da AEM Forms su JEE.

## Disattivazione dell&#39;accesso remoto non essenziale ai servizi {#disabling-non-essential-remote-access-to-services}

Dopo l’installazione e la configurazione di AEM Forms su JEE, molti servizi sono disponibili per la chiamata remota tramite SOAP e Enterprise JavaBeans™ (EJB). Il termine remoto, in questo caso, si riferisce a qualsiasi chiamante che dispone di accesso di rete alle porte SOAP, EJB o Action Message Format (AMF) per il server applicazioni.

Sebbene i servizi AEM Forms su JEE richiedano il passaggio di credenziali valide per un chiamante autorizzato, è necessario consentire solo l’accesso remoto ai servizi che devono essere accessibili in remoto. Per ottenere un&#39;accessibilità limitata, è necessario ridurre al minimo l&#39;insieme di servizi accessibili in remoto per un sistema funzionante e quindi abilitare la chiamata remota per i servizi aggiuntivi necessari.

I servizi AEM Forms su JEE richiedono sempre almeno l’accesso SOAP. Questi servizi sono in genere necessari per l’utilizzo da Workbench, ma includono anche i servizi richiamati dall’applicazione web Workspace.

Eseguire questa procedura utilizzando la pagina Web Applicazioni e servizi di Administration Console:

1. Accedi ad Administration Console e digita il seguente URL in un browser web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clic **Servizi > Applicazioni e servizi > Preferenze**.
1. Imposta le Preferenze per visualizzare fino a 200 servizi ed endpoint sulla stessa pagina.
1. Clic **Servizi** > **Applicazioni e servizi** > **Gestione degli endpoint**.
1. Seleziona **EJB** dal **Provider** e quindi fare clic su **Filtro**.
1. Per disattivare tutti gli endpoint EJB, selezionare la casella di controllo accanto a ciascuno degli endpoint nell&#39;elenco e fare clic su **Disattiva**.
1. Clic **Successivo** e ripetere il passaggio precedente per tutti gli endpoint EJB. Prima di disabilitare gli endpoint, accertati che l’EJB sia elencato nella colonna Provider.
1. Seleziona **SOAP** dal **Provider** e quindi fare clic su **Filtro**.
1. Per rimuovere gli endpoint SOAP, selezionare la casella di controllo accanto a ciascuno degli endpoint nell&#39;elenco e fare clic su **Rimuovi**. Non rimuovere i seguenti endpoint:

   * AuthenticationManagerService
   * DirectoryManagerService
   * Gestione processo
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * ServizioArchivio
   * ServizioGestioneAttività
   * TaskQueueManager
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. Clic **Successivo** e ripetere il passaggio precedente per gli endpoint SOAP non inclusi nell&#39;elenco precedente. Prima di rimuovere gli endpoint, verificare che SOAP sia elencato nella colonna Provider.

## Disabilitazione dell’accesso anonimo non essenziale ai servizi {#disabling-non-essential-anonymous-access-to-services}

Alcuni servizi di Forms Server consentono chiamate non autenticate (anonime) per alcune operazioni. Ciò significa che una o più operazioni esposte dal servizio possono essere richiamate come qualsiasi utente autenticato o come nessun utente autenticato.

1. Accedi alla console di amministrazione e digita il seguente URL in un browser web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clic **Servizi > Applicazioni e servizi > Gestione servizi**.
1. Fare clic sul nome del servizio che si desidera disabilitare, ad esempio AuthenticationManagerService.
1. Fai clic su **Scheda Sicurezza**, deseleziona **Accesso anonimo consentito** e fai clic su **Salva**.
1. Completare i passaggi 3 e 4 per i seguenti servizi:

   * AuthenticationManagerService
   * EJB
   * E-mail
   * Gestione processo
   * WatchedFolder
   * UsermanagerUtilService
   * Remoting
   * ServizioProviderArchivio
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * ServizioGestioneAttività
   * ConnettoreGestioneAttività
   * TaskManagerQueryService
   * TaskQueueManager
   * GestioneEndpointAttività
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Se si intende esporre uno di questi servizi per la chiamata remota, è consigliabile anche disabilitare l&#39;accesso anonimo per questi servizi. In caso contrario, qualsiasi chiamante con accesso di rete al servizio potrebbe richiamare il servizio senza passare credenziali valide.

   L’accesso anonimo deve essere disabilitato per tutti i servizi non necessari. Molti servizi interni richiedono l&#39;autenticazione anonima perché devono essere richiamati da qualsiasi utente del sistema senza essere pre-autorizzati.

## Modifica del timeout globale predefinito {#changing-the-default-global-time-out}

Gli utenti finali possono eseguire l’autenticazione in AEM Forms tramite Workbench, applicazioni web AEM Forms o applicazioni personalizzate che richiamano i servizi server di AEM Forms. Viene utilizzata un’impostazione di timeout globale per specificare per quanto tempo tali utenti possono interagire con AEM Forms (utilizzando un’asserzione basata su SAML) prima di essere costretti a ripetere l’autenticazione. L’impostazione predefinita è due ore. In un ambiente di produzione, la quantità di tempo deve essere ridotta al numero minimo di minuti accettabile.

### Riduci al minimo il limite di tempo per la riautenticazione {#minimize-reauthentication-time-limit}

1. Accedi alla console di amministrazione e digita il seguente URL in un browser web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clic **Impostazioni > Gestione Utente > Configurazione > Importa Ed Esporta File Di Configurazione**.
1. Clic **Esporta** per produrre un file config.xml con le impostazioni AEM Forms esistenti.
1. Apri il file XML in un editor e individua la seguente voce:

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. Modifica il valore in un numero maggiore di 5 (in minuti) e salva il file.
1. Nella console di amministrazione, accedi alla pagina Importa ed esporta file di configurazione.
1. Immettere il percorso del file config.xml modificato o fare clic su Sfoglia per individuarlo.
1. Clic **Importa** per caricare il file config.xml modificato e quindi fare clic su **OK**.
