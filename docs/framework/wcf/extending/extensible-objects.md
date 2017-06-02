---
title: "Oggetti estensibili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "oggetti estensibili [WCF]"
ms.assetid: bc88cefc-31fb-428e-9447-6d20a7d452af
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Oggetti estensibili
Questo modello viene usato per estendere le classi di runtime esistenti con nuove funzionalità oppure per aggiungere un nuovo stato a un oggetto.  Le estensioni, allegate a uno degli oggetti estensibili, attivano i comportamenti in fasi molto diverse dell'elaborazione per accedere a stato e funzionalità condivisi allegati a un oggetto estensibile comune al quale possono accedere.  
  
## Modello IExtensibleObject\<T\>  
 Nel modello di oggetti estensibili sono disponibili tre interfacce: <xref:System.ServiceModel.IExtensibleObject%601>, <xref:System.ServiceModel.IExtension%601> e <xref:System.ServiceModel.IExtensionCollection%601>.  
  
 L'interfaccia <xref:System.ServiceModel.IExtensibleObject%601> viene implementata dai tipi che consentono agli oggetti <xref:System.ServiceModel.IExtension%601> di personalizzare la funzionalità.  
  
 Gli oggetti estendibili consentono l'aggregazione dinamica di oggetti <xref:System.ServiceModel.IExtension%601>.  Gli oggetti <xref:System.ServiceModel.IExtension%601> sono caratterizzati dall'interfaccia seguente:  
  
```  
public interface IExtension<T>  
where T : IExtensibleObject<T>  
{  
    void Attach(T owner);  
    void Detach(T owner);  
}  
```  
  
 Tramite la restrizione dei tipi è possibile garantire che le estensioni possano essere definite solo per le classi <xref:System.ServiceModel.IExtensibleObject%601>.  <xref:System.ServiceModel.IExtension%601.Attach%2A> e <xref:System.ServiceModel.IExtension%601.Detach%2A> forniscono la notifica dell'aggregazione o disaggregazione.  
  
 È consigliabile limitare le implementazioni quando possono essere aggiunte e rimosse da un proprietario.  Ad esempio, è possibile impedire completamente la rimozione, impedire l'aggiunta o la rimozione delle estensioni quando il proprietario o l'estensione sono in un determinato stato, impedire l'aggiunta contemporaneamente a più proprietari o consentire solo una singola aggiunta seguita da una singola rimozione.  
  
 <xref:System.ServiceModel.IExtension%601> non implica alcuna interazione con le altre interfacce standard gestite.  In particolare, il metodo <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> sull'oggetto proprietario in genere non disconnette le relative estensioni.  
  
 Quando si aggiunge un'estensione alla raccolta, <xref:System.ServiceModel.IExtension%601.Attach%2A> viene chiamato prima dell'aggiunta alla raccolta. Quando si rimuove un'estensione dalla raccolta, <xref:System.ServiceModel.IExtension%601.Detach%2A> viene chiamato dopo la rimozione. Ciò significa che \(presupponendo che la sincronizzazione avvenga correttamente\) un'estensione può essere disponibile nella raccolta solo tra <xref:System.ServiceModel.IExtension%601.Attach%2A> e <xref:System.ServiceModel.IExtension%601.Detach%2A>.  
  
 L'oggetto passato al metodo <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> o al metodo <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> non deve necessariamente essere <xref:System.ServiceModel.IExtension%601> \(ad esempio, è possibile passare qualsiasi oggetto\), ma l'estensione restituita è un'interfaccia <xref:System.ServiceModel.IExtension%601>.  
  
 Se nessuna estensione nella raccolta è un oggetto <xref:System.ServiceModel.IExtension%601>, <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> restituisce Null e <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> restituisce una raccolta vuota. Se più estensioni implementano l'oggetto <xref:System.ServiceModel.IExtension%601>, <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> restituisce una di esse.  Il valore restituito dal metodo <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> è un'istantanea.  
  
 Sono disponibili due scenari principali.  Nel primo scenario la proprietà <xref:System.ServiceModel.IExtensibleObject%601.Extensions%2A> viene usa come un dizionario basato sui tipi per inserire lo stato su un oggetto allo scopo di consentire a un altro componente di ricercarlo usando il tipo.  
  
 Nel secondo scenario vengono usate le proprietà <xref:System.ServiceModel.IExtension%601.Attach%2A> e <xref:System.ServiceModel.IExtension%601.Detach%2A> per consentire a un oggetto di partecipare a un comportamento personalizzato, ad esempio la registrazione per gli eventi, il controllo delle transizioni di stato e così via.  
  
 L'interfaccia <xref:System.ServiceModel.IExtensionCollection%601> è una raccolta degli oggetti <xref:System.ServiceModel.IExtension%601> che consentono il recupero di <xref:System.ServiceModel.IExtension%601> in base al tipo.  <xref:System.ServiceModel.IExtensionCollection%601.Find%2A?displayProperty=fullName> restituisce l'ultimo oggetto aggiunto che è un oggetto <xref:System.ServiceModel.IExtension%601> di quel tipo.  
  
### Oggetti estensibili in Windows Communication Foundation  
 In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] esistono quattro oggetti estensibili:  
  
-   <xref:System.ServiceModel.ServiceHostBase>: è la classe base per l'host del servizio.  Le estensioni di questa classe possono essere usate per estendere il comportamento di <xref:System.ServiceModel.ServiceHostBase> o per archiviare lo stato per ogni servizio.  
  
-   <xref:System.ServiceModel.InstanceContext>: questa classe collega un'istanza del tipo del servizio con il runtime del servizio.  Contiene informazioni sull'istanza e un riferimento alla classe <xref:System.ServiceModel.ServiceHostBase> che contiene la classe <xref:System.ServiceModel.InstanceContext>.  Le estensioni di questa classe possono essere usate per estendere il comportamento di <xref:System.ServiceModel.InstanceContext> o per archiviare lo stato per ogni servizio.  
  
-   <xref:System.ServiceModel.OperationContext>: questa classe rappresenta le informazioni dell'operazione che il runtime raccoglie per ogni operazione.  Tra queste informazioni sono incluse le intestazioni dei messaggi in arrivo, le proprietà dei messaggi in arrivo, l'identità di sicurezza dei messaggi in arrivo e altre informazioni.  Le estensioni di questa classe possono estendere il comportamento di <xref:System.ServiceModel.OperationContext> o archiviare lo stato per ogni operazione.  
  
-   <xref:System.ServiceModel.IContextChannel>: questa interfaccia consente l'ispezione di ogni stato per i canali e i proxy compilati dal runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Le estensioni di questa classe possono estendere il comportamento di <xref:System.ServiceModel.IClientChannel> o usarlo per archiviare lo stato per ogni canale.  
  
 Nell'esempio di codice seguente viene illustrato l'uso di un'estensione semplice per tenere traccia degli oggetti <xref:System.ServiceModel.InstanceContext>.  
  
 [!code-csharp[IInstanceContextInitializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/iinstancecontextinitializer/cs/initializer.cs#1)]  
  
## Vedere anche  
 <xref:System.ServiceModel.IExtensibleObject%601>   
 <xref:System.ServiceModel.IExtension%601>   
 <xref:System.ServiceModel.IExtensionCollection%601>