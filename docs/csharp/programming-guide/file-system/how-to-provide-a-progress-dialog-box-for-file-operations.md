---
title: "Procedura: fornire una finestra di dialogo dello stato di avanzamento per operazioni su file (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Finestra di dialogo Stato avanzamento) [C#]"
ms.assetid: 01b71fe7-8178-4dc8-aeb1-12053be7b51c
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Procedura: fornire una finestra di dialogo dello stato di avanzamento per operazioni su file (Guida per programmatori C#)
È possibile fornire una finestra di dialogo standard con lo stato di avanzamento delle operazioni sui file in Windows se si utilizza il metodo <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%28System.String%2CSystem.String%2CMicrosoft.VisualBasic.FileIO.UIOption%29> nello spazio dei nomi <xref:Microsoft.VisualBasic?displayProperty=fullName>.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per aggiungere un riferimento in Visual Studio  
  
1.  Nella barra dei menu, scegliere **Progetto**, **Aggiungi riferimento**.  
  
     Viene visualizzata la finestra di dialogo **Gestione riferimenti**.  
  
2.  Nell'area **Assembly** scegliere l'opzione **Framework** se non è già stata selezionata.  
  
3.  Nell'elenco dei nomi, selezionare la casella di controllo **Microsoft.VisualBasic** e quindi scegliere il pulsante **OK** per chiudere la finestra di dialogo.  
  
## Esempio  
 Il seguente codice copia la directory specificata da `sourcePath` nella directory specificata da `destinationPath`.  Questo codice fornisce inoltre una finestra di dialogo standard che mostra il tempo rimanente stimato prima del completamento dell'operazione.  
  
 [!code-cs[csFilesandFolders#11](../../../csharp/programming-guide/file-system/codesnippet/CSharp/how-to-provide-a-progress-dialog-box-for-file-operations_1.cs)]  
  
## Vedere anche  
 [File system e Registro di sistema](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)