---
title: "Procedura: esporre le propriet&#224; dei controlli costitutivi | Microsoft Docs"
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
  - "controlli costitutivi"
  - "controlli [Windows Form], costitutivi"
  - "controlli personalizzati [Windows Form], esposizione di proprietà"
  - "controlli utente [Windows Form], controlli costitutivi esposti"
ms.assetid: 5c1ec98b-aa48-4823-986e-4712551cfdf1
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: esporre le propriet&#224; dei controlli costitutivi
I controlli che costituiscono un controllo composito sono detti *controlli costitutivi*.  Essi sono generalmente dichiarati Private e non sono pertanto accessibili allo sviluppatore.  Per rendere disponibili le proprietà di questi controlli agli utenti futuri, è necessario esporle all'utente.  La proprietà di un controllo costitutivo viene esposta creando una proprietà nel controllo utente e utilizzando le funzioni di accesso `get` e `set` di tale proprietà per rendere effettiva la modifica nella proprietà Private del controllo costitutivo.  
  
 Si consideri un controllo utente ipotetico con un pulsante costitutivo denominato `MyButton`.  In questo esempio, quando l'utente richiede la proprietà `ConstituentButtonBackColor`, viene inviato il valore memorizzato nella proprietà <xref:System.Windows.Forms.Control.BackColor%2A> di `MyButton`.  Quando l'utente assegna un valore a questa proprietà, tale valore viene automaticamente passato alla proprietà <xref:System.Windows.Forms.Control.BackColor%2A> di `MyButton` e viene eseguito il codice `set` che modifica il colore di `MyButton`.  
  
 L'esempio seguente mostra come esporre la proprietà <xref:System.Windows.Forms.Control.BackColor%2A> del pulsante costitutivo:  
  
```vb  
Public Property ButtonColor() as System.Drawing.Color  
   Get  
      Return MyButton.BackColor  
   End Get  
   Set(Value as System.Drawing.Color)  
      MyButton.BackColor = Value  
   End Set  
End Property  
```  
  
```csharp  
public Color ButtonColor  
{  
   get  
   {  
      return(myButton.BackColor);  
   }  
   set  
   {  
      myButton.BackColor = value;  
   }  
}  
```  
  
### Per esporre una proprietà di un controllo costitutivo  
  
1.  Creare una proprietà Public per il controllo utente.  
  
2.  Nella sezione `get` della proprietà scrivere il codice che recupera il valore della proprietà che si desidera esporre.  
  
3.  Nella sezione `set` della proprietà scrivere il codice che passa il valore della proprietà alla proprietà esposta del controllo costitutivo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.UserControl>   
 [Proprietà dei controlli Windows Form](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)