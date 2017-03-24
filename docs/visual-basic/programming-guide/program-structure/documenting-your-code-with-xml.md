---
title: Documentazione del codice tramite XML (Visual Basic) | Documenti di Microsoft
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
- XML, documenting code
- XML comments, Visual Basic
- Visual Basic code, documenting with XML
ms.assetid: a0d35dc7-c5f9-4d74-92ff-a1c6f28d5235
caps.latest.revision: 17
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
ms.openlocfilehash: 2ec4907ff96a0861f97de21bdf45662c558d0a95
ms.lasthandoff: 03/13/2017

---
# <a name="documenting-your-code-with-xml-visual-basic"></a>Documentazione del codice tramite XML (Visual Basic)
In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], è possibile documentare il codice tramite XML  
  
## <a name="xml-documentation-comments"></a>Commenti relativi alla documentazione XML  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce un modo semplice per creare automaticamente la documentazione XML per i progetti. È possibile generare automaticamente uno scheletro XML per i tipi e membri e quindi fornire i riepiloghi, la documentazione descrittiva per ogni parametro e altre note. Con l'impostazione appropriata, la documentazione XML viene generata automaticamente in un file XML con lo stesso nome del progetto e l'estensione XML. Per ulteriori informazioni, vedere [/doc](../../../visual-basic/reference/command-line-compiler/doc.md).  
  
 Il file XML può essere utilizzato o diversamente modificato come XML. Questo file si trova nella stessa directory del file di .exe o DLL di output del progetto.  
  
 Documentazione XML inizia con `'''`. L'elaborazione di questi commenti presenta alcune restrizioni:  
  
-   La documentazione deve essere ben formata XML. Se il codice XML non è corretto, viene generato un avviso e il file di documentazione contiene un commento per informare che si è verificato un errore.  
  
-   Gli sviluppatori sono liberi di creare il proprio set di tag. Esiste un set di tag (vedere "Sezioni correlate" in questo argomento). Alcuni dei tag consigliati hanno significati speciali:  
  
    -   Il \<param > tag viene utilizzato per descrivere i parametri. Se utilizzato, il compilatore verificherà che il parametro esista e che tutti i parametri sono descritti nella documentazione. Se la verifica ha esito negativo, il compilatore genera un avviso.  
  
    -   Il `cref` attributo può essere associato a qualsiasi tag per fornire un riferimento a un elemento di codice. Il compilatore verifica l'esistenza di questo elemento di codice. Se la verifica ha esito negativo, il compilatore genera un avviso. Il compilatore rispetta inoltre eventuali `Imports` istruzioni durante la ricerca di un tipo di `cref` attributo.  
  
    -   Il \<riepilogo > tag viene usato da IntelliSense nel [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] per visualizzare informazioni aggiuntive su un tipo o membro.  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per informazioni dettagliate sulla creazione di un file XML con i commenti della documentazione, vedere gli argomenti seguenti:  
  
-   [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)  
  
-   [Tag di commento XML](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)  
  
-   [Elaborazione del file XML](../../../visual-basic/programming-guide/program-structure/processing-the-xml-file.md)  
  
-   [Procedura: Creare documentazione XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)  
  
-   [Strumenti XML in Visual Studio](https://docs.microsoft.com/visualstudio/xml-tools/xml-tools-in-visual-studio)  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di applicazioni con Visual Basic](../../../visual-basic/developing-apps/index.md)   
 [Guida per programmatori Visual Basic](../../../visual-basic/programming-guide/index.md)
