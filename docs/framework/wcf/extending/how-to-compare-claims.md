---
title: "Procedura: confrontare le attestazioni | Microsoft Docs"
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
  - "attestazioni [WCF]"
  - "attestazioni [WCF], confronto"
ms.assetid: 0c4ec84d-53df-408f-8953-9bc437f56c28
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: confrontare le attestazioni
Per l'esecuzione dei controlli di autorizzazione viene utilizzata l'infrastruttura del modello di identità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Un'attività comune consiste quindi nel confrontare le attestazioni presenti nel contesto di autorizzazione con le attestazioni richieste per eseguire l'azione richiesta o accedere alla risorsa richiesta.In questo argomento viene illustrato come confrontare le attestazioni, compresi i tipi di attestazione incorporati e personalizzati.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] l'infrastruttura del modello di identità, vedere [Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md).  
  
 Questa operazione implica il confronto delle tre parti di un'attestazione \(tipo, diritto e risorsa\) con le stesse parti di un'altra attestazione per verificarne la corrispondenza.Vedere l'esempio seguente.  
  
 [!code-csharp[c_CustomClaimComparison#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#9)]
 [!code-vb[c_CustomClaimComparison#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#9)]  
  
 Entrambe le attestazioni dispongono di un tipo <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A>, un diritto <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> e una risorsa "someone."Poiché tutte le tre parti delle attestazioni sono uguali, le attestazioni sono uguali.  
  
 I tipi di attestazione incorporati vengono confrontati utilizzando il metodo <xref:System.IdentityModel.Claims.Claim.Equals%2A>.Il codice di confronto specifico dell'attestazione viene utilizzato laddove necessario.Ad esempio, date le due attestazioni del nome dell'entità utente \(UPN\) seguenti:  
  
 [!code-csharp[c_CustomClaimComparison#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#4)]
 [!code-vb[c_CustomClaimComparison#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#4)]  
  
 il codice di confronto nel metodo <xref:System.IdentityModel.Claims.Claim.Equals%2A> restituisce `true`, presupponendo che `example\someone` identifichi lo stesso utente del dominio di "someone@example.com."  
  
 Anche i tipi di attestazione personalizzati possono essere confrontati utilizzando il metodo <xref:System.IdentityModel.Claims.Claim.Equals%2A>.Tuttavia, nei casi in cui il tipo restituito dalla proprietà <xref:System.IdentityModel.Claims.Claim.Resource%2A> dell'attestazione non è un tipo primitivo, il metodo <xref:System.IdentityModel.Claims.Claim.Equals%2A> restituisce `true` solo se i valori restituiti dalle proprietà `Resource` sono uguali in base al metodo <xref:System.IdentityModel.Claims.Claim.Equals%2A>.Negli altri casi, il tipo personalizzato restituito dalla proprietà `Resource` deve eseguire l'override dei metodi <xref:System.IdentityModel.Claims.Claim.Equals%2A> e <xref:System.Object.GetHashCode%2A> per eseguire qualsiasi elaborazione personalizzata necessaria.  
  
### Confronto di attestazioni incorporate  
  
1.  Date due istanze della classe <xref:System.IdentityModel.Claims.Claim>, utilizzare il metodo <xref:System.IdentityModel.Claims.Claim.Equals%2A> per eseguire il confronto, come illustrato nel codice seguente.  
  
     [!code-csharp[c_CustomClaimComparison#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#5)]
     [!code-vb[c_CustomClaimComparison#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#5)]  
  
### Confronto di attestazioni personalizzate con tipi di risorsa primitivi  
  
1.  Per le attestazioni personalizzate con tipi di risorsa primitivi, è possibile eseguire il confronto come per le attestazioni incorporate, come illustrato nel codice seguente.  
  
     [!code-csharp[c_CustomClaimComparison#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#6)]
     [!code-vb[c_CustomClaimComparison#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#6)]  
  
2.  Per attestazioni personalizzate con tipi di risorsa basati su strutture o su classi, il tipo di risorsa deve eseguire l'override del metodo <xref:System.IdentityModel.Claims.Claim.Equals%2A>.  
  
3.  Controllare innanzitutto se il parametro `obj` è `null` e, in caso affermativo, restituire `false`.  
  
     [!code-csharp[c_CustomClaimComparison#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#7)]
     [!code-vb[c_CustomClaimComparison#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#7)]  
  
4.  Quindi chiamare il metodo <xref:System.Object.ReferenceEquals%2A> e passare `this` e `obj` come parametri.Se viene restituito `true`, restituire `true`.  
  
     [!code-csharp[c_CustomClaimComparison#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#8)]
     [!code-vb[c_CustomClaimComparison#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#8)]  
  
5.  Tentare di assegnare il parametro `obj` a una variabile locale del tipo di classe.In caso di errore, il riferimento è `null`.In tali casi, restituire `false`.  
  
6.  Eseguire il confronto personalizzato necessario per confrontare correttamente l'attestazione attuale con quella fornita.  
  
## Esempio  
 Nell'esempio seguente viene illustrato un confronto di attestazioni personalizzate in cui la risorsa dell'attestazione è un tipo non primitivo.  
  
 [!code-csharp[c_CustomClaimComparison#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#0)]
 [!code-vb[c_CustomClaimComparison#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#0)]  
  
## Vedere anche  
 [Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)   
 [Procedura: creare un'attestazione personalizzata](../../../../docs/framework/wcf/extending/how-to-create-a-custom-claim.md)