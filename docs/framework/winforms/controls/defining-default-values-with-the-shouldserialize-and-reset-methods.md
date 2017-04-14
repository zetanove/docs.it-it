---
title: "Definizione dei valori predefiniti utilizzando i metodi ShouldSerialize e Reset | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], metodi delle proprietà"
  - "Reset (metodo)"
  - "ShouldPersist (metodo)"
ms.assetid: 7b6c5e00-3771-46b4-9142-5a80d5864a5e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Definizione dei valori predefiniti utilizzando i metodi ShouldSerialize e Reset
`ShouldSerialize` e `Reset` sono metodi facoltativi che è possibile fornire per una proprietà, se tale proprietà non presenta un valore predefinito semplice.  Se la proprietà presenta un valore predefinito semplice, sarà necessario applicare <xref:System.ComponentModel.DefaultValueAttribute> e fornire invece il valore predefinito al costruttore della classe Attribute.  Entrambi questi meccanismi consentono di avvalersi, all'interno della finestra di progettazione, delle seguenti caratteristiche:  
  
-   La proprietà fornisce un'indicazione visiva nel visualizzatore proprietà se sono state apportate modifiche rispetto al valore predefinito.  
  
-   È possibile fare clic con il pulsante destro del mouse sulla proprietà e scegliere **Reimposta** per ripristinare il valore predefinito della proprietà.  
  
-   La finestra di progettazione genera codice più efficiente.  
  
    > [!NOTE]
    >  Applicare <xref:System.ComponentModel.DefaultValueAttribute> oppure fornire i metodi `Reset`*NomeProprietà* e `ShouldSerialize`*NomeProprietà*.  Non effettuare entrambe le operazioni.  
  
 Il metodo `Reset`*NomeProprietà* imposta una proprietà sul relativo valore predefinito, come illustrato nel frammento di codice riportato di seguito.  
  
```vb  
Public Sub ResetMyFont()  
   MyFont = Nothing  
End Sub  
```  
  
```csharp  
public void ResetMyFont() {  
   MyFont = null;  
}  
```  
  
> [!NOTE]
>  Se una proprietà non dispone di un metodo `Reset`, non è associata a un <xref:System.ComponentModel.DefaultValueAttribute> e non presenta un valore predefinito nella propria dichiarazione, l'opzione `Reset` per tale proprietà risulta disabilitata nel menu di scelta rapida della finestra **Proprietà** di Progettazione Windows Form in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
 Le finestre di progettazione quali [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] utilizzano il metodo `ShouldSerialize`*NomeProprietà* per verificare se una proprietà è stata modificata rispetto al valore predefinito e per scrivere codice nel form solo in caso di modifica, consentendo in tal modo una generazione del codice più efficiente.  Di seguito è riportato un esempio:  
  
```vb  
'Returns true if the font has changed; otherwise, returns false.  
' The designer writes code to the form only if true is returned.  
Public Function ShouldSerializeMyFont() As Boolean  
   Return Not (thefont Is Nothing)  
End Function  
```  
  
```csharp  
// Returns true if the font has changed; otherwise, returns false.  
// The designer writes code to the form only if true is returned.  
public bool ShouldSerializeMyFont() {  
   return thefont != null;  
}  
```  
  
 Di seguito è riportato un esempio di codice completo.  
  
```vb  
Option Explicit  
Option Strict  
  
Imports System  
Imports System.Windows.Forms  
Imports System.Drawing  
  
Public Class MyControl  
   Inherits Control  
  
   ' Declare an instance of the Font class  
   ' and set its default value to Nothing.  
   Private thefont As Font = Nothing  
  
   ' The MyFont property.   
   Public Property MyFont() As Font  
      ' Note that the Font property never  
      ' returns null.  
      Get  
         If Not (thefont Is Nothing) Then  
            Return thefont  
         End If  
         If Not (Parent Is Nothing) Then  
            Return Parent.Font  
         End If  
         Return Control.DefaultFont  
      End Get  
      Set  
         thefont = value  
      End Set  
   End Property  
  
   Public Function ShouldSerializeMyFont() As Boolean  
      Return Not (thefont Is Nothing)  
   End Function  
  
   Public Sub ResetMyFont()  
      MyFont = Nothing  
   End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Drawing;  
  
public class MyControl : Control {  
   // Declare an instance of the Font class  
   // and set its default value to null.  
   private Font thefont = null;  
  
   // The MyFont property.      
   public Font MyFont {  
      // Note that the MyFont property never  
      // returns null.  
      get {  
         if (thefont != null) return thefont;  
         if (Parent != null) return Parent.Font;  
         return Control.DefaultFont;  
      }  
      set {  
         thefont = value;  
      }  
   }  
  
   public bool ShouldSerializeMyFont() {  
      return thefont != null;  
   }  
  
   public void ResetMyFont() {  
      MyFont = null;  
   }  
}  
```  
  
 In questo caso, anche se il valore della variabile privata a cui accede la proprietà `MyFont` è `null`, nel Visualizzatore proprietà non viene riportato il valore `null`, ma la proprietà <xref:System.Windows.Forms.Control.Font%2A> del padre, se non è `null`, o il valore <xref:System.Windows.Forms.Control.Font%2A> predefinito specificato in <xref:System.Windows.Forms.Control>.  Non è pertanto possibile impostare semplicemente il valore predefinito di `MyFont`  né applicare un <xref:System.ComponentModel.DefaultValueAttribute> a questa proprietà.  È invece necessario implementare i metodi `ShouldSerialize` e `Reset` per la proprietà `MyFont`.  
  
## Vedere anche  
 [Proprietà dei controlli Windows Form](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [Definizione di una proprietà](../../../../docs/framework/winforms/controls/defining-a-property-in-windows-forms-controls.md)   
 [Eventi per proprietà modificate](../../../../docs/framework/winforms/controls/property-changed-events.md)