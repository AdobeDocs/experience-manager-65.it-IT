---
title: Sicurezza
seo-title: Sicurezza
description: Application Security inizia durante la fase di sviluppo
seo-description: Application Security inizia durante la fase di sviluppo
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Sicurezza{#security}

Application Security inizia durante la fase di sviluppo. Adobe consiglia di applicare le procedure ottimali di protezione seguenti.

## Usa sessione richiesta {#use-request-session}

In base al principio dei privilegi minimi, Adobe consiglia di utilizzare la sessione associata alla richiesta dell&#39;utente e al controllo di accesso adeguato per ogni accesso al repository.

## Protezione contro gli script tra siti (XSS) {#protect-against-cross-site-scripting-xss}

Lo scripting tra siti (XSS) consente agli aggressori di inserire codice nelle pagine Web visualizzate da altri utenti. Questa vulnerabilità di sicurezza può essere sfruttata da utenti Web malintenzionati per aggirare i controlli di accesso.

AEM applica il principio di filtrare tutti i contenuti forniti dall’utente al momento dell’output. La prevenzione di XSS viene data la massima priorità sia durante lo sviluppo che durante i test.

Il meccanismo di protezione XSS fornito da AEM si basa sulla libreria [Java](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) AntiSamy fornita da [OWASP (Open Web Application Security Project)](https://www.owasp.org/). La configurazione predefinita di AntiSamy si trova in

`/libs/cq/xssprotection/config.xml`

È importante adattare questa configurazione alle proprie esigenze di sicurezza sovrapponendo il file di configurazione. La documentazione [ufficiale](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) AntiSamy ti fornirà tutte le informazioni necessarie per implementare i tuoi requisiti di sicurezza.

>[!NOTE]
>
>È consigliabile accedere sempre all&#39;API di protezione XSS utilizzando [XSSAPI fornito da AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Inoltre, un firewall per applicazioni Web, come [mod_security per Apache](https://www.modsecurity.org), può fornire un controllo centrale affidabile sulla sicurezza dell&#39;ambiente di distribuzione e proteggere contro attacchi di script tra siti non rilevati in precedenza.

## Accesso alle informazioni sui servizi cloud {#access-to-cloud-service-information}

>[!NOTE]
>
>Gli ACL per le informazioni sul servizio cloud e le impostazioni OSGi necessarie per proteggere l&#39;istanza sono automatizzati nell&#39;ambito della modalità [](/help/sites-administering/production-ready.md)Production Ready. Anche se questo significa che non è necessario apportare manualmente le modifiche alla configurazione, è comunque consigliabile rivederle prima di iniziare a utilizzare la distribuzione.

Quando [integrate l&#39;istanza AEM con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) utilizzate le configurazioni [dei servizi](/help/sites-developing/extending-cloud-config.md)Cloud. Le informazioni su queste configurazioni, insieme alle eventuali statistiche raccolte, sono memorizzate nella directory archivio. Se utilizzate questa funzionalità, è consigliabile verificare se la protezione predefinita di queste informazioni corrisponde ai requisiti.

Il modulo di supporto del servizio Web scrive le statistiche e le informazioni di configurazione in:

`/etc/cloudservices`

Con le autorizzazioni predefinite:

* Ambiente di authoring: `read` for `contributors`

* Ambiente di pubblicazione: `read` for `everyone`

## Protezione da attacchi di contraffazione di richieste intersito {#protect-against-cross-site-request-forgery-attacks}

Per ulteriori informazioni sui meccanismi di sicurezza utilizzati da AEM per attenuare gli attacchi CSRF, consulta la sezione Filtro [Sling Referrer nella lista di controllo della sicurezza e la documentazione](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) sul quadro di protezione [](/help/sites-developing/csrf-protection.md)CSRF.