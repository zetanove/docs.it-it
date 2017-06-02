---
title: "Procedura: Impostare criteri di cache basati sulla posizione per un&#39;applicazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "definizione esplicita del comportamento della cache"
  - "criteri di cache basati sulla posizione"
  - "cache locale"
  - "criteri di cache per le richieste"
  - "cache [.NET Framework], criteri basati sulla posizione"
ms.assetid: 683bb88e-3411-4f46-9686-3411b6ba511c
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Procedura: Impostare criteri di cache basati sulla posizione per un&#39;applicazione
Ai criteri della cache basati sul percorso consentono un'applicazione definire in modo esplicito il comportamento di memorizzazione nella cache in base al percorso della risorsa richiesta.  In questo argomento viene illustrato impostare i criteri della cache a livello di codice.  Per informazioni sull'impostazione di criteri per un'applicazione utilizzando file di configurazione, vedere [Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md).  
  
### Per impostare criteri della cache basati sul percorso per un'applicazione  
  
1.  Creare un oggetto <xref:System.Net.Cache.HttpRequestCachePolicy> o <xref:System.Net.Cache.RequestCachePolicy>.  
  
2.  Impostare l'oggetto di criteri come predefinito per il dominio applicazione.  
  
### Per impostare criteri che accettano ha richiesto le risorse da una cache  
  
-   Creare criteri che hanno dispongono delle risorse richieste da una cache se disponibili in caso contrario, invia richieste al server, impostando il livello della cache in <xref:System.Net.Cache.HttpRequestCacheLevel>.  Una richiesta può essere eseguita da qualsiasi cache tra client e server, incluse le cache remoti.  
  
    ```csharp  
    public static void UseCacheIfAvailable()  
    {  
        HttpRequestCachePolicy policy = new HttpRequestCachePolicy  
            (HttpRequestCacheLevel.CacheIfAvailable);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
  
    ```  
  
    ```vb  
    Public Shared Sub UseCacheIfAvailable()  
        Dim policy As New HttpRequestCachePolicy _  
             (HttpRequestCacheLevel.CacheIfAvailable)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### Per impostare criteri che impediscono qualsiasi cache da fornire le risorse  
  
-   Creare criteri che impediscono qualsiasi cache da fornire le risorse richieste impostando il livello della cache in <xref:System.Net.Cache.HttpRequestCacheLevel>.  Questo livello di criteri rimuove la risorsa dalla cache locale se è presente e indica alla cache remoti che devono essere rimosse anche la risorsa.  
  
    ```csharp  
    public static void DoNotUseCache()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.NoCacheNoStore);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub DoNotUseCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.NoCacheNoStore)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### Per impostare criteri che restituiscono le risorse necessarie solo se sono nella cache locale  
  
-   Creare criteri che restituiscono le risorse necessarie solo se sono nella cache locale impostando il livello della cache in <xref:System.Net.Cache.HttpRequestCacheLevel>.  Se la risorsa richiesta non è presente, viene generata un'eccezione <xref:System.Net.WebException> viene generata un'eccezione.  
  
    ```csharp  
    public static void OnlyUseCache()  
    {  
        HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.CacheOnly);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub OnlyUseCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.CacheOnly)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### Per impostare criteri che impediscono la cache locale da fornire le risorse  
  
-   Creare criteri che impediscono la cache locale da fornire le risorse richieste impostando il livello della cache in <xref:System.Net.Cache.HttpRequestCacheLevel>.  Se la risorsa richiesta è in una cache intermedio e correttamente verranno riconvalidati, la cache intermedio può fornire la risorsa richiesta.  
  
    ```csharp  
    public static void DoNotUseLocalCache()  
    {  
     HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.Refresh);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub DoNotUseLocalCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Refresh)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### Per impostare criteri che impediscono qualsiasi cache da fornire le risorse richieste  
  
-   Creare criteri che impediscono qualsiasi cache da fornire le risorse richieste impostando il livello della cache in <xref:System.Net.Cache.HttpRequestCacheLevel>.  La risorsa restituita dal server può essere memorizzata nella cache.  
  
    ```csharp  
    public static void SendToServer()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.Reload);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub SendToServer()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Reload)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### Per impostare criteri che consentono qualsiasi la cache per assistere ha richiesto le risorse se la risorsa nel server non è più recente della copia memorizzata nella cache  
  
-   Creare criteri che consentono qualsiasi cache alle risorse richieste a se la risorsa nel server non è più recente della copia memorizzata nella cache impostando il livello della cache in <xref:System.Net.Cache.HttpRequestCacheLevel>.  
  
    ```csharp  
    public static void CheckServer()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy  
             (HttpRequestCacheLevel.Revalidate);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub CheckServer()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Revalidate)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)   
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)