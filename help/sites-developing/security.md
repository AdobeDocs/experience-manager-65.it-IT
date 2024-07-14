---
title: Sicurezza
description: La sicurezza dell’applicazione inizia durante la fase di sviluppo
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Sicurezza{#security}

La sicurezza dell’applicazione viene avviata durante la fase di sviluppo. L’Adobe consiglia di applicare le seguenti best practice per la sicurezza.

## Usa sessione di richiesta {#use-request-session}

In base al principio del privilegio minimo, l’Adobe consiglia di eseguire ogni accesso all’archivio utilizzando la sessione associata alla richiesta dell’utente e un controllo di accesso appropriato.

## Protect contro il cross-site scripting (XSS) {#protect-against-cross-site-scripting-xss}

Il cross-site scripting (XSS) consente agli aggressori di inserire codice nelle pagine web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti Web malintenzionati per aggirare i controlli di accesso.

L&#39;AEM applica il principio di filtrare tutti i contenuti forniti dall&#39;utente al momento dell&#39;output. Prevenire l’XSS è data la massima priorità sia durante lo sviluppo che durante il test.

Il meccanismo di protezione XSS fornito da AEM si basa sulla [libreria Java™ AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fornita da [OWASP (The Open Web Application Security Project)](https://owasp.org/). La configurazione predefinita di AntiSamy è disponibile all&#39;indirizzo

`/libs/cq/xssprotection/config.xml`

È importante adattare questa configurazione alle proprie esigenze di sicurezza sovrapponendo il file di configurazione. La documentazione ufficiale di [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fornisce tutte le informazioni necessarie per implementare i requisiti di sicurezza.

>[!NOTE]
>
>L&#39;Adobe consiglia di accedere sempre all&#39;API di protezione XSS utilizzando [XSSAPI fornita dall&#39;AEM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

Inoltre, un firewall dell&#39;applicazione Web, ad esempio [mod_security per Apache](https://www.modsecurity.org), può fornire un controllo centrale e affidabile sulla sicurezza dell&#39;ambiente di distribuzione e proteggere da attacchi di cross-site scripting non rilevati in precedenza.

## Accesso alle informazioni del Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Le ACL per le informazioni di Cloud Service e le impostazioni OSGi necessarie per proteggere l&#39;istanza sono automatizzate come parte della [modalità pronta per la produzione](/help/sites-administering/production-ready.md). Anche se questo significa che non è necessario modificare la configurazione manualmente, si consiglia comunque di rivederla prima di eseguire la distribuzione.

Quando [integri l&#39;istanza AEM con Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md), utilizzi [configurazioni di Cloud Service](/help/sites-developing/extending-cloud-config.md). Le informazioni su queste configurazioni, insieme a eventuali statistiche raccolte, vengono memorizzate nell’archivio. L&#39;Adobe consiglia, se si utilizza questa funzionalità, di verificare se la protezione predefinita di queste informazioni soddisfa i requisiti.

Il modulo webservicesupport scrive statistiche e informazioni di configurazione in:

`/etc/cloudservices`

Con le autorizzazioni predefinite:

* Ambiente di authoring: `read` per `contributors`

* Ambiente Publish: `read` per `everyone`

## Protect contro gli attacchi di tipo Cross-Site Request Forgery {#protect-against-cross-site-request-forgery-attacks}

Per ulteriori informazioni sui meccanismi di sicurezza utilizzati dall&#39;AEM per mitigare gli attacchi CSRF, consulta la sezione [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) dell&#39;elenco di controllo della sicurezza e la [documentazione del framework di protezione CSRF](/help/sites-developing/csrf-protection.md).
