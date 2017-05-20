---
title: 'Procedura: Condividere un assembly con altre applicazioni (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: c30e972b-1693-4e05-b115-c31831fdf9f2
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 1e6ddb6fcee23bbabd66d9295c5ff1534140175a
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="how-to-share-an-assembly-with-other-applications-c"></a>Procedura: Condividere un assembly con altre applicazioni (C#)
Gli assembly possono essere privati o condivisi. Per impostazione predefinita, i programmi più semplici sono costituiti da un assembly privato perché non sono destinati ad essere usati in altre applicazioni.  
  
 Per condividerlo con altre applicazioni, un assembly deve essere inserito nella [Global Assembly Cache](../../../../framework/app-domains/gac.md) (GAC).  
  
### <a name="sharing-an-assembly"></a>Condivisione di un assembly  
  
1.  Creare l'assembly. Per altre informazioni, vedere [Creazione degli assembly](../../../../framework/app-domains/create-assemblies.md).  
  
2.  Assegnare all'assembly un nome sicuro. Per altre informazioni, vedere [Procedura: Firmare un assembly con un nome sicuro](../../../../framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).  
  
3.  Assegnare all'assembly le informazioni sulla versione. Per altre informazioni, vedere [Controllo delle versioni degli assembly](https://msdn.microsoft.com/library/51ket42z).  
  
4.  Aggiungere l'assembly alla Global Assembly Cache. Per altre informazioni, vedere [Procedura: installare un assembly nella Global Assembly Cache](../../../../framework/app-domains/how-to-install-an-assembly-into-the-gac.md).  
  
5.  Accedere ai tipi contenuti nell'assembly da altre applicazioni. Per altre informazioni, vedere [Procedura: Aggiungere un riferimento a un assembly con nome sicuro](http://msdn.microsoft.com/library/4c6a406a-b5eb-44fa-b4ed-4e95bb95a813).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)   
 [Programmazione con gli assembly](../../../../framework/app-domains/programming-with-assemblies.md)
