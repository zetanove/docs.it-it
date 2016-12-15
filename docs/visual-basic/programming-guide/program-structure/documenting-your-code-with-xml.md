---
title: "Documenting Your Code with XML (Visual Basic) | Microsoft Docs"
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
  - "XML, documenting code"
  - "XML comments, Visual Basic"
  - "Visual Basic code, documenting with XML"
ms.assetid: a0d35dc7-c5f9-4d74-92ff-a1c6f28d5235
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Documenting Your Code with XML (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è possibile documentare il codice tramite XML  
  
## Commenti relativi alla documentazione XML  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente di creare automaticamente la documentazione XML per i progetti in modo semplice.  È possibile generare automaticamente uno scheletro XML per i tipi e i membri, quindi fornire i riepiloghi, la documentazione descrittiva per ogni parametro e altre note.  Con l'impostazione appropriata, la documentazione XML viene automaticamente generata in un file XML con lo stesso nome del progetto e con estensione XML.  Per ulteriori informazioni, vedere [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md).  
  
 Il file XML può essere utilizzato o diversamente modificato come XML.  Questo file si trova nella stessa directory del file di output EXE o DLL del progetto.  
  
 La documentazione XML inizia con `'''`.  L'elaborazione di questi commenti è regolata da alcune restrizioni:  
  
-   La documentazione deve essere utilizzare formato XML corretto.  Se il formato XML non è corretto, viene visualizzato un messaggio di avviso e nel file di documentazione viene inserito un commento per informare che si è verificato un errore.  
  
-   Gli sviluppatori sono liberi di creare set di tag personalizzati.  Esiste un set di tag consigliato \(vedere "Sezioni correlate" in questo argomento\).  Alcuni dei tag consigliati hanno un significato speciale:  
  
    -   Il tag \<param\> viene utilizzato per descrivere i parametri.  Se utilizzato, il compilatore verifica l'esistenza del parametro e che tutti i parametri siano descritti nella documentazione.  Se la verifica ha esito negativo, viene visualizzato un messaggio di avviso.  
  
    -   L'attributo `cref` può essere associato a qualsiasi tag per fornire un riferimento a un elemento del codice.  Il compilatore verifica l'esistenza dell'elemento del codice.  Se la verifica ha esito negativo, viene visualizzato un messaggio di avviso.  Il compilatore rispetta inoltre eventuali istruzioni `Imports` quando effettua la ricerca di un tipo descritto nell'attributo `cref`.  
  
    -   Il tag \<summary\> viene utilizzato da IntelliSense in [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] per visualizzare ulteriori informazioni su un tipo o un membro.  
  
## Sezioni correlate  
 Per informazioni dettagliate sulla creazione di un file XML con i commenti relativi, vedere gli argomenti elencati di seguito:  
  
-   [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)  
  
-   [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)  
  
-   [Processing the XML File](../../../visual-basic/programming-guide/program-structure/processing-the-xml-file.md)  
  
-   [How to: Create XML Documentation](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)  
  
-   [Strumenti XML in Visual Studio](/visual-studio/xml-tools/xml-tools-in-visual-studio)  
  
## Vedere anche  
 [Sviluppo di applicazioni con Visual Basic](../../../visual-basic/developing-apps/index.md)   
 [Visual Basic Programming Guide](../../../visual-basic/programming-guide/index.md)