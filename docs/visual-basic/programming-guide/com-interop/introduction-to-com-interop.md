---
title: "Introduzione all&quot;interoperabilità COM (Visual Basic) | Documenti di Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- interop assemblies
- COM interop, about COM interop
ms.assetid: 8bd62e68-383d-407f-998b-29aa0ce0fd67
caps.latest.revision: 12
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8866dbadca040c57ed2b59540dd2c341eb81758c
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-com-interop-visual-basic"></a>Introduzione all'interoperabilità COM (Visual Basic)
Il modello COM (Component Object) consente a un oggetto di esporre le proprie funzionalità per gli altri componenti e applicazioni host. Mentre gli oggetti COM sono stati fondamentali della programmazione per molti anni Windows, le applicazioni progettate per common language runtime (CLR) offrono numerosi vantaggi.  
  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]Infine, le applicazioni sostituiranno quelle sviluppate con COM. Fino ad allora, è necessario utilizzare o creare oggetti COM tramite [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]. Interoperabilità COM, o *l'interoperabilità COM*, consente di utilizzare gli oggetti COM esistenti durante la fase di transizione per il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] a proprio piacimento.  
  
 Tramite il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] per creare componenti COM, è possibile utilizzare l'interoperabilità COM senza registrazione. Ciò consente di controllare la versione della DLL viene attivata quando viene installata in un computer, più di una versione e consente agli utenti finali di utilizzare XCOPY o FTP per copiare l'applicazione in una directory appropriata nel computer in cui può essere eseguito. Per ulteriori informazioni, vedere [interoperabilità COM senza registrazione](http://msdn.microsoft.com/library/90f308b9-82dc-414a-bce1-77e0155e56bd).  
  
## <a name="managed-code-and-data"></a>Il codice gestito e dati  
 Il codice sviluppato per il [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] è detto *codice gestito*e contiene i metadati utilizzati da Common Language Runtime. I dati utilizzati dalle [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] applicazioni viene chiamato *dati gestiti* perché il runtime gestisce attività correlate ai dati, ad esempio l'allocazione e il recupero della memoria e dei tipi di controllo. Per impostazione predefinita, [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] utilizza codice gestito e dati, ma è possibile accedere al codice non gestito e dati di oggetti COM tramite assembly di interoperabilità (descritto più avanti in questa pagina).  
  
## <a name="assemblies"></a>Assembly  
 Un assembly costituisce la base di un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] dell'applicazione. È un insieme di funzionalità che vengono compilate, con controllo delle versioni e distribuiti come unità singola implementazione che contiene uno o più file. Ogni assembly contiene un manifesto dell'assembly.  
  
## <a name="type-libraries-and-assembly-manifests"></a>Manifesti dell'Assembly e librerie dei tipi  
 Librerie dei tipi descrivono le caratteristiche di oggetti COM, ad esempio i nomi dei membri e tipi di dati. Manifesti dell'assembly eseguono la stessa funzione per [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] applicazioni. E che comprendono le seguenti informazioni:  
  
-   Identità dell'assembly, versione, impostazioni cultura e firma digitale.  
  
-   File che compongono l'implementazione dell'assembly.  
  
-   Tipi e risorse che compongono l'assembly. Sono inclusi quelli che vengono esportati da esso.  
  
-   Dipendenze in fase di compilazione da altri assembly.  
  
-   Autorizzazioni necessarie per l'assembly venga eseguita correttamente.  
  
 Per ulteriori informazioni sugli assembly e manifesti dell'assembly, vedere [assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md).  
  
### <a name="importing-and-exporting-type-libraries"></a>Importazione ed esportazione delle librerie dei tipi  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]contiene un'utilità, Tlbimp, che consente di importare le informazioni da una libreria dei tipi in un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] dell'applicazione. È possibile generare librerie dei tipi da assembly utilizzando l'utilità Tlbexp.  
  
 Per informazioni su Tlbimp e Tlbexp, vedere [Tlbimp.exe (Type Library Importer)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382) e [Tlbexp.exe (Type Library Exporter)](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d).  
  
## <a name="interop-assemblies"></a>Assembly di interoperabilità  
 Assembly di interoperabilità sono [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] assembly bridge tra gestito e code, i membri dell'oggetto COM mapping equivalente [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] membri gestiti. Assembly di interoperabilità creati da [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)] gestiscono molti dei dettagli relativi all'utilizzo degli oggetti COM, ad esempio il marshalling di interoperabilità.  
  
## <a name="interoperability-marshaling"></a>Il marshalling di interoperabilità  
 Tutti [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] applicazioni condividono un set di tipi comuni che consentono l'interoperabilità tra gli oggetti, indipendentemente dal linguaggio di programmazione utilizzato. I parametri e valori restituiti di oggetti COM in alcuni casi utilizzano tipi di dati che differiscono da quelli utilizzati nel codice gestito. *Il marshalling di interoperabilità* è il processo di creazione dei pacchetti parametri e valori restituiti in tipi di dati equivalenti durante lo spostamento da e verso oggetti COM. Per ulteriori informazioni, vedere [marshalling di interoperabilità](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a).  
  
## <a name="see-also"></a>Vedere anche  
 [Interoperabilità COM](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Procedura dettagliata: Implementazione dell'ereditarietà con gli oggetti COM](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Interoperabilità con codice non gestito](https://msdn.microsoft.com/library/sd10k43k)   
 [Risoluzione dei problemi di interoperabilità](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [Gli assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Tlbimp.exe (Type Library Importer)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)   
 [Tlbexp.exe (Type Library Exporter)](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d)   
 [Marshalling di interoperabilità](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)   
 [Interoperabilità COM senza registrazione](http://msdn.microsoft.com/library/90f308b9-82dc-414a-bce1-77e0155e56bd)
