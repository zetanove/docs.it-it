---
title: "Processing the XML File (Visual Basic) | Microsoft Docs"
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
  - "XML comments, parsing [Visual Basic]"
ms.assetid: 78a15cd0-7708-4e79-85d1-c154b7a14a8c
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Processing the XML File (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il compilatore genera una stringa identificativa \(ID\) per ciascun costrutto del codice che contiene tag per la creazione della documentazione.  Per informazioni sull'inserimento di tag nel codice, vedere [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md). L'ID identifica in modo univoco il costrutto.  I programmi che elaborano il file XML sono in grado di utilizzare la stringa ID per identificare il corrispondente elemento metadati\/reflection di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  
  
 Il file XML non è una rappresentazione gerarchica del codice, bensì un normale elenco contenente gli ID generati per ciascun elemento.  
  
 Per generare gli ID, il compilatore applica le regole descritte di seguito.  
  
-   La stringa non deve contenere spazi vuoti.  
  
-   La prima parte della stringa ID specifica il tipo di membro da identificare, con un singolo carattere seguito dai due punti.  Vengono utilizzati i tipi di membri descritti di seguito.  
  
|||  
|-|-|  
|Carattere|Descrizione|  
|N|Spazio dei nomi<br /><br /> Non è possibile aggiungere commenti relativi alla documentazione a uno spazio dei nomi, ma è possibile creare riferimenti CREF a essi, se supportati.|  
|T|tipo: `Class`, `Module`, `Interface`, `Structure`, `Enum`, `Delegate`|  
|F|campo: `Dim`|  
|P|proprietà: `Property`, incluse le proprietà predefinite|  
|M|metodo: `Sub`, `Function`, `Declare`, `Operator`|  
|E|evento: `Event`|  
|\!|stringa di errore<br /><br /> Nella parte restante della stringa vengono fornite informazioni sull'errore.  Il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] genera informazioni sugli errori per i collegamenti che non è possibile risolvere.|  
  
-   La seconda parte della `String` identifica il nome completo dell'elemento, a partire dalla radice dello spazio dei nomi.  Il nome dell'elemento, i tipi che lo contengono e lo spazio dei nomi sono separati da punti.  Se il nome dell'elemento contiene punti, questi verranno sostituiti con il simbolo di cancelletto \(\#\),  in base al presupposto che nessun nome di elemento contiene direttamente il simbolo di cancelletto.  Ad esempio, il nome completo del costruttore `String` è `System.String.#ctor`.  
  
-   Per le proprietà e i metodi, se il metodo ha degli argomenti, verrà incluso di seguito l'elenco degli argomenti racchiuso tra parentesi.  Se non vi sono argomenti, non si utilizzeranno le parentesi.  Gli argomenti sono separati da virgole.  La codifica di ciascun argomento è del tutto simile alla modalità di codifica utilizzata in una firma [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  
  
## Esempio  
 Nel codice seguente viene illustrato come vengono generate le stringhe ID per una classe e i relativi membri:  
  
 [!code-vb[VbVbcnXmlDocComments#10](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/processing-the-xml-file_1.vb)]  
  
## Vedere anche  
 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)   
 [How to: Create XML Documentation](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)