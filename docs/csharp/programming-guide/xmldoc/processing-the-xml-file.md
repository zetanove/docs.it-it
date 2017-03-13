---
title: "Elaborazione del file XML (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "XML [C#], elaborazione"
  - "elaborazione XML [C#]"
ms.assetid: 60c71193-9dac-4cd3-98c5-100bd0edcc42
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Elaborazione del file XML (Guida per programmatori C#)
Il compilatore genera una stringa identificativa \(ID\) per ciascun costrutto del codice che contiene tag per la creazione della documentazione.  Per informazioni sull'applicazione di tag al codice, vedere [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md). L'ID identifica in modo univoco il costrutto.  Nei programmi in cui viene elaborato il file XML, l'ID può essere utilizzato per identificare i metadati o gli oggetti Reflection di .NET Framework a cui fa riferimento la documentazione.  
  
 Il file XML non è una rappresentazione gerarchica del codice, bensì un normale elenco contenente un ID generato per ciascun elemento.  
  
 Per generare gli ID, il compilatore applica le regole descritte di seguito.  
  
-   La stringa non deve contenere spazi vuoti.  
  
-   La prima parte della stringa ID specifica il tipo di membro da identificare, con un singolo carattere seguito dai due punti.  Vengono utilizzati i tipi di membri descritti di seguito.  
  
    |Carattere|Descrizione|  
    |---------------|-----------------|  
    |N|Spazio dei nomi<br /><br /> Non è possibile aggiungere commenti relativi alla documentazione a uno spazio dei nomi, ma è possibile creare riferimenti cref ad essi, se supportati.|  
    |T|tipo: classe, interfaccia, struct, enum, delegato|  
    |F|campo|  
    |P|proprietà \(compresi gli indicizzatori o altre proprietà indicizzate\)|  
    |M|metodo \(compresi i metodi speciali, ad esempio costruttori, operatori e così via\)|  
    |E|event|  
    |\!|stringa di errore<br /><br /> Nella parte restante della stringa vengono fornite informazioni sull'errore.  Il compilatore C\# genera informazioni sugli errori per tutti i collegamenti che non è possibile risolvere.|  
  
-   La seconda parte della stringa identifica il nome completo dell'elemento, a partire dalla radice dello spazio dei nomi.  Il nome dell'elemento, i tipi che lo contengono e lo spazio dei nomi sono separati da punti.  Se il nome dell'elemento contiene dei punti, questi verranno sostituiti con il segno di cancelletto \('\#'\),  in base al presupposto che nessun nome di elemento contiene direttamente il segno di cancelletto.  Ad esempio, il nome completo del costruttore String è "System.String.\#ctor".  
  
-   Per le proprietà e i metodi, se il metodo ha degli argomenti, verrà incluso di seguito l'elenco degli argomenti racchiuso tra parentesi.  Se non vi sono argomenti, non si utilizzeranno le parentesi.  Gli argomenti sono separati da virgole.  La codifica di ciascun argomento è del tutto simile alla modalità di codifica utilizzata in una firma .NET Framework.  
  
    -   Tipi base.  I tipi regolari \(ELEMENT\_TYPE\_CLASS o ELEMENT\_TYPE\_VALUETYPE\) vengono rappresentati con il nome completo del tipo.  
  
    -   Tipi intrinseci \(ad esempio, ELEMENT\_TYPE\_I4, ELEMENT\_TYPE\_OBJECT, ELEMENT\_TYPE\_STRING, ELEMENT\_TYPE\_TYPEDBYREF.  ed ELEMENT\_TYPE\_VOID\) sono rappresentati come nome completo del tipo completo corrispondente.  ad esempio System.Int32 o System.TypedReference.  
  
    -   ELEMENT\_TYPE\_PTR viene rappresentato con '\*' dopo il tipo modificato.  
  
    -   ELEMENT\_TYPE\_BYREF viene rappresentato con '@' dopo il tipo modificato.  
  
    -   ELEMENT\_TYPE\_PINNED viene rappresentato con '^' dopo il tipo modificato.  Non viene mai generato dal compilatore C\#.  
  
    -   ELEMENT\_TYPE\_CMOD\_REQ viene rappresentato con '&#124;' seguito dal nome completo della classe di modificatori dopo il tipo modificato.  Non viene mai generato dal compilatore C\#.  
  
    -   ELEMENT\_TYPE\_CMOD\_OPT viene rappresentato con '\!' seguito dal nome completo della classe di modificatori dopo il tipo modificato.  
  
    -   ELEMENT\_TYPE\_SZARRAY viene rappresentato con "\[\]" dopo il tipo di elemento della matrice.  
  
    -   ELEMENT\_TYPE\_GENERICARRAY viene rappresentato con "\[?\]" dopo il tipo di elemento della matrice.  Non viene mai generato dal compilatore C\#.  
  
    -   ELEMENT\_TYPE\_ARRAY viene rappresentato con \[*limite inferiore*:`size`,*limite inferiore*:`size`\], dove il numero di virgole indica il numero di dimensioni \- 1. I limiti inferiori e le dimensioni di ciascuna dimensione, qualora noti, vengono rappresentati con valori decimali.  Se non è specificato alcun valore, il limite o la dimensione inferiore viene omessa.  Se vengono omessi il limite inferiore e la dimensione per una dimensione specifica, anche ':' viene omesso.  Ad esempio, una matrice a due dimensioni con limiti inferiori pari a 1 e dimensioni non specificate viene rappresentata con \[1:,1:\].  
  
    -   ELEMENT\_TYPE\_FNPTR viene rappresentato con "\=FUNC:`type`\(*signature*\)", dove `type` rappresenta il tipo restituito e *signature* identifica gli argomenti del metodo.  Se non vi sono argomenti, le parentesi vengono omesse.  Non viene mai generato dal compilatore C\#.  
  
     I seguenti componenti della firma non vengono rappresentati in quanto non vengono mai utilizzati per differenziare i metodi di overload:  
  
    -   convenzione di chiamata;  
  
    -   tipo restituito;  
  
    -   ELEMENT\_TYPE\_SENTINEL.  
  
-   Limitatamente agli operatori di conversione \(op\_Implicit e op\_Explicit\), il valore restituito del metodo viene codificato come '~' seguito dal tipo restituito, codificato come descritto in precedenza.  
  
-   Nel caso di tipi generici il nome del tipo verrà seguito da un apice inverso e quindi da un numero che indica il numero di parametri di tipo generici.  Di seguito è riportato un esempio:  
  
     `<member name="T:SampleClass`2">` è il tag per un tipo definito come `public class SampleClass\<T, U>`.  
  
     Nel caso di metodi che accettano tipi generici come parametri, i parametri di tipo generici sono caratterizzati da numeri preceduti da apici inversi, ad esempio \`0,\`1.  Ciascun numero rappresenta la notazione della matrice in base zero per i parametri generici del tipo.  
  
## Esempi  
 Negli esempi seguenti viene illustrato come vengono generate le stringhe di ID per una classe e i relativi membri:  
  
 [!code-cs[csProgGuidePointers#21](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/processing-the-xml-file_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [\/doc \(Process Documentation Comments\)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [Commenti relativi alla documentazione XML](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)