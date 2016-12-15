---
title: "Delimitatori per i tag della documentazione (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/** */ (delimitatori per tag di documentazione) (C#)"
  - "/// (delimitatore per documentazione) (C#)"
  - "XML [C#], delimitatori"
ms.assetid: 9b2bdd18-4f5c-4c0b-988e-fb992e0d233e
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Delimitatori per i tag della documentazione (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'utilizzo dei commenti XML relativi alla documentazione richiede la specifica di delimitatori per indicare al compilatore il punto di inizio e di fine di un commento relativo alla documentazione.  I tipi di delimitatore utilizzabili con i tag della documentazione XML sono:  
  
 `///`  
 Delimitatore di singola riga.  Si tratta del formato riportato negli esempi della documentazione e utilizzato per i modelli dei progetti Visual C\#.  Se dopo il delimitatore è presente un carattere di spazio vuoto, quest'ultimo non è incluso nell'output XML.  
  
> [!NOTE]
>  Nell'IDE di Visual Studio è inclusa una funzionalità chiamata Modifica intelligente dei commenti che consente di inserire automaticamente i tag \<summary\> e \<\/summary\> e di spostare il cursore all'interno di questi tag dopo aver digitato il delimitatore `///` nell'editor di codice.  Tale funzione è accessibile dalla [Opzioni, Editor di testo, C\#, Formattazione](/visual-studio/ide/reference/options-text-editor-csharp-formatting) della pagina delle proprietà del progetto.  
  
 `/** */`  
 Delimitatori su più righe.  
  
 Quando si utilizzano i delimitatori `/** */`, è necessario rispettare determinate regole di formattazione.  
  
-   Sulla riga contenente il delimitatore `/**`  se la parte restante della riga è rappresentata da uno spazio vuoto, la riga non viene elaborata per i commenti.  Se il primo carattere dopo il delimitatore `/**` è uno spazio vuoto, tale spazio vuoto viene ignorato e il resto della riga viene elaborato.  In caso contrario, l'intero testo della riga dopo il delimitatore `/**` viene elaborato come parte del commento.  
  
-   Se sulla riga contenente il delimitatore `*/` sono presenti solo spazi vuoti fino al delimitatore `*/`, la riga viene ignorata.  In caso contrario, il testo contenuto nella riga fino al delimitatore `*/` viene elaborato come parte del commento, in base alle regole dei criteri di ricerca descritte nel punto che segue.  
  
-   Per le righe successive a quella che inizia con il delimitatore `/**`, il compilatore cerca criteri comuni all'inizio di ogni riga.  Il modello può essere costituito da uno spazio vuoto facoltativo e un asterisco \(`*`\), seguiti da altri spazi vuoti facoltativi.  Se trova un modello comune all'inizio di ogni riga che non inizia con il delimitatore `/**` o `*/`, il compilatore ignora tale modello per ogni riga.  
  
 Negli esempi seguenti vengono illustrate queste regole.  
  
-   La sola parte del commento riportato di seguito che verrà elaborata è la riga che inizia con `<summary>`.  I tre formati di tag producono gli stessi commenti.  
  
    ```  
    /** <summary>text</summary> */   
  
    /**   
    <summary>text</summary>   
    */   
  
    /**   
     * <summary>text</summary>   
    */  
  
    ```  
  
-   Il compilatore identifica il modello comune " \* " all'inizio della seconda e della terza riga.  Il modello non è incluso nell'output.  
  
    ```  
    /**   
     * <summary>   
     * text </summary>*/   
    ```  
  
-   Il compilatore non trova alcun modello comune nel commento seguente poiché il secondo carattere nella terza riga non è un asterisco.  Di conseguenza, tutto il testo contenuto nella seconda e nella terza riga viene elaborato come parte del commento.  
  
    ```  
    /**   
     * <summary>   
       text </summary>  
    */   
    ```  
  
-   Nel seguente commento non viene rilevato alcun criterio per due motivi.  Anzitutto, il numero di spazi prima dell'asterisco non è coerente.  Inoltre, la quinta riga inizia con una tabulazione, che non corrisponde agli spazi.  Di conseguenza, tutto il testo dalla seconda alla quinta riga verrà elaborato come parte del commento.  
  
    ```  
    /**   
      * <summary>   
      * text   
     *  text2   
        *  </summary>   
    */   
    ```  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Commenti relativi alla documentazione XML](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)   
 [\/doc \(Process Documentation Comments\)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [Commenti relativi alla documentazione XML](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)