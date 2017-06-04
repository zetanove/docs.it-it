---
title: "x:Code Intrinsic XAML Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Code"
  - "x:Code"
  - "xCode"
helpviewer_keywords: 
  - "Code directive in XAML [XAML Services]"
  - "x:Code XAML directive element [XAML Services]"
  - "XAML [XAML Services], x:Code directive element"
ms.assetid: 87986b13-1a2e-4830-ae36-15f9dc5629e8
caps.latest.revision: 19
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 19
---
# x:Code Intrinsic XAML Type
Consente di posizionare il codice all'interno di una produzione XAML.  Tale codice può essere compilato da qualsiasi implementazione del processore XAML che compila XAML o lasciato nella produzione XAML per gli utilizzi successivi, come interpretazione dal runtime.  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<x:Code>  
   // code instructions, usually enclosed by CDATA...  
</x:Code>  
```  
  
## Note  
 Il codice presente nell'elemento della direttiva XAML `x:Code` viene comunque interpretato all'interno degli spazi dei nomi XAML generici forniti.  Pertanto, generalmente è necessario includere il codice utilizzato per `x:Code` all'interno di un segmento `CDATA`.  
  
 `x:Code` non può essere utilizzato per tutti i possibili meccanismi di distribuzione di una produzione XAML.  Nei framework specifici \(ad esempio WPF\), il codice deve essere compilato.  Negli altri framework, l'utilizzo `x:Code` potrebbe essere generalmente impedito.  
  
 Per i framework che consentono un contenuto `x:Code` gestito, il compilatore di linguaggio corretto da utilizzare per il contenuto `x:Code` viene determinato tramite le impostazioni e le destinazioni del progetto che lo contiene utilizzato per compilare l'applicazione.  
  
## Note sull'utilizzo di WPF  
 Il codice dichiarato all'interno di `x:Code` per WPF dispone di molte limitazioni rilevanti:  
  
-   L'elemento della direttiva `x:Code` deve essere un elemento figlio diretto dell'elemento radice della produzione XAML.  
  
-   [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md) deve essere disponibile nell'elemento radice padre.  
  
-   Il codice posizionato all'interno di `x:Code` sarà trattato dalla compilazione come parte dell'ambito della classe parziale già in corso di creazione per quella pagina XAML.  Pertanto, tutti i codici definiti devono essere membri o variabili di quella classe parziale.  
  
-   È possibile definire classi aggiuntive soltanto se si annida una classe all'interno della classe parziale \(l'annidamento è consentito ma non è comune perché non è possibile fare riferimento alle classi annidate in XAML\).  Gli spazi dei nomi CLR diversi da quelli utilizzati per la classe parziale esistente non possono essere definiti o aggiunti.  
  
-   I riferimenti alle entità di codice esterne allo spazio dei nomi CLR della classe parziale devono essere completi.  Se i membri dichiarati sono override dei membri sottoponibili a override della classe parziale, è necessario specificarli con la parola chiave di override specifica del linguaggio.  Se i membri dichiarati nell'ambito di `x:Code` sono in conflitto con i membri della classe parziale creata da XAML, in modo il compilatore possa segnalare il conflitto, il file XAML non potrà essere compilato o caricato.  
  
## Vedere anche  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [Code\-behind e XAML in WPF](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)