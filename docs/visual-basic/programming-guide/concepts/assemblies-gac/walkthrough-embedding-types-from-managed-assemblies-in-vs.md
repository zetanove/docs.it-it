---
title: 'Procedura dettagliata: Incorporamento dei tipi da assembly in Visual Studio (Visual Basic) gestiti | Documenti di Microsoft'
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
ms.assetid: 56ed12ba-adff-4e9c-a668-7fcba80c4795
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
ms.openlocfilehash: adc58e081cd9b874a841d84b11d92cbffb6ba6b8
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-embedding-types-from-managed-assemblies-in-visual-studio-visual-basic"></a>Procedura dettagliata: Incorporamento dei tipi da assembly gestiti in Visual Studio (Visual Basic)
Se si incorporano informazioni sul tipo da un assembly gestito sicuro, è possibile un'associazione debole dei tipi in un'applicazione per ottenere l'indipendenza dalla versione. Vale a dire, il programma può essere scritto per utilizzare tipi di più versioni di una libreria gestita senza dover ricompilare per ogni versione.  
  
 L'incorporamento dei tipi viene spesso utilizzato con l'interoperabilità COM, ad esempio un'applicazione che utilizza gli oggetti di automazione di Microsoft Office. Incorporamento di informazioni sul tipo consente la stessa build di un programma per l'utilizzo delle diverse versioni di Microsoft Office in computer diversi. Tuttavia, è possibile utilizzare anche incorporamento dei tipi con una soluzione completamente gestita.  
  
 Informazioni sul tipo possono essere incorporati da un assembly che ha le caratteristiche seguenti:  
  
-   L'assembly espone almeno un'interfaccia pubblica.  
  
-   Le interfacce incorporate vengono annotate con un `ComImport` attributo e un `Guid` attributo (e un GUID univoco).  
  
-   L'assembly viene annotato con il `ImportedFromTypeLib` attributo o `PrimaryInteropAssembly` attributo e un livello di assembly `Guid` attributo. (Per impostazione predefinita, i modelli di progetto Visual Basic includono un livello di assembly `Guid` attributo.)  
  
 Dopo aver specificato le interfacce pubbliche che possono essere incorporate, è possibile creare classi di runtime che implementano tali interfacce. Un programma client può quindi incorporare le informazioni sul tipo per tali interfacce in fase di progettazione facendo riferimento all'assembly che contiene le interfacce pubbliche e l'impostazione di `Embed Interop Types` proprietà di riferimento su `True`. Ciò equivale a utilizzando il compilatore della riga di comando e fare riferimento all'assembly utilizzando il `/link` l'opzione del compilatore. Il programma client può quindi caricare le istanze degli oggetti di runtime tipizzati come tali interfacce. Se si crea una nuova versione dell'assembly con nome sicuro di runtime, il programma client non devono essere ricompilate con l'assembly di runtime aggiornato. Al contrario, il programma client continua a utilizzare qualsiasi versione di assembly di runtime è disponibile, utilizzando le informazioni sul tipo incorporato per le interfacce pubbliche.  
  
 Poiché la funzione principale di incorporamento dei tipi è supporta l'incorporamento di informazioni sui tipi da assembly di interoperabilità COM, le limitazioni seguenti si applicano quando si incorporano informazioni sul tipo in una soluzione completamente gestita:  
  
-   Solo gli attributi specifici per l'interoperabilità COM sono incorporati. altri attributi vengono ignorati.  
  
-   Se un tipo utilizza parametri generici e il tipo del parametro generico è un tipo incorporato, è Impossibile utilizzare tale tipo attraverso un limite di assembly. Esempi di oltrepassare il limite di un assembly chiama un metodo da un altro assembly o un tipo deriva da un tipo definito in un altro assembly.  
  
-   Le costanti non sono incorporate.  
  
-   La <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>classe non supporta un tipo incorporato come chiave.</xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> È possibile implementare un tipo di dizionario per supportare un tipo incorporato come chiave.  
  
 In questa procedura dettagliata, verranno effettuate le operazioni seguenti:  
  
-   Creare un assembly con nome sicuro che dispone di un'interfaccia pubblica che contiene informazioni sul tipo che può essere incorporati.  
  
-   Creare un assembly con nome sicuro di runtime che implementa l'interfaccia pubblica.  
  
-   Creare un programma client che incorpora le informazioni sul tipo dell'interfaccia pubblica e crea un'istanza della classe da assembly di runtime.  
  
-   Modificare e ricompilare l'assembly di runtime.  
  
-   Eseguire il programma client per verificare che la nuova versione dell'assembly di runtime viene usata senza dover ricompilare il programma client.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-an-interface"></a>Creazione di un'interfaccia  
  
#### <a name="to-create-the-type-equivalence-interface-project"></a>Per creare il progetto di interfaccia di equivalenza del tipo  
  
1.  In Visual Studio, nel **File** dal menu **New** e quindi fare clic su **progetto**.  
  
2.  Nel **nuovo progetto** della finestra di dialogo di **tipi di progetto** riquadro, assicurarsi che **Windows** è selezionata. Selezionare **libreria di classi** nel **modelli** riquadro. Nel **nome** digitare `TypeEquivalenceInterface`, quindi fare clic su **OK**. Viene creato il nuovo progetto.  
  
3.  In **Esplora**, il file Class1. vb e fare clic su **rinominare**. Rinominare il file in `ISampleInterface.vb` e premere INVIO. Ridenominazione del file verrà anche rinominare la classe come `ISampleInterface`. Questa classe rappresenterà l'interfaccia pubblica per la classe.  
  
4.  Pulsante destro del mouse sul progetto TypeEquivalenceInterface e fare clic su **proprietà**. Fare clic sulla scheda **Compila**. Impostare il percorso di output a un percorso valido sul computer di sviluppo, ad esempio `C:\TypeEquivalenceSample`. Questo percorso verrà utilizzato anche in un passaggio successivo in questa procedura dettagliata.  
  
5.  Durante la modifica delle proprietà del progetto, scegliere il **firma** scheda. Selezionare il **firmare l'assembly** (opzione). Nel **Scegli un file chiave con nome sicuro** elenco, fare clic su ** <New...> **.</New...> Nel **nome file di chiave** digitare `key.snk`. Cancella il **Proteggi file di chiave con una password** casella di controllo. Fare clic su **OK**.  
  
6.  Aprire il file vb. Aggiungere il codice seguente al file di classe ISampleInterface per creare l'interfaccia ISampleInterface.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
7.  Nel **strumenti** menu, fare clic su **crea Guid**. Nel **Crea GUID** la finestra di dialogo, fare clic su **il formato del Registro di sistema** e quindi fare clic su **copia**. Fare clic su **Esci**.  
  
8.  Nel `Guid` attributo, eliminare il GUID di esempio e incollare il GUID copiato dal **Crea GUID** la finestra di dialogo. Rimuovere le parentesi graffe ({}) dal GUID copiato.  
  
9. Nel **progetto** menu, fare clic su **Mostra tutti i file**.  
  
10. In **Esplora**, espandere il **progetto** cartella. Fare doppio clic il file AssemblyInfo. vb. Aggiungere l'attributo seguente al file.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
     Salvare il file.  
  
11. Salvare il progetto.  
  
12. Pulsante destro del mouse sul progetto TypeEquivalenceInterface e fare clic su **Build**. Il file con estensione dll della libreria di classi viene compilato e salvato nel percorso di output di compilazione specificata (ad esempio, C:\TypeEquivalenceSample).  
  
## <a name="creating-a-runtime-class"></a>Creazione di una classe di Runtime  
  
#### <a name="to-create-the-type-equivalence-runtime-project"></a>Per creare il progetto di runtime di equivalenza del tipo  
  
1.  In Visual Studio, nel **File** dal menu **New** e quindi fare clic su **progetto**.  
  
2.  Nel **nuovo progetto** della finestra di dialogo di **tipi di progetto** riquadro, assicurarsi che **Windows** è selezionata. Selezionare **libreria di classi** nel **modelli** riquadro. Nel **nome** digitare `TypeEquivalenceRuntime`, quindi fare clic su **OK**. Viene creato il nuovo progetto.  
  
3.  In **Esplora**, il file Class1. vb e fare clic su **rinominare**. Rinominare il file in `SampleClass.vb` e premere INVIO. Ridenominazione del file consente inoltre di rinominare la classe `SampleClass`. Questa classe implementerà il `ISampleInterface` interfaccia.  
  
4.  Pulsante destro del mouse sul progetto TypeEquivalenceRuntime e fare clic su **proprietà**. Fare clic sulla scheda **Compila**. Impostare il percorso di output nello stesso percorso usato nel progetto TypeEquivalenceInterface, ad esempio, `C:\TypeEquivalenceSample`.  
  
5.  Durante la modifica delle proprietà del progetto, scegliere il **firma** scheda. Selezionare il **firmare l'assembly** (opzione). Nel **Scegli un file chiave con nome sicuro** elenco, fare clic su ** <New...> **.</New...> Nel **nome file di chiave** digitare `key.snk`. Cancella il **Proteggi file di chiave con una password** casella di controllo. Fare clic su **OK**.  
  
6.  Pulsante destro del mouse sul progetto TypeEquivalenceRuntime e fare clic su **Aggiungi riferimento**. Fare clic su di **Sfoglia** scheda e passare alla cartella del percorso di output. Selezionare il file TypeEquivalenceInterface. dll e fare clic su **OK**.  
  
7.  Nel **progetto** menu, fare clic su **Mostra tutti i file**.  
  
8.  In **Esplora**, espandere il **riferimenti** cartella. Selezionare il riferimento TypeEquivalenceInterface. Nella finestra proprietà per il riferimento TypeEquivalenceInterface, impostare il **versione specifica** proprietà **False**.  
  
9. Aggiungere il codice seguente al file di classe SampleClass per creare la classe SampleClass.  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
10. Salvare il progetto.  
  
11. Pulsante destro del mouse sul progetto TypeEquivalenceRuntime e fare clic su **Build**. Il file con estensione dll della libreria di classi viene compilato e salvato nel percorso di output di compilazione specificata (ad esempio, C:\TypeEquivalenceSample).  
  
## <a name="creating-a-client-project"></a>Creazione di un progetto Client  
  
#### <a name="to-create-the-type-equivalence-client-project"></a>Per creare il progetto client di equivalenza del tipo  
  
1.  In Visual Studio, nel **File** dal menu **New** e quindi fare clic su **progetto**.  
  
2.  Nel **nuovo progetto** della finestra di dialogo di **tipi di progetto** riquadro, assicurarsi che **Windows** è selezionata. Selezionare **applicazione Console** nel **modelli** riquadro. Nel **nome** digitare `TypeEquivalenceClient`, quindi fare clic su **OK**. Viene creato il nuovo progetto.  
  
3.  Pulsante destro del mouse sul progetto TypeEquivalenceClient e fare clic su **proprietà**. Fare clic sulla scheda **Compila**. Impostare il percorso di output nello stesso percorso usato nel progetto TypeEquivalenceInterface, ad esempio, `C:\TypeEquivalenceSample`.  
  
4.  Pulsante destro del mouse sul progetto TypeEquivalenceClient e fare clic su **Aggiungi riferimento**. Fare clic su di **Sfoglia** scheda e passare alla cartella del percorso di output. Selezionare il file TypeEquivalenceInterface. dll (non TypeEquivalenceRuntime. dll) e fare clic su **OK**.  
  
5.  Nel **progetto** menu, fare clic su **Mostra tutti i file**.  
  
6.  In **Esplora**, espandere il **riferimenti** cartella. Selezionare il riferimento TypeEquivalenceInterface. Nella finestra proprietà per il riferimento TypeEquivalenceInterface, impostare il **Embed Interop Types** proprietà **True**.  
  
7.  Aggiungere il codice seguente al file Module1. vb per creare il programma client.  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
8.  Premere CTRL + F5 per compilare ed eseguire il programma.  
  
## <a name="modifying-the-interface"></a>Modifica dell'interfaccia  
  
#### <a name="to-modify-the-interface"></a>Per modificare l'interfaccia  
  
1.  In Visual Studio, nel **File** dal menu **aprire**, quindi fare clic su **progetto/soluzione**.  
  
2.  Nel **Apri progetto** la finestra di dialogo, fare clic sul progetto TypeEquivalenceInterface, quindi fare clic su **proprietà**. Fare clic sulla scheda **Applicazione** . Fare clic su di **informazioni sull'Assembly** pulsante. Modifica il **versione dell'Assembly** e **versione File** valori `2.0.0.0`.  
  
3.  Aprire il file vb. Aggiungere la riga di codice seguente all'interfaccia ISampleInterface.  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
     Salvare il file.  
  
4.  Salvare il progetto.  
  
5.  Pulsante destro del mouse sul progetto TypeEquivalenceInterface e fare clic su **Build**. Una nuova versione del file. dll della libreria di classe viene compilata e salvata nel percorso di output di compilazione specificato (ad esempio, C:\TypeEquivalenceSample).  
  
## <a name="modifying-the-runtime-class"></a>Modifica la classe di Runtime  
  
#### <a name="to-modify-the-runtime-class"></a>Per modificare la classe di runtime  
  
1.  In Visual Studio, nel **File** dal menu **aprire**, quindi fare clic su **progetto/soluzione**.  
  
2.  Nel **Apri progetto** finestra di dialogo, fare clic sul progetto TypeEquivalenceRuntime e scegliere **proprietà**. Fare clic sulla scheda **Applicazione** . Fare clic su di **informazioni sull'Assembly** pulsante. Modifica il **versione dell'Assembly** e **versione File** valori `2.0.0.0`.  
  
3.  Aprire il SampleClass.vbfile. Aggiungere le seguenti righe di codice alla classe SampleClass.  
  
```vb  
Public Function GetDate() As DateTime Implements ISampleInterface.GetDate  
    Return Now  
End Function  
```  
  
     Save the file.  
  
4.  Salvare il progetto.  
  
5.  Pulsante destro del mouse sul progetto TypeEquivalenceRuntime e fare clic su **Build**. Una versione aggiornata del file. dll della libreria di classe viene compilata e salvata nel percorso di output di compilazione specificata in precedenza (ad esempio, C:\TypeEquivalenceSample).  
  
6.  In Esplora File, aprire la cartella del percorso di output (ad esempio, C:\TypeEquivalenceSample). Fare doppio clic su TypeEquivalenceClient.exe per eseguire il programma. Il programma rifletterà la nuova versione dell'assembly TypeEquivalenceRuntime senza essere stato ricompilato.  
  
## <a name="see-also"></a>Vedere anche  
 [/Link (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/link.md)   
 [Concetti di programmazione](../../../../visual-basic/programming-guide/concepts/index.md)   
 [Programmazione con assembly](http://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)   
 [Gli assembly e Global Assembly Cache (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)

