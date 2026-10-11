---
title: Supporto per i cookie SameSite per AEM 6.5
description: Scopri il supporto per i cookie SameSite per AEM 6.5.
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 78%
---
# Supporto per i cookie SameSite per AEM 6.5 {#same-site-cookie-support-for-aem-65}

A partire dalla versione 80, Chrome, e successivamente Safari, hanno introdotto un nuovo modello per la sicurezza dei cookie. Questa modalità è progettata per introdurre controlli di sicurezza riguardo alla disponibilità di cookie per i siti di terze parti, tramite un’impostazione denominata `SameSite`. Per informazioni più dettagliate, consulta questo articolo [web.dev - Spiegazione dei cookie SameSite](https://web.dev/samesite-cookies-explained/).

Il valore predefinito di questa impostazione (`SameSite=Lax`) potrebbe impedire il funzionamento dell’autenticazione tra istanze o servizi AEM. Questo perché i domini o le strutture URL di questi servizi potrebbero non rientrare nei vincoli di questo criterio dei cookie.

Per ovviare a questo problema, è necessario impostare l&#39;attributo cookie `SameSite` su `None` per il token di accesso.

>[!CAUTION]
>
>L’impostazione `SameSite=None` viene applicata solo se il protocollo è protetto (HTTPS).
>
>Se il protocollo non è protetto (HTTP), l’impostazione viene ignorata e il server persenta questo messaggio di avvertenza:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Per aggiungere l’impostazione, segui questi passaggi:

1. Passa alla console Web all’indirizzo `http://serveraddress:serverport/system/console/configMgr`
1. Cerca e fai clic sull’**handler di autenticazione token di Adobe Granite**
1. Imposta **l’attributo SameSite per il cookie token di accesso** su `None`, come illustrato nell’immagine seguente
   ![samesite](assets/samesite1.png)
1. Fai clic su Salva
1. Quando questa impostazione è aggiornata e gli utenti vengono disconnessi e di nuovo connessi, i cookie `login-token` avranno l’attributo `None` impostato e verranno inclusi nelle richieste cross-site.
