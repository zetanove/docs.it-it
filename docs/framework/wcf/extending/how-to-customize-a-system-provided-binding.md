---
title: "Procedura: personalizzare un&#39;associazione fornita dal sistema | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f8b97862-e8bb-470d-8b96-07733c21fe26
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Procedura: personalizzare un&#39;associazione fornita dal sistema
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] include diverse associazioni fornite dal sistema che consentono di configurare alcune delle proprietà degli elementi di associazione sottostanti.  In questo argomento viene illustrato come impostare proprietà sugli elementi di associazione  per creare un'associazione personalizzata.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] su come creare e configurare direttamente elementi di associazione senza usare le associazioni fornite dal sistema, vedere [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla creazione e l'estensione di associazioni personalizzate, vedere [Estensione delle associazioni](../../../../docs/framework/wcf/extending/extending-bindings.md).  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tutte le associazioni sono costituite da *elementi di associazione*.  Ogni elemento di associazione deriva dalla classe <xref:System.ServiceModel.Channels.BindingElement>.  Le associazioni fornite dal sistema, ad esempio <xref:System.ServiceModel.BasicHttpBinding>, creano e configurano propri elementi di associazione.  In questo argomento viene illustrato come accedere e modificare le proprietà di questi elementi di associazione che non sono direttamente esposte sull'associazione; in particolare, la classe <xref:System.ServiceModel.BasicHttpBinding>.  
  
 I singoli elementi di associazione sono inclusi in una raccolta rappresentata dalla classe <xref:System.ServiceModel.Channels.BindingElementCollection> e vengono aggiunti nell'ordine seguente: Flusso delle transazioni, Sessione affidabile, Protezione, Duplex composito, Unidirezionale, Protezione di flusso, Codifica messaggi e Trasporto.  Si noti che non tutti gli elementi di associazione elencati sono necessari in ogni associazione.  In questa raccolta di elementi di associazione possono essere inclusi anche elementi di associazione definiti dall'utente, che devono essere visualizzati nello stesso ordine descritto in precedenza.  Ad esempio, un trasporto definito dall'utente deve essere l'ultimo elemento della raccolta di elementi di associazione.  
  
 La classe <xref:System.ServiceModel.BasicHttpBinding> contiene tre elementi di associazione:  
  
1.  Un elemento di associazione di sicurezza facoltativo: la classe <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> usata con il trasporto HTTP \(protezione a livello di messaggio\) o la classe <xref:System.ServiceModel.Channels.TransportSecurityBindingElement> usata quando il livello di trasporto fornisce la protezione, caso in cui viene usato il trasporto HTTPS.  
  
2.  Un elemento di associazione del codificatore dei messaggi obbligatorio: <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> o <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>.  
  
3.  Un elemento di associazione del trasporto obbligatorio: <xref:System.ServiceModel.Channels.HttpTransportBindingElement> o <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>.  
  
 In questo esempio viene creata un'istanza dell'associazione, da cui viene generata un'*associazione personalizzata*, vengono esaminati gli elementi di associazione nell'associazione personalizzata e, quando viene trovato l'elemento di associazione HTTP, viene impostata la proprietà `KeepAliveEnabled` su `false`.  La proprietà `KeepAliveEnabled` non è esposta direttamente su `BasicHttpBinding`, pertanto è necessario creare un'associazione personalizzata per spostarsi verso il basso sull'elemento di associazione e impostare questa proprietà.  
  
### Per modificare un'associazione fornita dal sistema  
  
1.  Creare un'istanza della classe <xref:System.ServiceModel.BasicHttpBinding> e impostarne la modalità di sicurezza a livello di messaggio.  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#1)]
     [!code-vb[C_HowTo_ChangeStandardBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#1)]  
  
2.  Creare un'associazione personalizzata dall'associazione e creare una classe <xref:System.ServiceModel.Channels.BindingElementCollection> da una delle proprietà dell'associazione personalizzata.  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#2)]
     [!code-vb[C_HowTo_ChangeStandardBinding#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#2)]  
  
3.  Eseguire un ciclo nella classe <xref:System.ServiceModel.Channels.BindingElementCollection> e, quando viene trovata la classe <xref:System.ServiceModel.Channels.HttpTransportBindingElement>, impostarne la proprietà <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A> su `false`.  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#3)]
     [!code-vb[C_HowTo_ChangeStandardBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#3)]  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>   
 <xref:System.ServiceModel.BasicHttpBinding>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md)