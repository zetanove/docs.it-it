---
title: "Procedura: utilizzare le funzionalit&#224; relative alla documentazione XML (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "documentazione XML [C#]"
  - "Linguaggio c#, funzionalità della documentazione XML"
ms.assetid: 8f33917b-9577-4c9a-818a-640dbbb0b399
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Procedura: utilizzare le funzionalit&#224; relative alla documentazione XML (Guida per programmatori C#)
Nell'esempio seguente fornisce una panoramica di base di un tipo che è stato documentato.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuideDocComments#15](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/how-to-use-the-xml-docum_1.cs)]  
  
 **Questo file XML è stato generato con codice di esempio precedente.**  
**\<? xml versione = "1.0"?>**  
**\< doc>**  
 **\< assembly>**  
 **\< nome>xmlsample \< / name>**  
 **\< / assembly>**  
 **\< membri>**  
 **\< nome del membro = "T:SomeClass">**  
 **\< riepilogo>**  
 **Inserire la documentazione di riepilogo livello di classe. \< / riepilogo>**  
 **\< note>**  
 **Commenti più possono essere associati un tipo o membro**   
 **tramite il tag remarks \< / note>**  
 **\< / membro>**  
 **\< name="F:SomeClass.m_Name membro">**  
 **\< riepilogo>**  
 **Archivio per la proprietà nome \< / riepilogo>**  
 **\< / membro>**  
 **\< nome del membro = "M:SomeClass. #ctor">**  
 **\< riepilogo>il costruttore di classe. \< / riepilogo>**   
 **\< / membro>**  
 **\< name="M:SomeClass.SomeMethod(System.String) membro">**  
 **\< riepilogo>**  
 **Descrizione SomeMethod. \< / riepilogo>**  
 **\< param name = "s"> qui la descrizione del parametro per s \< / param>**  
 **\< seealso cref="T:System.String">**  
 **È possibile utilizzare l'attributo cref in qualsiasi tag per fare riferimento a un tipo o membro**   
 **e il compilatore verificherà l'esistenza del riferimento. \< / seealso>**  
 **\< / membro>**  
 **\< name="M:SomeClass.SomeOtherMethod membro">**  
 **\< riepilogo>**  
 **Un altro metodo. \< / riepilogo>**  
 **\< restituisce>**  
 **Restituire i risultati sono descritti tramite il tag restituisce. \< / restituisce>**  
 **\< seealso cref="M:SomeClass.SomeMethod(System.String)">**  
 **Si noti l'utilizzo dell'attributo cref per fare riferimento a un metodo specifico \< / seealso>**  
 **\< / membro>**  
 **\< name="M:SomeClass.Main(System.String[]) membro">**  
 **\< riepilogo>**  
 **Il punto di ingresso per l'applicazione.**  
 **\< / riepilogo>**  
 **\< param name = "args"> un elenco di argomenti della riga di comando \< / param>**  
 **\< / membro>**  
 **\< name="P:SomeClass.Name membro">**  
 **\< riepilogo>**  
 **Proprietà nome \< / riepilogo>**  
 **\< valore>**  
 **Un tag per il valore viene utilizzato per descrivere il valore della proprietà \< / value>**  
 **\< / membro>**  
 **\< / membri>**  
**\< / doc>**   
## <a name="compiling-the-code"></a>Compilazione del codice  
 Per compilare l'esempio, digitare la riga di comando seguente:  
  
 `csc XMLsample.cs /doc:XMLsample.xml`  
  
 Verrà creato il file XML XMLsample. XML, è possibile visualizzare nel browser o tramite il comando TYPE.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Documentazione XML inizia con / / /. Quando si crea un nuovo progetto, le procedure guidate inserire alcune righe starter / / / in automaticamente. L'elaborazione di questi commenti presenta alcune restrizioni:  
  
-   La documentazione deve essere ben formata XML. Se il codice XML non è corretto, viene generato un avviso e il file di documentazione viene inserito un commento che indica che si è verificato un errore.  
  
-   Gli sviluppatori sono liberi di creare il proprio set di tag. Esiste un set di tag (vedere la sezione ulteriori informazioni). Alcuni dei tag consigliati hanno significati speciali:  
  
    -   Il \< param> tag viene utilizzato per descrivere i parametri. Se utilizzato, il compilatore verificherà che il parametro esista e che tutti i parametri sono descritti nella documentazione. Se la verifica non riesce, il compilatore genera un avviso.  
  
    -   Il `cref` attributo può essere associato a qualsiasi tag per fornire un riferimento a un elemento di codice. Il compilatore verifica l'esistenza di questo elemento di codice. Se la verifica non riesce, il compilatore genera un avviso. Il compilatore rispetta eventuali `using` istruzioni per la ricerca di un tipo di `cref` attributo.  
  
    -   Il \< riepilogo> tag viene utilizzato da IntelliSense in Visual Studio per visualizzare ulteriori informazioni su un tipo o membro.  
  
        > [!NOTE]
        >  Il file XML non fornisce informazioni complete sul tipo e sui membri (ad esempio, non contiene alcuna informazione sul tipo). Per ottenere informazioni complete su un tipo o membro, il file di documentazione deve essere utilizzato con la reflection sul tipo effettivo o sul membro.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori c#](../../../csharp/programming-guide/index.md)   
 [/doc (opzioni del compilatore c#)](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [Commenti di documentazione XML](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)