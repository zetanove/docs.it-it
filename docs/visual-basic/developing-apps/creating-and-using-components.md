---
title: "Creating and Using Components in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "components [Visual Basic]"
ms.assetid: ee6a4156-73f7-4e9b-8e01-c74c4798b65c
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Creating and Using Components in Visual Basic
[!INCLUDE[vs2017banner](../../csharp/includes/vs2017banner.md)]

Un *componente* è una classe che implementa l'interfaccia <xref:System.ComponentModel.IComponent?displayProperty=fullName> o che deriva direttamente o indirettamente da una classe che implementa <xref:System.ComponentModel.IComponent>.  Un componente [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)] è un oggetto riutilizzabile che interagisce con altri oggetti, consente di esercitare il controllo sulle risorse esterne e fornisce supporto in fase di progettazione.  
  
 Una funzionalità importante dei componenti è che sono progettabili, pertanto una classe che rappresenta un componente può essere utilizzata nell'ambiente di sviluppo integrato di [!INCLUDE[vsprvs](../../csharp/includes/vsprvs_md.md)].  I componenti possono essere aggiunti alla Casella degli strumenti, trascinati e rilasciati su un form nonché modificati su una superficie di progettazione.  Si noti che il supporto base per la fase di progettazione per i componenti è incorporato in [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)]. La fruizione di tale supporto non richiede allo sviluppatore di componenti alcun intervento aggiuntivo.  
  
 I *controlli* sono simili ai componenti poiché anch'essi sono progettabili.  Al contrario dei componenti, tuttavia, i controlli forniscono un'interfaccia utente.  I controlli devono derivare da una delle classi di controlli base: <xref:System.Windows.Forms.Control> e <xref:System.Web.UI.Control>.  
  
## Quando creare un componente  
 Se la classe verrà utilizzata su un'area di progettazione, quale la finestra di progettazione di Windows Form o di Web Form, ma è priva di interfaccia utente, deve essere un componente e implementare <xref:System.ComponentModel.IComponent> oppure derivare da una classe che implementa direttamente o indirettamente <xref:System.ComponentModel.IComponent>.  
  
 Le classi <xref:System.ComponentModel.Component> e <xref:System.ComponentModel.MarshalByValueComponent> sono implementazioni base dell'interfaccia <xref:System.ComponentModel.IComponent>.  La principale differenza fra queste classi risiede nel fatto che la classe <xref:System.ComponentModel.Component> è sottoposta al marshalling per riferimento, mentre la classe <xref:System.ComponentModel.IComponent> al marshalling per valore.  Nell'elenco che segue vengono fornite indicazioni di massima per l'implementazione.  
  
-   Se è necessario sottoporre un componente al marshalling per riferimento, eseguire una derivazione da <xref:System.ComponentModel.Component>.  
  
-   Se è necessario sottoporre un componente al marshalling per valore, eseguire una derivazione da <xref:System.ComponentModel.MarshalByValueComponent>.  
  
-   Se a causa dell'ereditarietà singola non è possile eseguire una derivazione del componente da una delle implementazioni base, implementare <xref:System.ComponentModel.IComponent>.  
  
 Per ulteriori informazioni sul supporto di base in fase di progettazione, vedere [Design\-Time Attributes for Components](../Topic/Design-Time%20Attributes%20for%20Components.md) e [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md).  
  
## Classi di componenti  
 Lo spazio dei nomi <xref:System.ComponentModel> fornisce classi che vengono utilizzate per implementare il comportamento di componenti e controlli in fase di esecuzione e in fase di progettazione.  In questo spazio dei nomi sono comprese le classi base e le interfacce per l'implementazione di convertitori di attributo e tipo, associazioni a origini dati e componenti relativi alle licenze.  
  
 Le principali classi di componenti sono le seguenti:  
  
-   <xref:System.ComponentModel.Component>.  Un'implementazione di base per l'interfaccia <xref:System.ComponentModel.IComponent>.  Questa classe consente di condividere oggetti fra applicazioni diverse.  
  
-   <xref:System.ComponentModel.MarshalByValueComponent>.  Un'implementazione di base per l'interfaccia <xref:System.ComponentModel.IComponent>.  
  
-   <xref:System.ComponentModel.Container>.  L'implementazione di base per l'interfaccia <xref:System.ComponentModel.IContainer>.  Questa classe incapsula zero o più componenti.  
  
 Di seguito sono riportate alcune delle classi utilizzate per le licenze relative ai componenti.  
  
-   <xref:System.ComponentModel.License>.  La classe base astratta per tutte le licenze.  La licenza viene concessa per una specifica istanza di un componente.  
  
-   <xref:System.ComponentModel.LicenseManager>.  Fornisce proprietà e metodi per aggiungere una licenza a un componente e per gestire un oggetto <xref:System.ComponentModel.LicenseProvider>.  
  
-   <xref:System.ComponentModel.LicenseProvider>.  La classe base astratta per l'implementazione di un provider di licenze.  
  
-   <xref:System.ComponentModel.LicenseProviderAttribute>.  Specifica la classe <xref:System.ComponentModel.LicenseProvider> da utilizzare con una classe.  
  
 Classi maggiormente utilizzate per descrivere e rendere permanenti i componenti.  
  
-   <xref:System.ComponentModel.TypeDescriptor>.  Fornisce informazioni sulle caratteristiche di un componente, quali attributi, proprietà ed eventi.  
  
-   <xref:System.ComponentModel.EventDescriptor>.  Fornisce informazioni su un evento.  
  
-   <xref:System.ComponentModel.PropertyDescriptor>.  Fornisce informazioni relative a una proprietà.  
  
## Sezioni correlate  
 [Class vs. Component vs. Control](../Topic/Class%20vs.%20Component%20vs.%20Control.md)  
 Vengono fornite le definizioni di *componente* e *controllo* e illustrate le differenze che esistono fra di essi e le classi.  
  
 [Component Authoring](../Topic/Component%20Authoring.md)  
 Guida di orientamento all'utilizzo dei componenti.  
  
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)  
 Vengono forniti collegamenti a istruzioni dettagliate per la programmazione dei componenti.  
  
 [Component Classes](../Topic/Component%20Classes.md)  
 Vengono descritti gli aspetti che fanno di una classe un componente, alcune modalità per esporre le funzionalità dei componenti, il controllo dell'accesso ai componenti e il controllo della modalità di creazione delle istanze dei componenti.  
  
 [Risoluzione dei problemi relativi alla modifica di controlli e componenti](../Topic/Troubleshooting%20Control%20and%20Component%20Authoring.md)  
 Viene illustrato come risolvere alcuni problemi comuni.  
  
## Vedere anche  
 [How to: Access Design\-Time Support in Windows Forms](../Topic/How%20to:%20Access%20Design-Time%20Support%20in%20Windows%20Forms.md)   
 [How to: Extend the Appearance and Behavior of Controls in Design Mode](../Topic/How%20to:%20Extend%20the%20Appearance%20and%20Behavior%20of%20Controls%20in%20Design%20Mode.md)   
 [How to: Perform Custom Initialization for Controls in Design Mode](../Topic/How%20to:%20Perform%20Custom%20Initialization%20for%20Controls%20in%20Design%20Mode.md)