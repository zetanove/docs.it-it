---
title: "Introduction to COM Interop (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "interop assemblies"
  - "COM interop, about COM interop"
ms.assetid: 8bd62e68-383d-407f-998b-29aa0ce0fd67
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Introduction to COM Interop (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il modello COM \(Component Object Model\) consente a un oggetto di esporre le proprie funzionalità ad altri componenti e ad applicazioni host.  Anche se gli oggetti COM sono stati a lungo un elemento essenziale della programmazione Windows, le applicazioni progettate per Common Language Runtime \(CLR\) offrono molti vantaggi.  
  
 Con il tempo, le applicazioni [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] sostituiranno quelle sviluppate con il modello COM.  Fino a quando tale sostituzione non verrà completata, è possibile che sia necessario utilizzare o creare oggetti COM con [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)].  L'*interoperabilità COM* consente di utilizzare gli oggetti COM esistenti in attesa del passaggio a [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  
  
 Se si utilizza [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] per la creazione dei componenti COM, è possibile utilizzare l'interoperabilità COM senza registrazione.  Questo consente di determinare quale versione della DLL viene attivata quando in un computer sono installate più versioni e permette agli utenti finali di utilizzare XCOPY o FTP per copiare l'applicazione in una directory appropriata del proprio computer dalla quale possa essere eseguita.  Per ulteriori informazioni, vedere [Registration\-Free COM Interop](../Topic/Registration-Free%20COM%20Interop.md).  
  
## Codice e dati gestiti  
 Il codice sviluppato per [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] viene definito *codice gestito* e contiene i metadati utilizzati da Common Language Runtime \(CLR\).  I dati utilizzati dalle applicazioni [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] sono definiti *dati gestiti* poiché le attività correlate ai dati, ad esempio l'allocazione e il recupero della memoria e il controllo dei tipi, sono gestite dai servizi di runtime.  Per impostazione predefinita, [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] utilizza dati e codice gestiti. Tuttavia, per accedere al codice e ai dati non gestiti degli oggetti COM è possibile utilizzare assembly di interoperabilità \(descritti più avanti in questa pagina\).  
  
## Assembly  
 Un assembly è il blocco di compilazione principale di un'applicazione [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  Ogni assembly è una raccolta di funzionalità che vengono compilate, associate a una versione e distribuite come una singola unità di implementazione che contiene uno o più file.  Ogni assembly contiene un manifesto assembly.  
  
## Librerie dei tipi e manifesti assembly  
 Le librerie dei tipi descrivono le caratteristiche degli oggetti COM, ad esempio i nomi dei membri e i tipi di dati.  Nelle applicazioni [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] questa funzione viene svolta dai manifesti degli assembly.  Includono informazioni sugli elementi seguenti:  
  
-   Identità, versione, impostazioni cultura e firma digitale dell'assembly.  
  
-   File che formano l'implementazione dell'assembly.  
  
-   Tipi e risorse che compongono l'assembly  inclusi quelli esportati.  
  
-   Dipendenze da altri assembly in fase di compilazione.  
  
-   Autorizzazioni necessarie per la corretta esecuzione dell'assembly.  
  
 Per ulteriori informazioni sugli assembly e sui manifesti degli assembly, vedere [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md).  
  
### Importazione ed esportazione delle librerie dei tipi  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] contiene un'utilità, Tlbimp, che consente di importare informazioni da una libreria dei tipi in un'applicazione [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  Per generare librerie dei tipi da assembly, è possibile utilizzare l'utilità Tlbexp.  
  
 Per informazioni su Tlbimp e Tlbexp, vedere [Tlbimp.exe \(Type Library Importer\)](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md) e [Tlbexp.exe \(Type Library Exporter\)](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md).  
  
## Assembly di interoperabilità  
 Gli assembly di interoperabilità sono assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] che fungono da ponte tra codice gestito e codice non gestito, eseguendo il mapping dei membri degli oggetti COM ai membri gestiti [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] equivalenti.  Gli assembly di interoperabilità creati da [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] gestiscono molti dei dettagli relativi all'utilizzo degli oggetti COM, ad esempio il marshalling di interoperabilità.  
  
## Marshalling di interoperabilità  
 Tutte le applicazioni [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] condividono un insieme di tipi comuni che consentono l'interoperabilità tra oggetti, indipendentemente dal linguaggio di programmazione utilizzato.  I parametri e i valori restituiti degli oggetti COM a volte utilizzano tipi di dati diversi da quelli utilizzati dal codice gestito.  Il termine *marshalling di interoperabilità* indica il processo di assemblaggio dei parametri e dei valori restituiti in tipi di dati equivalenti durante lo spostamento da e verso oggetti COM.  Per ulteriori informazioni, vedere [Interop Marshaling](../Topic/Interop%20Marshaling.md).  
  
## Vedere anche  
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Walkthrough: Implementing Inheritance with COM Objects](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Interoperating with Unmanaged Code](../Topic/Interoperating%20with%20Unmanaged%20Code.md)   
 [Troubleshooting Interoperability](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Tlbimp.exe \(Type Library Importer\)](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)   
 [Tlbexp.exe \(Type Library Exporter\)](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md)   
 [Interop Marshaling](../Topic/Interop%20Marshaling.md)   
 [Registration\-Free COM Interop](../Topic/Registration-Free%20COM%20Interop.md)