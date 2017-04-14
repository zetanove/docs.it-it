---
title: "Derivazione da WebResponse | Microsoft Docs"
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
  - "Derivazione da WebResponse"
ms.assetid: f11d4866-a199-4087-9306-a5a4c18b13db
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Derivazione da WebResponse
La classe <xref:System.Net.WebResponse> è una classe base astratta che fornisce metodi e proprietà di base per creare una risposta protocollo specifica che estende il modello di protocollo di .NET Framework.  Le applicazioni che utilizzano la classe <xref:System.Net.WebRequest> ai dati della richiesta le risorse ricevono le risposte in **WebResponse**.  i discendenti protocollo specifici **WebResponse** devono implementare i membri astratti della classe **WebResponse**.  
  
 La classe collegata **WebRequest** deve creare i discendenti **WebResponse**.  Ad esempio, le istanze <xref:System.Net.HttpWebResponse> vengono create solo come risultato della chiamata <xref:System.Net.HttpWebRequest.GetResponse%2A?displayProperty=fullName> o <xref:System.Net.HttpWebRequest.EndGetResponse%2A?displayProperty=fullName>.  Ogni **WebResponse** contiene il risultato di una richiesta a una risorsa e non deve essere riutilizzato.  
  
## Proprietà di ContentLength  
 La proprietà <xref:System.Net.WebResponse.ContentLength%2A> indica il numero di byte di dati disponibili dal flusso restituito dal metodo <xref:System.Net.WebResponse.GetResponseStream%2A>.  La proprietà **ContentLength** non indica il numero di byte di intestazione o delle informazioni dei metadati restituite dal server; indica solo il numero di byte dei dati della risorsa richiesta stesso.  
  
## Proprietà di Tipocontenuto  
 La proprietà <xref:System.Net.WebResponse.ContentType%2A> fornisce tutte le informazioni specifiche del protocollo è necessario inviare al client per identificare il tipo di contenuto inviato dal server.  In genere questo è il tipo di contenuto MIME di tutti i dati restituiti.  
  
## Proprietà delle intestazioni  
 La proprietà <xref:System.Net.WebResponse.Headers%2A> contiene una raccolta arbitraria di coppie nome\/valore dei metadati associati alla risposta.  Tutti i metadati necessari dal protocollo che può essere espresso come coppia nome\/valore possono essere inclusi nella proprietà **Headers**.  
  
 Non è necessario utilizzare la proprietà **Headers** per utilizzare i metadati dell'intestazione.  i metadati protocollo specifici possono essere esposti come proprietà; ad esempio, la proprietà <xref:System.Net.HttpWebResponse.LastModified%2A?displayProperty=fullName> espone l'intestazione HTTP **Last\-Modified**.  Quando si espone i metadati dell'intestazione come proprietà, non è necessario consentire la stessa proprietà da impostare utilizzando la proprietà **Headers**.  
  
## Proprietà di ResponseUri  
 La proprietà <xref:System.Net.WebResponse.ResponseUri%2A> contiene l'uri della risorsa che effettivamente fornita dalla risposta.  Per i protocolli che non supportano il reindirizzamento, **ResponseUri** sarà lo stesso della proprietà <xref:System.Net.WebRequest.RequestUri%2A>**WebRequest** che ha creato la risposta.  Se i contenuti multimediali protocolli di reindirizzamento la richiesta, **ResponseUri** conterranno l'uri della risposta.  
  
## Metodo close  
 Il metodo <xref:System.Net.WebResponse.Close%2A> chiuse tutte le connessioni dalla richiesta e la risposta e pulizia delle risorse utilizzate dalla risposta.  Il metodo **Close** chiudere tutte le istanze del flusso utilizzate dalla risposta, ma non genera un'eccezione se il flusso di risposte in precedenza è stato chiuso da una chiamata al metodo <xref:System.IO.Stream.Close%2A?displayProperty=fullName>.  
  
## Metodo di GetResponseStream  
 Il metodo <xref:System.Net.WebResponse.GetResponseStream%2A> restituisce un flusso che contiene la risposta alla risorsa richiesta.  Il flusso di risposte contiene solo i dati restituiti dalla risorsa, qualsiasi intestazione o importato di metadati nella risposta deve essere rimosso dalla risposta ed essere esposto all'applicazione tramite le proprietà specifiche del protocollo o la proprietà **Headers**.  
  
 L'istanza del flusso restituita dal metodo **GetResponseStream** è posseduta dall'applicazione e può essere chiusa senza chiudere **WebResponse**.  Per convenzione, chiamare il metodo **WebResponse.Close** si chiude il flusso restituito da **GetResponse**.  
  
## Vedere anche  
 <xref:System.Net.WebResponse>   
 <xref:System.Net.HttpWebResponse>   
 <xref:System.Net.FileWebResponse>   
 [Programmazione di protocolli di collegamento](../../../docs/framework/network-programming/programming-pluggable-protocols.md)   
 [Derivazione da WebRequest](../../../docs/framework/network-programming/deriving-from-webrequest.md)