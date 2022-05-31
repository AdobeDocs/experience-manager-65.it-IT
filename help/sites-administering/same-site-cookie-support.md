---
title: Supporto per cookie per lo stesso sito per AEM 6.5
description: Supporto per cookie per lo stesso sito per AEM 6.5
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: f7a4907ca6ce8ecaff9ef1fdf99ec0951ff497e0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 55%

---

# Supporto per cookie per lo stesso sito per AEM 6.5 {#same-site-cookie-support-for-aem-65}

A partire dalla versione 80, Chrome, e successivamente Safari, hanno introdotto un nuovo modello per la sicurezza dei cookie. Questa modalità è progettata per introdurre controlli di sicurezza sulla disponibilità di cookie per siti di terze parti, tramite un&#39;impostazione denominata `SameSite`. Per informazioni più dettagliate, consulta questo [articolo](https://web.dev/samesite-cookies-explained/).

Il valore predefinito di questa impostazione (`SameSite=Lax`) potrebbe impedire il funzionamento dell’autenticazione tra istanze o servizi AEM. Questo perché i domini o le strutture URL di questi servizi potrebbero non rientrare nei vincoli di questo criterio dei cookie.

Per aggirare questo problema, è necessario impostare il `SameSite` attributo cookie a `None` per il token di accesso.

>[!CAUTION]
>
>La `SameSite=None` viene applicata solo se il protocollo è protetto (HTTPS).
>
>Se il protocollo non è protetto (HTTP), l&#39;impostazione viene ignorata e il server visualizza questo messaggio WARN:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Puoi aggiungere l’impostazione seguendo i passaggi seguenti:

1. Passa alla console Web all’indirizzo `http://serveraddress:serverport/system/console/configMgr`
1. Cerca e fai clic sull’**handler di autenticazione token di Adobe Granite**
1. Imposta **l’attributo SameSite per il cookie token di accesso** su `None`, come illustrato nell’immagine seguente
   ![samesite](assets/samesite1.png)
1. Fai clic su Salva
1. Quando questa impostazione è aggiornata e gli utenti vengono disconnessi e di nuovo connessi, i cookie `login-token` avranno l’attributo `None` impostato e verranno inclusi nelle richieste cross-site.
