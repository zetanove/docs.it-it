---
title: 'Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office (C# ) | Microsoft Docs'
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
ms.assetid: 3320e866-01f1-4b7f-8932-049a7b2d2a9b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b698372d28198cfcd34aef69043334e3fc50ce6d
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-embedding-type-information-from-microsoft-office-assemblies-in-visual-studio-c"></a>Procedura dettagliata: Incorporamento delle informazioni sui tipi da assembly di Microsoft Office in Visual Studio (C#)
Se si incorporano informazioni sui tipi in un'applicazione che fa riferimento a oggetti COM, è possibile eliminare la necessità di un assembly di interoperabilità primario (PIA). Inoltre, le informazioni sui tipi incorporate consentono di ottenere l'indipendenza dalla versione per l'applicazione. Ovvero, il programma può essere scritto in modo da usare tipi di più versioni di una libreria COM senza richiedere un assembly di interoperabilità primario specifico per ogni versione. Si tratta di uno scenario comune per le applicazioni che usano gli oggetti delle librerie di Microsoft Office. L'incorporamento di informazioni sui tipi consente l'uso della stessa build di un programma con delle diverse versioni di Microsoft Office in computer diversi senza dover ridistribuire il programma o l'assembly di interoperabilità primario per ogni versione di Microsoft Office.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per l'esecuzione di questa procedura sono richiesti i seguenti elementi:  
  
-   Un computer in cui sono installati Visual Studio e Microsoft Excel.  
  
-   Un secondo computer in cui sono installati .NET Framework 4 o versione successiva e una versione diversa di Excel.  
  
##  <a name="BKMK_createapp"></a> Per creare un'applicazione che funziona con più versioni di Microsoft Office  
  
1.  Avviare Visual Studio in un computer in cui è installato Excel.  
  
2.  Nel menu **File** , scegliere **Nuovo**, **Progetto**.  
  
3.  Nel riquadro **Tipi di progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata l'opzione **Windows**. Selezionare **Applicazione console** nel riquadro **Modelli**. Nella casella **Nome** immettere `CreateExcelWorkbook`, quindi scegliere il pulsante **OK** . Il nuovo progetto viene creato.  
  
4.  In **Esplora soluzioni** aprire il menu di scelta rapida per la cartella **Riferimenti**e quindi scegliere **Aggiungi riferimento**.  
  
5.  Nella scheda **.NET** scegliere la versione più recente di `Microsoft.Office.Interop.Excel`. Ad esempio, **Microsoft.Office.Interop.Excel 14.0.0.0**. Fare clic sul pulsante **OK** .  
  
6.  Nell'elenco di riferimenti per il progetto **CreateExcelWorkbook** selezionare il riferimento per `Microsoft.Office.Interop.Excel` aggiunto nel passaggio precedente. Nella finestra **Proprietà** verificare che la proprietà `Embed Interop Types` sia impostata su `True`.  
  
    > [!NOTE]
    >  L'applicazione creata in questa procedura dettagliata viene eseguita con diverse versioni di Microsoft Office grazie alle informazioni incorporate sul tipo di interoperabilità. Se la proprietà `Embed Interop Types` è impostata su `False`, è necessario includere un assembly di interoperabilità primario per ogni versione di Microsoft Office con cui verrà eseguita l'applicazione.  
  
7.  Aprire il file **Program.cs**. Sostituire il codice nel file con il codice seguente:  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.IO;  
    using Excel = Microsoft.Office.Interop.Excel;  
  
    namespace CreateExcelWorkbook  
    {  
        class Program  
        {  
            static void Main(string[] args)  
            {  
                int[] values = {4, 6, 18, 2, 1, 76, 0, 3, 11};  
  
                CreateWorkbook(values, @"C:\SampleFolder\SampleWorkbook.xls");  
            }  
  
            static void CreateWorkbook(int[] values, string filePath)  
            {  
                Excel.Application excelApp = null;  
                Excel.Workbook wkbk;  
                Excel.Worksheet sheet;  
  
                try  
                {  
                        // Start Excel and create a workbook and worksheet.  
                        excelApp = new Excel.Application();  
                        wkbk = excelApp.Workbooks.Add();  
                        sheet = wkbk.Sheets.Add() as Excel.Worksheet;  
                        sheet.Name = "Sample Worksheet";  
  
                        // Write a column of values.  
                        // In the For loop, both the row index and array index start at 1.  
                        // Therefore the value of 4 at array index 0 is not included.  
                        for (int i = 1; i < values.Length; i++)  
                        {  
                            sheet.Cells[i, 1] = values[i];  
                        }  
  
                        // Suppress any alerts and save the file. Create the directory   
                        // if it does not exist. Overwrite the file if it exists.  
                        excelApp.DisplayAlerts = false;  
                        string folderPath = Path.GetDirectoryName(filePath);  
                        if (!Directory.Exists(folderPath))  
                        {  
                            Directory.CreateDirectory(folderPath);  
                        }  
                        wkbk.SaveAs(filePath);  
                }  
                catch  
                {  
                }  
                finally  
                {  
                    sheet = null;  
                    wkbk = null;  
  
                    // Close Excel.  
                    excelApp.Quit();  
                    excelApp = null;  
                }  
            }  
        }  
    }  
    ```  
  
8.  Salvare il progetto.  
  
9. Premere CTRL+F5 per compilare ed eseguire il progetto. Verificare che sia stata creata una cartella di lavoro di Excel nel percorso specificato nel codice di esempio: C:\SampleFolder\SampleWorkbook.xls.  
  
##  <a name="BKMK_publishapp"></a> Per pubblicare l'applicazione in un computer in cui è installata una versione diversa di Microsoft Office  
  
1.  Aprire il progetto creato da questa procedura dettagliata in Visual Studio.  
  
2.  Scegliere **Pubblica CreateExcelWorkbook** nel menu **Compila**. Seguire i passaggi della pubblicazione guidata per creare una versione installabile dell'applicazione. Per altre informazioni, vedere [Pubblicazione guidata (sviluppo per Office in Visual Studio)](https://msdn.microsoft.com/library/bb625071).  
  
3.  Installare l'applicazione in un computer in cui sono installati .NET Framework 4 o versione successiva e una versione diversa di Excel.  
  
4.  Al termine dell'installazione eseguire il programma installato.  
  
5.  Verificare che sia stata creata una cartella di lavoro di Excel nel percorso specificato nel codice di esempio: C:\SampleFolder\SampleWorkbook.xls.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti in Visual Studio (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md)   
 [/link (opzioni del compilatore C#)](../../../../csharp/language-reference/compiler-options/link-compiler-option.md)

