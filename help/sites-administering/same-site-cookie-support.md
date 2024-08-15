---
title: Supporto per i cookie dello stesso sito per AEM 6.5
description: Scopri il Supporto per i cookie SameSite per AEM 6.5.
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: db7830895c8a2d1b7228dc4780296d43f15776df
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 77%

---

# Supporto per i cookie dello stesso sito per AEM 6.5 {#same-site-cookie-support-for-aem-65}

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
