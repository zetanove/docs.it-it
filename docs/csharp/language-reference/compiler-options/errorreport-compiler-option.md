---
title: "/errorreport (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/errorreport"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-errorreport compiler option [C#]"
  - "errorreport compiler option [C#]"
  - "/errorreport compiler option [C#]"
ms.assetid: bd0e7493-b79d-4369-9c3f-ba26ebdfbedf
caps.latest.revision: 35
caps.handback.revision: 35
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /errorreport (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Questa opzione è un modo pratico per segnalare a Microsoft un errore del compilatore interno C\#.  
  
> [!NOTE]
>  In Windows Vista e Windows Server 2008, le impostazioni di segnalazione errori apportate per Visual Studio non eseguono l'override delle impostazioni apportate tramite Segnalazioni errori Windows.  Le impostazioni di Segnalazione errori Windows hanno la precedenza sulle impostazioni della segnalazione errori di Visual Studio.  
  
## Sintassi  
  
```  
/errorreport:{ none | prompt | queue | send }  
```  
  
## Argomenti  
 **none**  
 Le segnalazioni sugli errori interni del compilatore non verranno raccolte o inviate a Microsoft.  
  
 **prompt**  
 Chiede di inviare una segnalazione quando si riceve un errore interno del compilatore.  **prompt** è l'impostazione predefinita quando un'applicazione viene compilata nell'ambiente di sviluppo.  
  
 **queue**  
 Accoda la segnalazione errori.  Quando si accede con credenziali amministrative, è possibile segnalare qualsiasi errore dall'ultima volta che è stato effettuato l'accesso.  Non sarà richiesto di inviare i rapporti per gli errori più di una volta ogni tre giorni.  **queue** è l'impostazione predefinita quando si compila un'applicazione dalla riga di comando.  
  
 **send**  
 Invia automaticamente a Microsoft le segnalazioni di errori interni del compilatore.  Per abilitare questa opzione, è necessario innanzitutto accettare le Informazioni raccolta dati Microsoft.  La prima volta che si specifica **\/errorreport:send** in un computer, viene visualizzato un messaggio del compilatore che indica un sito Web contenente le Informazioni raccolta dati Microsoft.  
  
 Questa opzione dipende dalle impostazione del Registro di sistema.  Per informazioni su come impostare i valori appropriati nel Registro di sistema, vedere la pagina relativa alla [Modalità di Abilitazione della Segnalazione degli Errori Automatica negli Strumenti da Riga di Comando di Visual Studio 2008](http://go.microsoft.com/fwlink/?LinkID=184695) sul sito Web MSDN.  
  
## Note  
 Viene restituito un errore interno del compilatore \(ICE\) quando non è possibile elaborare un file del codice sorgente.  Quando si verifica un ICE, il compilatore non genera né un file di output né informazioni di diagnostica utili per correggere il codice.  
  
 Nelle versioni precedenti a ogni errore interno del compilatore lo sviluppatore veniva invitato a contattare il Servizio supporto tecnico Microsoft per segnalare il problema.  Con **\/errorreport** è possibile fornire informazioni sugli errori interni del compilatore al team Visual C\#.  Le segnalazioni errori consentono di migliorare le future versioni del compilatore.  
  
 La capacità di un utente di inviare report dipende dalle autorizzazioni relative ai criteri utente e del computer.  
  
 Per ulteriori informazioni sul debugger di errori, vedere [Descrizione di Dr. Watson per lo Strumento di Windows \(Drwtsn32.exe\)](http://go.microsoft.com/fwlink/?LinkId=147286).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  Per ulteriori informazioni, vedere [Pagina Compilazione, Progettazione progetti \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp).  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Fare clic sul pulsante **Avanzate**.  
  
4.  Modificare la proprietà **Segnalazione errore interno del compilatore**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.ErrorReport%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)