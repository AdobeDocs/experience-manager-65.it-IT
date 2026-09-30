---
title: Protezione
description: La sicurezza dell’applicazione inizia durante la fase di sviluppo
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%
---
# Protezione{#security}

La sicurezza dell’applicazione viene avviata durante la fase di sviluppo. Adobe consiglia di applicare le seguenti best practice per la sicurezza.

## Usa sessione di richiesta {#use-request-session}

In base al principio del privilegio minimo, Adobe consiglia di eseguire ogni accesso all’archivio utilizzando la sessione associata alla richiesta dell’utente e un controllo di accesso appropriato.

## Protezione da vulnerabilità cross-site scripting (XSS) {#protect-against-cross-site-scripting-xss}

Il cross-site scripting (XSS) consente agli aggressori di inserire codice nelle pagine web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti Web malintenzionati per aggirare i controlli di accesso.

AEM applica il principio di filtrare tutti i contenuti forniti dall’utente al momento dell’output. Prevenire l’XSS è data la massima priorità sia durante lo sviluppo che durante il test.

Il meccanismo di protezione XSS fornito da AEM si basa sulla [libreria Java™ AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fornita da [OWASP (The Open Web Application Security Project)](https://owasp.org/). La configurazione predefinita di AntiSamy è disponibile all&#39;indirizzo

`/libs/cq/xssprotection/config.xml`

È importante adattare questa configurazione alle proprie esigenze di sicurezza sovrapponendo il file di configurazione. La documentazione ufficiale di [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fornisce tutte le informazioni necessarie per implementare i requisiti di sicurezza.

>[!NOTE]
>
>Adobe consiglia di accedere sempre all&#39;API di protezione XSS utilizzando [XSSAPI fornita da AEM](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

Inoltre, un firewall dell&#39;applicazione Web, ad esempio [mod_security per Apache](https://www.modsecurity.org), può fornire un controllo centrale e affidabile sulla sicurezza dell&#39;ambiente di distribuzione e proteggere da attacchi di cross-site scripting non rilevati in precedenza.

## Accesso alle informazioni di Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Le ACL per le informazioni di Cloud Service e le impostazioni OSGi necessarie per proteggere l&#39;istanza sono automatizzate come parte della [modalità pronta per la produzione](/help/sites-administering/production-ready.md). Anche se questo significa che non è necessario modificare la configurazione manualmente, si consiglia comunque di rivederla prima di eseguire la distribuzione.

Quando [integri l&#39;istanza di AEM con Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md), utilizzi [Configurazioni Cloud Service](/help/sites-developing/extending-cloud-config.md). Le informazioni su queste configurazioni, insieme a eventuali statistiche raccolte, vengono memorizzate nell’archivio. Adobe consiglia di verificare che, se utilizzi questa funzionalità, la protezione predefinita di queste informazioni corrisponda ai tuoi requisiti.

Il modulo webservicesupport scrive statistiche e informazioni di configurazione in:

`/etc/cloudservices`

Con le autorizzazioni predefinite:

* Ambiente di authoring: `read` per `contributors`

* Ambiente di pubblicazione: `read` per `everyone`

## Protezione da attacchi di tipo Cross-Site Request Forgery {#protect-against-cross-site-request-forgery-attacks}

Per ulteriori informazioni sui meccanismi di sicurezza utilizzati da AEM per mitigare gli attacchi CSRF, consulta la sezione [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) dell&#39;elenco di controllo della sicurezza e la [documentazione del framework di protezione CSRF](/help/sites-developing/csrf-protection.md).
