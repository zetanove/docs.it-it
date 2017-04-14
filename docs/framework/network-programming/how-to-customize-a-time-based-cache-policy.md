---
title: "Procedura: Personalizzare criteri di cache basati sull&#39;ora | Microsoft Docs"
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
  - "criteri di cache basati sull'ora"
  - "personalizzazione di criteri di cache basati sull'ora"
  - "cache [.NET Framework], criteri basati sull'ora"
ms.assetid: 8d84f936-2376-4356-9264-03162e0f9279
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# Procedura: Personalizzare criteri di cache basati sull&#39;ora
Nel creare criteri della cache basati sull'ora, è possibile personalizzare il comportamento di memorizzazione nella cache specificando i valori per la validità massima, la validità minima, la rancidità massima, o la data di sincronizzazione della cache.  L'oggetto <xref:System.Net.Cache.HttpRequestCachePolicy> fornisce molti costruttori che consentono di specificare le combinazioni valide di questi valori.  
  
### Per creare criteri della cache basati sull'ora che utilizzano una data di sincronizzazione della cache  
  
-   Creare criteri della cache basati sull'ora che utilizzano una data di sincronizzazione della cache passando un oggetto <xref:System.DateTime> al costruttore <xref:System.Net.Cache.HttpRequestCachePolicy>.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateLastSyncPolicy(DateTime when)  
    {  
        HttpRequestCachePolicy policy =   
            new HttpRequestCachePolicy(when);  
        Console.WriteLine("When: {0}", when);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateLastSyncPolicy([when] As DateTime) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy([when])  
        Console.WriteLine("When: {0}", [when])  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 L'output è simile al seguente:  
  
```  
When: 1/14/2004 8:07:30 AM  
Level:Default CacheSyncDate:1/14/2004 8:07:30 AM  
```  
  
### Per creare criteri della cache basati sull'ora basati su validità minima  
  
-   Creare criteri della cache basati sull'ora basati su validità minima specificando <xref:System.Net.Cache.HttpCacheAgeControl> come valore del parametro `cacheAgeControl` e passando un oggetto <xref:System.TimeSpan> al costruttore <xref:System.Net.Cache.HttpRequestCachePolicy>.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateMinFreshPolicy(TimeSpan span)  
    {  
        HttpRequestCachePolicy policy =   
            new HttpRequestCachePolicy(HttpCacheAgeControl.MinFresh, span);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateMinFreshPolicy(span As TimeSpan) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy(HttpCacheAgeControl.MinFresh, span)  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 Per la chiamata seguente:  
  
```  
CreateMinFreshPolicy(new TimeSpan(1,0,0));  
```  
  
```  
Level:Default MinFresh:3600  
  
```  
  
### Per creare criteri della cache basati sull'ora basati su validità minima e la validità massima  
  
-   Creare criteri della cache basati sull'ora basati su validità minima e la validità massima specificando <xref:System.Net.Cache.HttpCacheAgeControl> come valore del parametro `cacheAgeControl` e passando due oggetti <xref:System.TimeSpan> al costruttore <xref:System.Net.Cache.HttpRequestCachePolicy>, uno per specificare la validità massima per le risorse e un secondo specificare la validità minima consentita per un oggetto restituito dalla cache.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateFreshAndAgePolicy(TimeSpan freshMinimum, TimeSpan ageMaximum)  
    {  
        HttpRequestCachePolicy policy =   
        new HttpRequestCachePolicy(HttpCacheAgeControl.MaxAgeAndMinFresh, ageMaximum, freshMinimum);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateFreshAndAgePolicy(freshMinimum As TimeSpan, ageMaximum As TimeSpan) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy(HttpCacheAgeControl.MaxAgeAndMinFresh, ageMaximum, freshMinimum)  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 Per la chiamata seguente:  
  
```  
CreateFreshAndAgePolicy(new TimeSpan(5,0,0), new TimeSpan(10,0,0));  
```  
  
```  
Level:Default MaxAge:36000 MinFresh:18000  
```  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)   
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)