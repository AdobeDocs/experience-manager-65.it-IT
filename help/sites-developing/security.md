---
title: Sicurezza
seo-title: Security
description: La sicurezza dell’applicazione inizia durante la fase di sviluppo
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Sicurezza{#security}

La sicurezza dell’applicazione viene avviata durante la fase di sviluppo. L’Adobe consiglia di applicare le seguenti best practice per la sicurezza.

## Usa sessione di richiesta {#use-request-session}

In base al principio del privilegio minimo, l’Adobe consiglia di eseguire ogni accesso all’archivio utilizzando la sessione associata alla richiesta dell’utente e un controllo di accesso appropriato.

## Protect contro il cross-site scripting (XSS) {#protect-against-cross-site-scripting-xss}

Il cross-site scripting (XSS) consente agli aggressori di inserire codice nelle pagine web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti Web malintenzionati per aggirare i controlli di accesso.

L&#39;AEM applica il principio di filtrare tutti i contenuti forniti dall&#39;utente al momento dell&#39;output. Prevenire l’XSS è data la massima priorità sia durante lo sviluppo che durante il test.

Il meccanismo di protezione XSS fornito dall’AEM si basa sulla [Libreria Java AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fornito da [OWASP (Progetto di protezione dell&#39;applicazione Web aperta)](https://www.owasp.org/). La configurazione predefinita di AntiSamy è disponibile all&#39;indirizzo

`/libs/cq/xssprotection/config.xml`

È importante adattare questa configurazione alle proprie esigenze di sicurezza sovrapponendo il file di configurazione. Il funzionario [Documentazione di AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ti fornirà tutte le informazioni necessarie per implementare i tuoi requisiti di sicurezza.

>[!NOTE]
>
>È consigliabile accedere sempre all’API di protezione XSS utilizzando [XSSAPI fornito dall’AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Inoltre, un firewall per le applicazioni web, ad esempio [mod_security per Apache](https://www.modsecurity.org), è in grado di fornire un controllo centrale e affidabile sulla sicurezza dell&#39;ambiente di distribuzione e di proteggere da attacchi di cross-site scripting non rilevati in precedenza.

## Accesso alle informazioni del Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>Le ACL per le informazioni di Cloud Service e le impostazioni OSGi necessarie per proteggere l’istanza vengono automatizzate come parte delle [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Anche se questo significa che non è necessario apportare manualmente le modifiche alla configurazione, si consiglia comunque di rivederle prima di eseguire la distribuzione.

Quando [integrare l’istanza AEM con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) utilizzi [Configurazioni Cloud Service](/help/sites-developing/extending-cloud-config.md). Le informazioni su queste configurazioni, insieme a eventuali statistiche raccolte, vengono memorizzate nell’archivio. Se si utilizza questa funzionalità, è consigliabile verificare se la protezione predefinita di queste informazioni soddisfa i requisiti.

Il modulo webservicesupport scrive statistiche e informazioni di configurazione in:

`/etc/cloudservices`

Con le autorizzazioni predefinite:

* Ambiente di authoring: `read` per `contributors`

* Ambiente di pubblicazione: `read` per `everyone`

## Protect contro gli attacchi di tipo Cross-Site Request Forgery {#protect-against-cross-site-request-forgery-attacks}

Per ulteriori informazioni sui meccanismi di sicurezza utilizzati dall&#39;AEM per mitigare gli attacchi CSRF, vedere [Filtro referrer Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) nell&#39;elenco di controllo della sicurezza e nella sezione [Documentazione di CSRF Protection Framework](/help/sites-developing/csrf-protection.md).
