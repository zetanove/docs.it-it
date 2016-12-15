---
title: "Procedura: utilizzare argomenti denominati e facoltativi nella programmazione di Office (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "argomenti denominati e facoltativi [C#], programmazione Office"
  - "argomenti denominati [C#], programmazione Office"
  - "argomenti facoltativi [C#], programmazione Office"
ms.assetid: 65b8a222-bcd8-454c-845f-84adff5a356f
caps.latest.revision: 34
caps.handback.revision: 34
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: utilizzare argomenti denominati e facoltativi nella programmazione di Office (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Gli argomenti denominati e gli argomenti facoltativi, introdotti in [!INCLUDE[csharp_dev10_long](../../../csharp/programming-guide/classes-and-structs/includes/csharp_dev10_long_md.md)], migliorano la praticità, la flessibilità e la leggibilità nella programmazione C\#. Queste funzionalità, inoltre, semplificano notevolmente l'accesso alle interfacce COM, quali le API di automazione di Microsoft Office.  
  
 Nell'esempio seguente, il metodo [ConvertToTable](http://go.microsoft.com/fwlink/?LinkId=145378) dispone di sedici parametri che rappresentano le caratteristiche di una tabella, ad esempio il numero di colonne e di righe, la formattazione, i bordi, i tipi di carattere e i colori.  I sedici parametri sono tutti facoltativi, perché in genere non si desidera specificare particolari valori per tutti.  Senza gli argomenti denominati e facoltativi, tuttavia, è necessario specificare un valore o un valore di segnaposto per ogni parametro.  Con gli argomenti denominati e facoltativi, si specificano valori solo per i parametri obbligatori per il progetto.  
  
 Per completare queste procedure, è necessario che sia installato Microsoft Office Word sul computer.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### Per creare una nuova applicazione console  
  
1.  Avviare Visual Studio.  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
3.  Nel riquadro **Categorie di modelli** espandere **Visual C\#**, quindi fare clic su **Windows**.  
  
4.  Verificare che nella parte superiore del riquadro **Modelli** sia visualizzato **.NET Framework 4** nella casella **Versione .NET Framework di destinazione**.  
  
5.  Nel riquadro **Modelli** fare clic su **Applicazione console**.  
  
6.  Digitare un nome per il progetto nel campo **Nome**.  
  
7.  Scegliere **OK**.  
  
     Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
### Per aggiungere un riferimento  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto, quindi scegliere **Aggiungi riferimento**.  Verrà visualizzata la finestra di dialogo **Aggiungi riferimento**.  
  
2.  Nella pagina **.NET** selezionare **Microsoft.Office.Interop.Word** nell'elenco **Nome componente**.  
  
3.  Scegliere **OK**.  
  
### Per aggiungere le direttive using necessarie  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file **Program.cs**, quindi scegliere **Visualizza codice**.  
  
2.  Aggiungere le seguenti direttive `using` all'inizio del file di codice.  
  
     [!code-cs[csProgGuideNamedAndOptional#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_1.cs)]  
  
### Per visualizzare il testo in un documento di Word  
  
1.  Nella classe `Program` in Program.cs aggiungere il metodo seguente per creare un'applicazione di Word e un documento di Word.  Il metodo [Add](http://go.microsoft.com/fwlink/?LinkId=145381) dispone di quattro parametri facoltativi.  In questo esempio vengono utilizzati i valori predefiniti.  Non è pertanto necessario alcun argomento nell'istruzione di chiamata.  
  
     [!code-cs[csProgGuideNamedAndOptional#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_2.cs)]  
  
2.  Aggiungere il codice seguente alla fine del metodo per definire dove visualizzare il testo nel documento e quale testo visualizzare.  
  
     [!code-cs[csProgGuideNamedAndOptional#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_3.cs)]  
  
### Per eseguire l'applicazione  
  
1.  Aggiungere l'istruzione riportata di seguito a Main.  
  
     [!code-cs[csProgGuideNamedAndOptional#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_4.cs)]  
  
2.  Premere CTRL\+F5 per eseguire il progetto.  Verrà visualizzato un documento di Word contenente il testo specificato.  
  
### Per convertire il testo in una tabella  
  
1.  Utilizzare il metodo `ConvertToTable` per racchiudere il testo in una tabella.  Il metodo dispone di sedici parametri facoltativi.  IntelliSense racchiude tra parentesi i parametri facoltativi, come mostrato nell'immagine seguente.  
  
     ![Elenco di parametri per il metodo ConvertToTable.](../../../csharp/programming-guide/classes-and-structs/media/convert_tableparameters.png "Convert\_TableParameters")  
Parametri ConvertToTable  
  
     Gli argomenti denominati e facoltativi consentono di specificare valori esclusivamente per i parametri che si desidera modificare.  Aggiungere il seguente codice alla fine del metodo `DisplayInWord` per creare una tabella semplice.  L'argomento indica che le virgole nella stringa di testo in `range` separano le celle della tabella.  
  
     [!code-cs[csProgGuideNamedAndOptional#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_5.cs)]  
  
     Nelle versioni precedenti di C\# la chiamata a `ConvertToTable` richiede un argomento di riferimento per ogni parametro, come mostrato nel codice seguente.  
  
     [!code-cs[csProgGuideNamedAndOptional#14](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_6.cs)]  
  
2.  Premere CTRL\+F5 per eseguire il progetto.  
  
### Per provare a utilizzare altri parametri  
  
1.  Per modificare la tabella in modo che contenga una colonna e tre righe, sostituire l'ultima riga in `DisplayInWord` con l'istruzione seguente, quindi premere CTRL\+F5.  
  
     [!code-cs[csProgGuideNamedAndOptional#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_7.cs)]  
  
2.  Per specificare un formato predefinito per la tabella, sostituire l'ultima riga in `DisplayInWord` con l'istruzione seguente, quindi premere CTRL\+F5.  Il formato può corrispondere a qualsiasi costante [WdTableFormat](http://go.microsoft.com/fwlink/?LinkId=145382).  
  
     [!code-cs[csProgGuideNamedAndOptional#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_8.cs)]  
  
## Esempio  
 Il codice seguente include l'esempio completo.  
  
 [!code-cs[csProgGuideNamedAndOptional#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-use-named-and-optional-arguments-in-office-programming_9.cs)]  
  
## Vedere anche  
 [Argomenti denominati e facoltativi](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)