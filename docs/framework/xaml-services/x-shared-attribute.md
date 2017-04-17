---
title: "x:Shared Attribute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XAML [XAML Services], x:Shared attribute"
  - "x:Shared attribute [XAML Services]"
  - "Shared attribute in XAML [XAML Services]"
ms.assetid: c8cff434-2785-405f-9f95-16deb34c9e64
caps.latest.revision: 16
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 16
---
# x:Shared Attribute
Se impostato su `false`, modifica il comportamento di recupero delle risorse di WPF. Pertanto, le richieste per la risorsa attribuita creeranno una nuova istanza per ciascuna richiesta, anziché condividere la stessa istanza per tutte le richieste.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<ResourceDictionary>  
  <object x:Shared="false".../>  
</ResourceDictionary>  
```  
  
## Note  
 `x:Shared` è mappato allo spazio dei nomi XAML del linguaggio XAML ed è riconosciuto come un elemento di linguaggio XAML valido dai servizi XAML di .NET Framework e dai relativi lettori XAML.  Tuttavia, le funzionalità dichiarate di `x:Shared` sono attinenti solo per le applicazioni WPF e per il parser XAML WPF.  In WPF, `x:Shared` è utile come attributo solo quando applicato a un oggetto che esiste all'interno di un oggetto <xref:System.Windows.ResourceDictionary> WPF.  Gli altri utilizzi non generano eccezioni di analisi o altri errori, ma non hanno effetto.  
  
 Il significato di `x:Shared` non è specificato nella specifica del linguaggio XAML.  Altre implementazioni XAML, quali quelle che compilano sui Servizi XAML di .NET Framework, non forniscono necessariamente supporto per condivisione di risorse.  Tali implementazioni XAML potrebbero fornire un comportamento simile nel framework di supporto che utilizza i valori `x:Shared`.  
  
 In WPF, la condizione `x:Shared` predefinita per le risorse è `true`.  Tale condizione indica che qualsiasi richiesta della risorsa data restituisce sempre la stessa istanza.  
  
 La modifica di un oggetto restituito tramite un'API di risorse, come <xref:System.Windows.FrameworkElement.FindResource%2A>, o la modifica diretta di un oggetto all'interno di un oggetto <xref:System.Windows.ResourceDictionary>, modifica la risorsa originale.  Se i riferimenti a quella risorsa erano riferimenti alla risorsa dinamica, gli utenti di quella risorsa otterranno la risorsa modificata.  
  
 Se i riferimenti alla risorsa erano riferimenti alla risorsa statica, le modifiche alla risorsa dopo il tempo di elaborazione [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] sono irrilevanti.  Per ulteriori informazioni sui riferimenti a risorse statiche rispetto a quelle dinamiche, vedere [Risorse XAML](../../../ocs/framework/wpf/advanced/xaml-resources.md).  
  
 Raramente `x:Shared="true"` è specificato in modo esplicito, in quanto si tratta già di un valore predefinito.  Non c'è equivalente del codice diretto per `x:Shared` nel modello a oggetti WPF; è possibile specificarlo solo in un utilizzo di XAML e deve essere elaborato dal comportamento WPF predefinito o in un flusso del nodo XAML intermedio sul percorso di caricamento, se viene elaborato utilizzando i Servizi XAML di .NET Framework e i lettori XAML.  
  
 L'attributo `x:Shared="false"` può essere utilizzato quando si definisce una classe derivata <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> come risorsa, quindi si introduce la risorsa dell'elemento in un modello di contenuto.  `x:Shared="false"` consente di introdurre più volte una risorsa dell'elemento nella stessa raccolta \(ad esempio un oggetto <xref:System.Windows.Controls.UIElementCollection>\).  Senza `x:Shared="false"` tale operazione non sarebbe valida, in quanto la raccolta applica l'unicità del contenuto.  Tuttavia, il comportamento di `x:Shared="false"` crea un'altra istanza identica della risorsa, invece che restituire la stessa istanza.  
  
 Un altro scenario `x:Shared="false"` in cui è possibile utilizzare una risorsa <xref:System.Windows.Freezable> per i valori di animazione ma si decide di modificare la risorsa per singola animazione.  
  
 Per la gestione di stringa di `false` non viene effettuata alcuna distinzione tra maiuscole e minuscole.  
  
 In WPF, l'attributo `x:Shared` è valido solo nelle seguenti condizioni:  
  
-   L'oggetto <xref:System.Windows.ResourceDictionary> che contiene gli elementi con l'attributo `x:Shared` deve essere compilato.  L'oggetto <xref:System.Windows.ResourceDictionary> non può essere presente all'interno della sintassi libera XAML né essere utilizzato per i temi.  
  
-   L'oggetto <xref:System.Windows.ResourceDictionary> che contiene gli elementi non deve essere annidato in un altro oggetto <xref:System.Windows.ResourceDictionary>.  Ad esempio, non è possibile utilizzare l'attributo `x:Shared` per gli elementi di un oggetto <xref:System.Windows.ResourceDictionary> che si trova all'interno di un oggetto <xref:System.Windows.Style> che è già un elemento <xref:System.Windows.ResourceDictionary>.  
  
## Vedere anche  
 <xref:System.Windows.ResourceDictionary>   
 [Risorse XAML](../../../ocs/framework/wpf/advanced/xaml-resources.md)   
 [Elementi di base](../../../ocs/framework/wpf/advanced/base-elements.md)