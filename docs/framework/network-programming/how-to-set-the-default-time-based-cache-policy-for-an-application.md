---
title: "Procedura: Impostare criteri di cache predefiniti basati sull&#39;ora per un&#39;applicazione | Microsoft Docs"
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
  - "cache [.NET Framework], criteri basati sull'ora"
  - "criteri di cache basati sull'ora predefiniti"
ms.assetid: 6bfce066-a2e7-4add-a05e-85c12ec9f07f
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Procedura: Impostare criteri di cache predefiniti basati sull&#39;ora per un&#39;applicazione
Criteri della cache basati sull'ora predefiniti consentono a un'applicazione del comportamento della cache definito dalle intestazioni inviate con la risorsa memorizzata nella cache e il comportamento della cache definito in parti 13 e 14 dello standard RFC 2616, disponibile su [http:\/\/www.ietf.org](http://www.ietf.org/).  Questo è il comportamento appropriato della cache per la maggior parte delle applicazioni.  
  
### Per impostare i criteri automatici predefiniti per un'applicazione  
  
1.  Creare un oggetto basati sull'ora di criteri predefinito.  
  
2.  Impostare l'oggetto di criteri come predefinito per il dominio applicazione.  
  
## Esempio  
 I due esempi riportati in questa sezione producono i criteri identici.  
  
 Nell'esempio vengono creati i criteri temporizzati predefiniti e impostarlo su come predefinito per il dominio applicazione.  
  
```csharp  
public static void SetDefaultTimeBasedPolicy ()  
{  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy ();  
    HttpWebRequest.DefaultCachePolicy = policy ;  
}  
```  
  
```vb  
Public Shared Sub SetDefaultTimeBasedPolicy ()  
    Dim policy = New HttpRequestCachePolicy ()  
    HttpWebRequest.DefaultCachePolicy = policy  
End Sub  
```  
  
 È inoltre possibile creare criteri della cache basati sull'ora predefiniti utilizzando la classe <xref:System.Net.Cache.RequestCachePolicy> come illustrato nel seguente esempio:  
  
```csharp  
public static void SetDefaultTimeBasedPolicy2()  
{  
    RequestCachePolicy policy = new RequestCachePolicy ();  
    HttpWebRequest.DefaultCachePolicy = policy ;  
}  
```  
  
```vb  
Public Shared Sub SetDefaultTimeBasedPolicy2()  
    Dim policy As New RequestCachePolicy()  
    HttpWebRequest.DefaultCachePolicy = policy  
End Sub  
  
```  
  
## Vedere anche  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)   
 [Criteri di cache](../../../docs/framework/network-programming/cache-policy.md)   
 [Criteri di cache basati sulla posizione](../../../docs/framework/network-programming/location-based-cache-policies.md)   
 [Criteri di cache basati sull'ora](../../../docs/framework/network-programming/time-based-cache-policies.md)   
 [Elemento \<requestCaching\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)