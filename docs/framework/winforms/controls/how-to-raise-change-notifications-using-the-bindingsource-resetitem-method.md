---
title: "Procedura: generare notifiche di modifica utilizzando il metodo ResetItem di BindingSource | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BindingSource (componente) [Windows Form], generazione di notifiche di modifica"
  - "notifiche di modifica"
  - "notifiche di modifica, generazione"
  - "associazione dati, notifiche di modifica"
  - "origini dati, rilevamento modifiche"
ms.assetid: ab8b4096-37ff-4e30-aabc-de79a2f2e972
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: generare notifiche di modifica utilizzando il metodo ResetItem di BindingSource
Alcune origini dati dei controlli non generano notifiche di modifica quando si verificano modifiche, aggiunte o eliminazioni di elementi.  Il componente <xref:System.Windows.Forms.BindingSource> consente di eseguire l'associazione a tali origini dati e di generare una notifica di modifica dal codice.  
  
## Esempio  
 Questo form illustra l'uso di un componente <xref:System.Windows.Forms.BindingSource> per associare un elenco a un controllo <xref:System.Windows.Forms.DataGridView>.  Poiché l'elenco non genera notifiche di modifica, quando un elemento dell'elenco subisce una modifica viene chiamato il metodo <xref:System.Windows.Forms.BindingSource.ResetItem%2A> dell'elemento <xref:System.Windows.Forms.BindingSource>.  .  
  
 [!code-cpp[System.Windows.Forms.DataConnector.ResetItem#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.ResetItem/CPP/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.DataConnector.ResetItem#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.ResetItem/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnector.ResetItem#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.ResetItem/VB/form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Data, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.BindingNavigator>   
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Procedura: associare un controllo Windows Form a un tipo](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)