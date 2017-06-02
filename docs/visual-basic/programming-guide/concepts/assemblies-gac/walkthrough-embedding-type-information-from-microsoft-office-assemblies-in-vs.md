---
title: 'Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office in Visual Studio (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 26b44286-5066-4ad4-8e6a-c24902be347c
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4347ba0e740419b53a1aa662c43933dead107e9c
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-embedding-type-information-from-microsoft-office-assemblies-in-visual-studio-visual-basic"></a>Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office in Visual Studio (Visual Basic)
Se si incorporano informazioni sul tipo in un'applicazione che fa riferimento a oggetti COM, è possibile eliminare la necessità di un assembly di interoperabilità primario (PIA). Inoltre, le informazioni sul tipo incorporato consente di ottenere l'indipendenza dalla versione dell'applicazione. Vale a dire, il programma può essere scritto per utilizzare tipi di più versioni di una libreria COM senza un PIA specifico per ogni versione. Si tratta di uno scenario comune per le applicazioni che utilizzano gli oggetti delle librerie di Microsoft Office. Incorporamento di informazioni sul tipo consente la stessa build di un programma per l'utilizzo delle diverse versioni di Microsoft Office in computer diversi senza dover ridistribuire l'applicazione o assembly di interoperabilità primario per ogni versione di Microsoft Office.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per l'esecuzione di questa procedura sono richiesti i seguenti elementi:  
  
-   Un computer in cui sono installati Visual Studio e Microsoft Excel.  
  
-   Un secondo computer in cui sono installati .NET Framework 4 o versione successiva e una versione diversa di Excel.  
  
##  <a name="BKMK_createapp"></a>Per creare un'applicazione che funziona con più versioni di Microsoft Office  
  
1.  Avviare Visual Studio in un computer in cui è installato Excel.  
  
2.  Nel menu **File** , scegliere **Nuovo**, **Progetto**.  
  
3.  Nel **nuovo progetto** della finestra di dialogo di **tipi di progetto** riquadro, assicurarsi che **Windows** è selezionata. Selezionare **applicazione Console** nel **modelli** riquadro. Nel **nome** immettere `CreateExcelWorkbook`, quindi scegliere il **OK** pulsante. Viene creato il nuovo progetto.  
  
4.  Aprire il menu di scelta rapida per il progetto CreateExcelWorkbook e scegliere **proprietà**. Scegliere il **riferimenti** scheda. Scegliere il pulsante **Aggiungi** .  
  
5.  Nel **.NET** , scegliere la versione più recente della scheda `Microsoft.Office.Interop.Excel`. Ad esempio, **Microsoft Excel 14.0.0.0**. Fare clic sul pulsante **OK** .  
  
6.  Nell'elenco di riferimenti per il **CreateExcelWorkbook** del progetto, selezionare il riferimento per `Microsoft.Office.Interop.Excel` aggiunto nel passaggio precedente. Nel **proprietà** finestra, assicurarsi che il `Embed Interop Types` è impostata su `True`.  
  
    > [!NOTE]
    >  L'applicazione creata in questa procedura dettagliata viene eseguito con diverse versioni di Microsoft Office a causa di informazioni sul tipo di interoperabilità incorporato. Se il `Embed Interop Types` è impostata su `False`, è necessario includere un assembly di interoperabilità primario per ogni versione di Microsoft Office che l'applicazione verrà eseguita con.  
  
7.  Aprire il file Module1. vb. Sostituire il codice nel file con il codice seguente:  
  
    ```vb  
    Imports Excel = Microsoft.Office.Interop.Excel  
  
    Module Module1  
  
        Sub Main()  
            Dim values = {4, 6, 18, 2, 1, 76, 0, 3, 11}  
  
            CreateWorkbook(values, "C:\SampleFolder\SampleWorkbook.xls")  
        End Sub  
  
        Sub CreateWorkbook(ByVal values As Integer(), ByVal filePath As String)  
            Dim excelApp As Excel.Application = Nothing  
            Dim wkbk As Excel.Workbook  
            Dim sheet As Excel.Worksheet  
  
            Try  
                ' Start Excel and create a workbook and worksheet.  
                excelApp = New Excel.Application  
                wkbk = excelApp.Workbooks.Add()  
                sheet = CType(wkbk.Sheets.Add(), Excel.Worksheet)  
                sheet.Name = "Sample Worksheet"  
  
                ' Write a column of values.  
                ' In the For loop, both the row index and array index start at 1.  
                ' Therefore the value of 4 at array index 0 is not included.  
                For i = 1 To values.Length - 1  
                    sheet.Cells(i, 1) = values(i)  
                Next  
  
                ' Suppress any alerts and save the file. Create the directory   
                ' if it does not exist. Overwrite the file if it exists.  
                excelApp.DisplayAlerts = False  
                Dim folderPath = My.Computer.FileSystem.GetParentPath(filePath)  
                If Not My.Computer.FileSystem.DirectoryExists(folderPath) Then  
                    My.Computer.FileSystem.CreateDirectory(folderPath)  
                End If  
                wkbk.SaveAs(filePath)  
        Catch  
  
            Finally  
                sheet = Nothing  
                wkbk = Nothing  
  
                ' Close Excel.  
                excelApp.Quit()  
                excelApp = Nothing  
            End Try  
  
        End Sub  
    End Module  
    ```  
  
8.  Salvare il progetto.  
  
9. Premere CTRL + F5 per compilare ed eseguire il progetto. Verificare che sia stata creata una cartella di lavoro di Excel nella posizione specificata nel codice di esempio: c:\SampleFolder\SampleWorkbook.xls..  
  
##  <a name="BKMK_publishapp"></a>Per pubblicare l'applicazione in un computer in cui è installata una versione diversa di Microsoft Office  
  
1.  Aprire il progetto creato da questa procedura dettagliata in Visual Studio.  
  
2.  Nel **compilare** menu, scegliere **Pubblica CreateExcelWorkbook**. Seguire i passaggi della pubblicazione guidata per creare una versione installabile dell'applicazione. Per ulteriori informazioni, vedere [pubblicazione guidata (sviluppo per Office in Visual Studio)](https://msdn.microsoft.com/library/bb625071).  
  
3.  Installare l'applicazione in un computer in cui sono installati .NET Framework 4 o versione successiva e una versione diversa di Excel.  
  
4.  Al termine dell'installazione, eseguire il programma installato.  
  
5.  Verificare che sia stata creata una cartella di lavoro di Excel nella posizione specificata nel codice di esempio: c:\SampleFolder\SampleWorkbook.xls..  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti in Visual Studio (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-vs.md)   
 [/Link (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/link.md)

