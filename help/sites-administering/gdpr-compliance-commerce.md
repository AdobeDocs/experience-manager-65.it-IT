---
title: AEM Commerce - Preparazione all’RGPD
seo-title: AEM Commerce - GDPR Readiness
description: "Commercio AEM - Preparazione al RGPD"
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# AEM Commerce - Preparazione all’RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come RGPD, CCPA, ecc.

Il Regolamento generale sulla protezione dei dati dell&#39;Unione europea sui diritti relativi alla privacy dei dati entra in vigore a maggio 2018. Per ulteriori informazioni, consulta [Pagina RGPD nell’Adobe Privacy Center](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Vedi [Preparazione AEM RGPD](/help/managing/data-protection-and-privacy.md) per ulteriori dettagli.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Nelle nostre integrazioni Commerce predefinite, AEM è il livello di esperienza, consuma servizi e invia nuovamente dati alla piattaforma di e-commerce del cliente che viene eseguita in modalità headless.

Per alcune piattaforme di e-commerce, memorizziamo le informazioni sul profilo ( `/home/users`) e token di e-commerce (per accedere alla piattaforma commerce) in AEM. Per questi casi d&#39;uso, leggere [Gestione delle richieste RGPD per la piattaforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestione delle richieste RGPD per AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Per l’integrazione con Salesforce Commerce Cloud, AEM Commerce non memorizza informazioni rilevanti per il RGPD. Inoltrare la richiesta al [Salesforce Cloud](https://documentation.demandware.com/).

Per le integrazioni hybris e IBM WebSphere, sono presenti alcuni dati in AEM. Utilizza la [Istruzioni AEM Platform RGPD](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considera queste domande:

1. **Dove vengono memorizzati o utilizzati i miei dati?** Le informazioni del profilo utente memorizzate nella cache, come nome, identificatore utente di e-commerce, token, password, dati dell’indirizzo e così via, vengono visualizzate da AEM.
1. **Con chi condivido i dati RGPD coperti?** Eventuali aggiornamenti dei dati relativi al RGPD in AEM Commerce non vengono memorizzati (ad eccezione delle informazioni di profilo rilevanti, come indicato in precedenza) ma vengono trasmessi nuovamente alla piattaforma di e-commerce.
1. **Come eliminare i dati utente**? Elimina il profilo utente in AEM e richiama l’eliminazione dell’utente sulla piattaforma commerce.

>[!NOTE]
>
>Dai un&#39;occhiata al [wiki ibrido](https://wiki.hybris.com/) o [Documentazione di Websphere Commerce](https://www-01.ibm.com/support/docview.wss?uid=swg27036450) se necessario.
