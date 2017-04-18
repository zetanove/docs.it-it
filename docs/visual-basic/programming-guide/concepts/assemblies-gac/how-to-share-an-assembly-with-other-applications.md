---
title: 'Procedura: condividere un Assembly con altre applicazioni (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 5388aedc-cb42-4622-8b70-8e701eee057a
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8065a66c8f7c7b9ccb9125b060b0c03cde273482
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-share-an-assembly-with-other-applications-visual-basic"></a>Procedura: condividere un Assembly con altre applicazioni (Visual Basic)
Gli assembly possono essere privati o condivisi: per impostazione predefinita, la maggior parte dei programmi semplici sono composti da un assembly privato perché non sono progettati per essere utilizzato da altre applicazioni.  
  
 Per condividere un assembly con altre applicazioni, deve essere inserito nel [Global Assembly Cache](http://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202) (GAC).  
  
### <a name="sharing-an-assembly"></a>Condivisione di un assembly  
  
1.  Creare l'assembly. Per ulteriori informazioni, vedere [creazione di assembly](http://msdn.microsoft.com/library/54832ee9-dca8-4c8b-913c-c0b9d265e9a4).  
  
2.  Assegnare un nome sicuro all'assembly. Per ulteriori informazioni, vedere [procedura: firmare un Assembly con un nome sicuro](http://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67).  
  
3.  Assegnare le informazioni sulla versione per l'assembly. Per ulteriori informazioni, vedere [il controllo delle versioni di Assembly](https://msdn.microsoft.com/library/51ket42z).  
  
4.  Aggiungere l'assembly nella Global Assembly Cache. Per ulteriori informazioni, vedere [procedura: installare un Assembly nella Global Assembly Cache](http://msdn.microsoft.com/library/a7e6f091-d02c-49ba-b736-7295cb0eb743).  
  
5.  Accedere ai tipi contenuti nell'assembly dalle altre applicazioni. Per ulteriori informazioni, vedere [procedura: fare riferimento a un Assembly con nomi sicuri](http://msdn.microsoft.com/library/4c6a406a-b5eb-44fa-b4ed-4e95bb95a813).  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione](../../../../visual-basic/programming-guide/concepts/index.md)
 [assembly e Global Assembly Cache (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Programmazione con assembly](http://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)
