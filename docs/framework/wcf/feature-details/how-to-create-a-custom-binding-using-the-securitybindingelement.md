---
title: "Procedura: creare un&#39;associazione personalizzata usando SecurityBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sicurezza [WCF], creazione di associazioni personalizzate"
ms.assetid: 203a9f9e-3a73-427c-87aa-721c56265b29
caps.latest.revision: 19
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 19
---
# Procedura: creare un&#39;associazione personalizzata usando SecurityBindingElement
In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono incluse numerose associazioni fornite dal sistema che possono essere configurate, ma che non forniscono totale flessibilità durante la configurazione di tutte le opzioni di sicurezza supportate da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. In questo argomento viene illustrato come creare direttamente un'associazione personalizzata di singoli elementi di associazione e vengono evidenziate alcune impostazioni di sicurezza che è possibile specificare durante la creazione di tale associazione. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]creazione di associazioni personalizzate, vedere [estensione delle associazioni](../../../../docs/framework/wcf/extending/extending-bindings.md).  
  
> [!WARNING]
>  <xref:System.ServiceModel.Channels.SecurityBindingElement> non supporta il <xref:System.ServiceModel.Channels.IDuplexSessionChannel> shape, che è la forma di canale predefinita utilizzata da TCP del canale di trasporto quando <xref:System.ServiceModel.TransferMode> è impostato su <xref:System.ServiceModel.TransferMode.Buffered>. È necessario impostare <xref:System.ServiceModel.TransferMode> a <xref:System.ServiceModel.TransferMode.Streamed> per poter utilizzare <xref:System.ServiceModel.Channels.SecurityBindingElement> in questo scenario.  
  
## <a name="creating-a-custom-binding"></a>Creazione di un'associazione personalizzata  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tutte le associazioni sono costituite da *gli elementi di associazione*. Ogni elemento di associazione deriva il <xref:System.ServiceModel.Channels.BindingElement> (classe). Per le associazioni standard fornite dal sistema, vengono creati e configurati gli elementi di associazione, sebbene sia possibile personalizzare alcune delle impostazioni delle proprietà.  
  
 Al contrario, per creare un'associazione personalizzata, vengono creati e configurati gli elementi di associazione e un <xref:System.ServiceModel.Channels.CustomBinding> creato dagli elementi di associazione.  
  
 A tale scopo, aggiungere singoli elementi di associazione a una raccolta rappresentata da un'istanza del <xref:System.ServiceModel.Channels.BindingElementCollection> e quindi impostare il `Elements` proprietà del `CustomBinding` uguale all'oggetto. È necessario aggiungere gli elementi di associazione nell'ordine seguente: Transaction Flow, Reliable Session, Security, Composite Duplex, One-way, Stream Security, Message Encoding e Transport. Si noti che non tutti gli elementi di associazione elencati sono necessari in ogni associazione.  
  
## <a name="securitybindingelement"></a>SecurityBindingElement  
 Tre elementi di associazione sono correlati alla sicurezza a livello di messaggio, che derivano dal <xref:System.ServiceModel.Channels.SecurityBindingElement> (classe). I tre elementi sono <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>, <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>, e <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>. Il <xref:System.ServiceModel.Channels.TransportSecurityBindingElement> viene utilizzata per fornire sicurezza a modalità mista. Gli altri due elementi sono utilizzati quando la protezione è fornita dal livello di messaggio.  
  
 Le classi aggiuntive vengono utilizzate quando viene fornita la protezione a livello di trasporto:  
  
-   <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
-   <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
## <a name="required-binding-elements"></a>Elementi di associazione obbligatori  
 Esiste un ampio numero di possibili elementi di associazione che si possono combinare in un'associazione. Non tutte queste combinazioni sono valide. Contenuto della sezione vengono descritti gli elementi obbligatori che devono essere presenti in un'associazione di sicurezza.  
  
 Le associazioni di sicurezza valide dipendono da molti fattori, tra cui:  
  
-   Modalità di sicurezza.  
  
-   Protocollo di trasporto.  
  
-   Modello di scambio dei messaggi (MEP, Message Exchange Pattern) specificato nel contratto.  
  
 Nella tabella seguente vengono illustrate le configurazioni dello stack dell'elemento di associazione valide per ogni combinazione dei fattori precedenti. Si noti che si tratta di requisiti minimi. È possibile aggiungere ulteriori elementi all'associazione, ad esempio elementi di associazione di codifica dei messaggi, di transazione e di altro tipo.  
  
|Modalità di sicurezza|Trasporto|Modello di scambio dei messaggi del contratto|Modello di scambio dei messaggi del contratto|Modello di scambio dei messaggi del contratto|  
|-------------------|---------------|---------------------------------------|---------------------------------------|---------------------------------------|  
|||`Datagram`|`Request Reply`|`Duplex`|  
|Trasporto|Https||||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP||||  
|||OneWayBindingElement|||  
|||SSL o Windows StreamSecurityBindingElement|SSL o Windows StreamSecurityBindingElement|SSL o Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|Messaggio|Http|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement (modalità di autenticazione = SecureConversation)|  
|||||CompositeDuplexBindingElement|  
|||OneWayBindingElement||OneWayBindingElement|  
|||HttpTransportBindingElement|HttpTransportBindingElement|HttpTransportBindingElement|  
||Tcp|SecurityBindingElement|SecurityBindingElement|SymmetricSecurityBindingElement (modalità di autenticazione = SecureConversation)|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|Misto (trasporto con credenziali messaggio)|Https|TransportSecurityBindingElement|TransportSecurityBindingElement||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP|TransportSecurityBindingElement|SymmetricSecurityBindingElement (modalità di autenticazione = SecureConversation)|SymmetricSecurityBindingElement (modalità di autenticazione = SecureConversation)|  
|||OneWayBindingElement|||  
|||SSL o Windows StreamSecurityBindingElement|SSL o Windows StreamSecurityBindingElement|SSL o Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
  
 Si noti che esistono molte impostazioni configurabili in SecurityBindingElements. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Modalità di autenticazione di SecurityBindingElement](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md).  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Conversazioni e sessioni protette](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md).  
  
## <a name="procedures"></a>Procedure  
  
#### <a name="to-create-a-custom-binding-that-uses-a-symmetricsecuritybindingelement"></a>Per creare un'associazione personalizzata che utilizza un SymmetricSecurityBindingElement  
  
1.  Creare un'istanza di <xref:System.ServiceModel.Channels.BindingElementCollection> classe con il nome `outputBec`.  
  
2.  Chiamare il metodo statico `M:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement(true)`, che restituisce un'istanza di <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> (classe).  
  
3.  Aggiungere il <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> alla raccolta (`outputBec`) chiamando il `Add` metodo il <xref:System.Collections.ObjectModel.Collection%601> di <xref:System.ServiceModel.Channels.BindingElement> (classe).  
  
4.  Creare un'istanza di <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> classe e aggiungerla alla raccolta (`outputBec`). In tal modo viene specificata la codifica utilizzata dall'associazione.  
  
5.  Creare un <xref:System.ServiceModel.Channels.HttpTransportBindingElement> e aggiungerlo alla raccolta (`outputBec`). In tal modo viene specificato che l'associazione utilizza il trasporto HTTP.  
  
6.  Creare una nuova associazione personalizzata creando un'istanza di <xref:System.ServiceModel.Channels.CustomBinding> classe e passando la raccolta `outputBec` al costruttore.  
  
7.  L'associazione personalizzata risultante condivide molte delle stesse caratteristiche standard <xref:System.ServiceModel.WSHttpBinding>. Specifica la protezione a livello di messaggio e le credenziali di Windows, ma disattiva le sessioni protette. Richiede che la credenziale del servizio venga specificata fuori banda e non crittografa le firme. L'ultima può essere controllata solo impostando la <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A> proprietà come illustrato nel passaggio 4. Le altre possono essere controllate utilizzando le impostazioni nell'associazione standard.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene riportata una funzione completa per creare un'associazione personalizzata che utilizza un <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>.  
  
### <a name="code"></a>Codice  
 [!code-csharp[c_CustomBinding#20](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#20)]
 [!code-vb[c_CustomBinding#20](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombinding/vb/source.vb#20)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>   
 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Estensione delle associazioni](../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md)