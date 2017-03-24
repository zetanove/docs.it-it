---
title: "Questa applicazione a istanza singola non è riuscito a connettersi all&quot;istanza originale | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrAppModel_SingleInstanceCantConnect
ms.assetid: 7c2c0cee-02a1-4157-be03-39d18e18408f
caps.latest.revision: 12
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 17a3ecd69e0e0974b2a8fc50090097b93dc0def3
ms.lasthandoff: 03/13/2017

---
# <a name="this-single-instance-application-could-not-connect-to-the-original-instance"></a>Impossibile connettere l'applicazione a istanza singola con l'istanza originale
Impossibile connettere l'applicazione a istanza singola con l'istanza originale. Alcune possibili cause di questo problema sono le seguenti:  
  
-   L'istanza originale attualmente non risponde.  
  
-   L'applicazione non dispone di autorizzazioni per la creazione di oggetti del kernel. Per ulteriori informazioni sugli oggetti kernel, vedere [mutex](http://msdn.microsoft.com/library/9dd06e25-12c0-4a9e-855a-452dc83803e2).  
  
     Il nome base degli oggetti del kernel deriva dalla concatenazione del GUID dell'assembly, del numero di versione principale e del numero di versione secondario. Il nome base ad esempio potrebbe essere `3639f15d-9547-43da-8145-60da347829915.1`.  
  
## <a name="to-correct-this-error-when-developing-the-application"></a>Per correggere questo errore quando si sviluppa l'applicazione  
  
1.  Verificare che l'applicazione non passi allo stato di non reattività.  
  
2.  Verificare che l'applicazione abbia autorizzazioni sufficienti per creare oggetti kernel.  
  
3.  Riavviare l'istanza originale dell'applicazione.  
  
4.  Riavviare il computer per cancellare i processi che stanno usando la risorsa necessaria per la connessione all'istanza originale.  
  
5.  Prendere nota delle circostanze in cui si è verificato l'errore e chiamare il Servizio supporto tecnico Microsoft.  
  
## <a name="see-also"></a>Vedere anche  
 [NIB: Procedura: specificare il comportamento Instancing di un'applicazione (Visual Basic)](http://msdn.microsoft.com/en-us/48539ad8-d960-4210-beab-ee65f6c6dc6e)   
 [Nozioni di base del debugger](https://docs.microsoft.com/visualstudio/debugger/debugger-basics)   
 [Supporto tecnico di preparazione e accessibilità](http://msdn.microsoft.com/en-us/14e1d293-7b6d-40a6-bf3e-a92f8ee6c88c)
