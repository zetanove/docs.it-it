---
title: 'Procedura: caricare e scaricare gli assembly (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: bbc84236-04b6-4c1b-9672-52773f65a5dc
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 460d3a18fdee74c9b9c49ee465247b5b12d554d8
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-load-and-unload-assemblies-visual-basic"></a>Procedura: caricare e scaricare gli assembly (Visual Basic)
Gli assembly a cui fa riferimento il programma automaticamente verrà caricati in fase di compilazione, ma è anche possibile caricare assembly specifici nel dominio applicazione corrente in fase di esecuzione. Per ulteriori informazioni, vedere [procedura: caricamento di assembly in un dominio applicazione](http://msdn.microsoft.com/library/1432aa2d-bd83-4346-bf3b-a1b7920e2aa9).  
  
 Non è possibile scaricare un singolo assembly senza scaricare tutti i domini applicazione che lo contengono. Anche se l'assembly esce dall'ambito, il file effettivo dell'assembly rimane caricato finché non vengono scaricati tutti i domini applicazione che lo contengono.  
  
 Se si desidera scaricare alcuni assembly ma non altri, è consigliabile creare un nuovo dominio applicazione, l'esecuzione del codice all'interno del dominio e quindi scaricare tale dominio applicazione. Per ulteriori informazioni, vedere [procedura: scaricare un dominio applicazione](http://msdn.microsoft.com/library/f356116d-e415-4f7c-a332-6e6a60227192).  
  
### <a name="to-load-an-assembly-into-an-application-domain"></a>Per caricare un assembly in un dominio applicazione  
  
1.  Utilizzare uno dei numerosi metodi di caricamento di classi <xref:System.AppDomain>e <xref:System.Reflection>.</xref:System.Reflection> </xref:System.AppDomain> Per ulteriori informazioni, vedere [procedura: caricamento di assembly in un dominio applicazione](http://msdn.microsoft.com/library/1432aa2d-bd83-4346-bf3b-a1b7920e2aa9).  
  
### <a name="to-unload-an-application-domain"></a>Per scaricare un dominio applicazione  
  
1.  Non è possibile scaricare un singolo assembly senza scaricare tutti i domini applicazione che lo contengono. Utilizzare il `Unload` metodo <xref:System.AppDomain>per scaricare i domini applicazione.</xref:System.AppDomain> Per ulteriori informazioni, vedere [procedura: scaricare un dominio applicazione](http://msdn.microsoft.com/library/f356116d-e415-4f7c-a332-6e6a60227192).  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti di programmazione](../../../../visual-basic/programming-guide/concepts/index.md)   
 [Gli assembly e Global Assembly Cache (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Procedura: caricare assembly nel dominio applicazione](http://msdn.microsoft.com/library/1432aa2d-bd83-4346-bf3b-a1b7920e2aa9)
