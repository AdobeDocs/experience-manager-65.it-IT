---
title: Configurare l’autenticazione estesa dal browser esterno per la sicurezza dei documenti
description: Scopri come configurare l’autenticazione del browser esterno in modo che gli utenti possano eseguire l’autenticazione per i documenti PDF protetti tramite policy in Acrobat o Reader utilizzando il browser web predefinito del sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 89a07256cd5bb850aac19565ad86273322fa1f31
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 1%

---

# Configurare l’autenticazione estesa dal browser esterno per la sicurezza dei documenti {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> Assicurati di disporre dei privilegi di amministratore per accedere alla console di amministrazione di AEM Forms.

L’autenticazione estesa da un browser esterno consente agli utenti di eseguire l’autenticazione per i documenti PDF protetti tramite policy utilizzando il browser web predefinito del sistema (ad esempio Microsoft Edge o Google Chrome) invece del controllo del browser incorporato all’interno di Acrobat o Reader. Ciò consente di utilizzare metodi di autenticazione moderni, come PassKey, l’autenticazione biometrica e altre funzioni del provider di identità (IDP) che richiedono un browser moderno.

Quando questa opzione è attivata, l’apertura di un documento protetto tramite policy in Acrobat o Reader avvia la pagina di accesso IDP nel browser predefinito dell’utente. Dopo l’autenticazione, l’utente viene automaticamente reindirizzato ad Acrobat o Reader e il documento viene sbloccato.

## Prerequisiti {#prerequisites}

Prima di configurare l’autenticazione esterna del browser, verifica che siano soddisfatti i seguenti requisiti:

* AEM Forms 6.5 su JEE con Service Pack 6.5.25.0 distribuito o Service Pack 6.5.24.0 con la patch hotfix JEE applicabile installata su un server applicazioni supportato (JBoss, WebLogic o WebSphere). Consulta [Collegamenti di distribuzione software per AEM Forms JEE Hotfix2 6.5.24.0](#software-distribution-links).
* Autenticazione estesa (autenticazione di terze parti) già abilitata e funzionante con un IDP. Vedere [Impostazioni di configurazione del server](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings) e [Aggiungere il provider di autenticazione estesa](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider).
* Adobe Acrobat Pro o Adobe Acrobat Reader (a 64 bit) installato sul PC client Windows con l&#39;aggiornamento più recente.

>[!NOTE]
>
> L’autenticazione tramite browser esterno richiede una versione supportata di Adobe Acrobat o Adobe Acrobat Reader sul client. Consulta [Note sulla versione di Acrobat (Continuous Track, marzo 2026)](https://www.adobe.com/devnet-docs/acrobatetk/tools/ReleaseNotesDC/continuous/dccontinuousmarch2026.html#dccontinuousmarchtwentytwentysix) per i dettagli e gli aggiornamenti della versione.

### Collegamenti di distribuzione software per AEM Forms JEE Hotfix2 6.5.24.0 {#software-distribution-links}

L&#39;autenticazione del browser esterno è disponibile in AEM Forms su JEE Service Pack 6.5.25.0 e versioni successive.

Se si utilizza AEM Forms con JEE Service Pack 6.5.24.0 o versioni precedenti, eseguire una delle operazioni seguenti:

* Effettua l&#39;aggiornamento a [AEM Forms su JEE Service Pack 6.5.25.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip).
* Installa la patch 6.5.24.0 dell&#39;hotfix JEE AEM Forms per il server applicazioni e la piattaforma utilizzando i collegamenti riportati di seguito.

Scarica e installa la patch AEM Forms JEE Hotfix 6.5.24.0 per la tua piattaforma da [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html):

**JBoss**

* Windows: [Hotfix per AEM Service Pack 6.5.24.0 su Windows per il server JEE JBoss](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-jboss.zip)
* Linux: [Hotfix per AEM Service Pack 6.5.24.0 su Linux per il server JEE JBoss](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-jboss.tar.gz)

**WebSphere**

* Windows: [Hotfix per AEM Service Pack 6.5.24.0 su Windows per il server WebSphere JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-websphere.zip)
* Linux: [Hotfix per AEM Service Pack 6.5.24.0 su Linux per il server WebSphere JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-websphere.tar.gz)

**WebLogic**

* Windows: [Hotfix per AEM Service Pack 6.5.24.0 su Windows per il server WebLogic JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-weblogic.zip)
* Linux: [Hotfix per AEM Service Pack 6.5.24.0 su Linux per il server WebLogic JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-weblogic.tar.gz)

Per istruzioni sull&#39;installazione, vedere [Installare una patch JEE](/help/release-notes/jee-patch-installer-65.md).

## Abilita autenticazione browser esterna {#enable-external-browser-authentication}

Questo video mostra come abilitare l’autenticazione esterna del browser sul server AEM Forms Document Security.

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. Nella console di amministrazione, fai clic su **Servizi** > **Document Security** > **Configurazione** > **Configurazione server**.
1. Individua la sezione **Consenti autenticazione estesa dal browser esterno per le applicazioni client Adobe**.
1. Seleziona la casella di controllo per ogni piattaforma client Adobe che desideri abilitare:
   * **Adobe Acrobat e Reader (64 bit) - Desktop**
   * **Adobe Acrobat Reader (32 bit) - Desktop**
1. Fai clic su **OK**.

Per la descrizione delle impostazioni del server, vedere [Impostazioni di configurazione del server](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings).

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## Verifica {#verification}

Questo video mostra come verificare l’autenticazione del browser esterno: apri un PDF protetto tramite policy in Acrobat, accedi con il browser predefinito e conferma che il documento si sblocca dopo l’autenticazione.

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. Crea un documento PDF protetto tramite policy utilizzando il server di Document Security.
1. Su un computer client Windows, apri il PDF protetto in Acrobat Pro o Acrobat Reader.
1. In Acrobat viene visualizzata una finestra di dialogo per il consenso. Fai clic su **Accedi**.
1. Verifica che venga aperto il browser predefinito del sistema con la pagina di accesso IDP.
1. Autenticazione completa.
1. Verificare che il documento protetto venga aperto correttamente.

## Risoluzione di problemi {#troubleshooting}

### Viene aperto il browser incorporato al posto del browser di sistema {#embedded-browser-opens-instead-of-system-browser}

* Verificare che nel server sia abilitata l&#39;autenticazione del browser esterno. Vedere [Abilitare l&#39;autenticazione del browser esterno](#enable-external-browser-authentication).
* Conferma che la versione di Acrobat o Reader supporti questa funzione. Vedi [Acrobat](#acrobat).

### L&#39;autenticazione viene eseguita correttamente nel browser, ma il documento non si sblocca {#authentication-succeeds-but-document-does-not-unlock}

* Assicurati che Acrobat o Reader sia in esecuzione e non sia bloccato dal firewall o da un software di sicurezza.
* Se il problema persiste, reinstallare o ripristinare l’installazione di Acrobat o Reader per ripristinare la registrazione del gestore del protocollo.

### In Acrobat viene visualizzato il messaggio &quot;Non è stato possibile accedere&quot; {#we-couldnt-sign-you-in-message}

* L&#39;utente potrebbe aver impiegato troppo tempo per completare l&#39;autenticazione. Riprova.
* Verifica la connettività di rete tra il browser e il server AEM Forms.

### L’opzione di autenticazione non viene visualizzata nella pagina di accesso {#authentication-option-does-not-appear}

* I metodi e le opzioni di autenticazione sono configurati dall’IDP, non da AEM Forms o Acrobat. Verificare che l&#39;IDP supporti il metodo di autenticazione desiderato.
* Verifica che la pagina di accesso venga caricata nel browser di sistema (non nel browser incorporato).
