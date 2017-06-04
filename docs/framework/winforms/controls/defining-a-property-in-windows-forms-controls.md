---
title: "Definizione di una propriet&#224; nei controlli Windows Form | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], definizione delle proprietà nel codice"
  - "proprietà [Windows Form], definizione nel codice"
ms.assetid: c2eb8277-a842-4d99-89a9-647b901a0434
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Definizione di una propriet&#224; nei controlli Windows Form
Per informazioni generali sulle proprietà vedere [Properties Overview](../Topic/Properties%20Overview.md).  Quando si definisce una proprietà è importante tenere presenti alcuni aspetti:  
  
-   È necessario applicare attributi alle proprietà che si definiscono.  Gli attributi specificano le modalità di visualizzazione di una proprietà nella finestra di progettazione.  Per informazioni dettagliate vedere [Design\-Time Attributes for Components](../Topic/Design-Time%20Attributes%20for%20Components.md).  
  
-   Se la modifica di una proprietà ha effetto sulla visualizzazione del controllo, chiamare il metodo <xref:System.Windows.Forms.Control.Invalidate%2A> \(che il controllo eredita da <xref:System.Windows.Forms.Control>\) dalla funzione di accesso `set`.  <xref:System.Windows.Forms.Control.Invalidate%2A> chiama a sua volta il metodo <xref:System.Windows.Forms.Control.OnPaint%2A>, che ridisegna il controllo.  Più chiamate a <xref:System.Windows.Forms.Control.Invalidate%2A> producono, ai fini di una maggiore efficienza, un'unica chiamata a <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
-   La libreria di classi di .NET Framework fornisce convertitori di tipi per tipi di dati comuni quali Integer, numeri decimali, valori booleani e altri.  Lo scopo di un convertitore di tipi è in genere di operare una conversione da stringa a valore, ovvero da dati di tipo stringa ad altri tipi di dati.  I tipi di dati comuni sono associati a convertitori di tipi predefiniti che convertono i valori in stringhe e le stringhe nei tipi di dati appropriati.  Se si definisce una proprietà che rappresenta un tipo di dati personalizzato, ovvero non standard, sarà necessario applicare un attributo che specifichi il convertitore di tipi da associare a tale proprietà.  È inoltre possibile utilizzare un attributo per associare a una proprietà un editor di tipi con interfaccia utente personalizzato.  Un editor di tipi con interfaccia utente fornisce un'interfaccia utente per la modifica di una proprietà o di un tipo di dati.  La finestra Selezione colori è un esempio di editor di tipi con interfaccia utente.  Esempi di attributi sono forniti al termine di questo argomento.  
  
    > [!NOTE]
    >  Se non è disponibile alcun convertitore di tipi o editor di tipi con interfaccia utente per la proprietà personalizzata, sarà possibile implementarne uno come descritto in [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md).  
  
 Nel codice riportato di seguito viene definita una proprietà predefinita denominata `EndColor` per il controllo personalizzato `FlashTrackBar`.  
  
```vb  
Public Class FlashTrackBar  
   Inherits Control  
   ...  
   ' Private data member that backs the EndColor property.  
   Private _endColor As Color = Color.LimeGreen  
  
   ' The Category attribute tells the designer to display  
   ' it in the Flash grouping.   
   ' The Description attribute provides a description of  
   ' the property.   
   <Category("Flash"), _  
   Description("The ending color of the bar.")>  _  
   Public Property EndColor() As Color  
      ' The public property EndColor accesses _endColor.  
      Get  
         Return _endColor  
      End Get  
      Set  
         _endColor = value  
         If Not (baseBackground Is Nothing) And showGradient Then  
            baseBackground.Dispose()  
            baseBackground = Nothing  
         End If  
         ' The Invalidate method calls the OnPaint method, which redraws    
         ' the control.  
         Invalidate()  
      End Set  
   End Property  
   ...  
End Class  
  
```  
  
```csharp  
public class FlashTrackBar : Control {  
   ...  
   // Private data member that backs the EndColor property.  
   private Color endColor = Color.LimeGreen;  
   // The Category attribute tells the designer to display  
   // it in the Flash grouping.   
   // The Description attribute provides a description of  
   // the property.   
   [  
   Category("Flash"),  
   Description("The ending color of the bar.")  
   ]  
   // The public property EndColor accesses endColor.  
   public Color EndColor {  
      get {  
         return endColor;  
      }  
      set {  
         endColor = value;  
         if (baseBackground != null && showGradient) {  
            baseBackground.Dispose();  
            baseBackground = null;  
         }  
         // The Invalidate method calls the OnPaint method, which redraws   
         // the control.  
         Invalidate();  
      }  
   }  
   ...  
}  
```  
  
 Nel codice riportato di seguito vengono associati un convertitore di tipi e un editor di tipi con interfaccia utente alla proprietà `Value`.  In questo caso `Value` è un intero e presenta un convertitore di tipi predefinito, ma l'attributo <xref:System.ComponentModel.TypeConverterAttribute> applica un convertitore di tipi personalizzato \(`FlashTrackBarValueConverter`\) che consente la visualizzazione di tale intero sotto forma di valore percentuale nella finestra di progettazione.  L'editor di tipi con interfaccia utente, `FlashTrackBarValueEditor`, consente la rappresentazione visiva della percentuale.  In questo esempio viene inoltre mostrato che il convertitore di tipi o l'editor specificato dall'attributo <xref:System.ComponentModel.TypeConverterAttribute> o <xref:System.ComponentModel.EditorAttribute> esegue l'override del convertitore predefinito.  
  
```vb  
<Category("Flash"), _  
TypeConverter(GetType(FlashTrackBarValueConverter)), _  
Editor(GetType(FlashTrackBarValueEditor), _  
GetType(UITypeEditor)), _  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")>  _  
Public ReadOnly Property Value() As Integer  
...  
End Property  
  
```  
  
```csharp  
[  
Category("Flash"),   
TypeConverter(typeof(FlashTrackBarValueConverter)),  
Editor(typeof(FlashTrackBarValueEditor), typeof(UITypeEditor)),  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")  
]  
public int Value {  
...  
}  
```  
  
## Vedere anche  
 [Proprietà dei controlli Windows Form](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [Definizione dei valori predefiniti utilizzando i metodi ShouldSerialize e Reset](../../../../docs/framework/winforms/controls/defining-default-values-with-the-shouldserialize-and-reset-methods.md)   
 [Eventi per proprietà modificate](../../../../docs/framework/winforms/controls/property-changed-events.md)   
 [Attributi nei controlli Windows Form](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)