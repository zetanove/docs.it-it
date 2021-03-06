---
title: "Aggiungere un riferimento al servizio in un progetto di subset portabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 61ccfe0f-a34b-40ca-8f5e-725fa1b8095e
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Aggiungere un riferimento al servizio in un progetto di subset portabili
I progetti di subset portabili consentono ai programmatori di assembly .NET di gestire un unico albero di origine e di compilare il sistema supportando allo stesso tempo più piattaforme .NET \(desktop, Silverlight, Windows Phone e XBOX\).I progetti di subset portabili fanno riferimento solo alle librerie portabili .NET che rappresentano un assembly .NET Framework che può essere utilizzato in qualsiasi piattaforma .NET principale.  
  
## Dettagli relativi a Aggiungi riferimento al servizio  
 Quando si aggiunge un riferimento al servizio in un progetto di subset portabili, si applicano le limitazioni seguenti:  
  
1.  Per l'oggetto <xref:System.Xml.Serialization.XmlSerializer> sono consentite solo le codifiche letterali.Le codifiche SOAP generano un errore durante l'importazione.  
  
2.  Per i servizi che utilizzano gli scenari <xref:System.Runtime.Serialization.DataContractSerializer>, viene fornito un surrogato del contratto dati per assicurarsi che i tipi riutilizzati provengano solo dal subset portabile.  
  
3.  Gli endpoint che si basano su associazioni non supporte nelle librerie portabili \(tutte le associazioni tranne <xref:System.ServiceModel.BasicHttpBinding>, l'oggetto <xref:System.ServiceModel.WsHttpBinding> senza flusso di transazione, le sessioni affidabili o la codifica MTOM e le associazioni personalizzate equivalenti\) vengono ignorati.  
  
4.  Le intestazioni dei messaggi vengono eliminate da tutte le descrizioni dei messaggi in tutte le operazioni prima dell'importazione.  
  
5.  Gli attributi non portabili <xref:System.ComponentModel.DesignerCategoryAttribute>, <xref:System.Serializable> e <xref:System.ServiceModel.TransactionFlow> vengono rimossi dal codice del proxy client generato.  
  
6.  Le proprietà non portabili ProtectionLevel, SessionMode, IsInitiating, IsTerminating vengono rimosse dagli oggetti <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.OperationContract> e <xref:System.ServiceModel.FaultContract>.  
  
7.  Tutte le operazioni del servizio vengono create come operazioni asincrone nel proxy client.  
  
8.  I costruttori client generati che utilizzano i tipi non portabili vengono rimossi.  
  
9. Un'istanza dell'oggetto <xref:System.Net.CookieContainer> viene esposta nel client generato.  
  
10. All'inizio del file viene inserito un commento che identifica l'assembly e la versione del generatore di codice:`// This code was auto-generated by Microsoft.VisualStudio.Portable.AddServiceReference, version 1.0.0.0`  
  
11. L'interfaccia <xref:System.Runtime.Serialization.ISerializable> non è supportata.  
  
12. Le associazioni Net.Tcp e PollingDuplex non sono supportate  
  
13. L'oggetto <xref:System.Runtime.Serialization.DataContractSerializer> verrà sempre utilizzato per gli errori.  
  
14. La proprietà <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> non è supportata nei progetti di subset portabili.  
  
## Vedere anche  
 [Accesso ai servizi tramite client WCF](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)   
 [Libreria di classi portabile](http://msdn.microsoft.com/library/gg597391\(v=vs.110\))