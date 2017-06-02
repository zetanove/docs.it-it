---
title: -errorreport (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /errorreport
dev_langs:
- CSharp
helpviewer_keywords:
- -errorreport compiler option [C#]
- errorreport compiler option [C#]
- /errorreport compiler option [C#]
ms.assetid: bd0e7493-b79d-4369-9c3f-ba26ebdfbedf
caps.latest.revision: 35
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 34e7e3b8c6a9f645ec1b359095c2d289afd1370a
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="errorreport-c-compiler-options"></a>/errorreport (opzioni del compilatore C#)
Questa opzione rappresenta un modo pratico per segnalare a Microsoft un errore del compilatore interno C#.  
  
> [!NOTE]
>  In Windows Vista e Windows Server 2008 le impostazioni di segnalazione errori apportate per Visual Studio non eseguono l'override delle impostazioni apportate tramite Segnalazioni errori Windows. Le impostazioni di Segnalazione errori Windows hanno sempre la precedenza sulle impostazioni della funzione di segnalazione errori di Visual Studio.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/errorreport:{ none | prompt | queue | send }  
```  
  
## <a name="arguments"></a>Argomenti  
 **none**  
 Le segnalazioni sugli errori interni del compilatore non verranno raccolte o inviate a Microsoft.  
  
 **prompt**  
 Chiede di inviare una segnalazione quando si riceve un errore interno del compilatore. **prompt** è l'impostazione predefinita se si compila un'applicazione all'interno dell'ambiente di sviluppo.  
  
 **queue**  
 Accoda la segnalazione errori. Se si accede con credenziali amministrative, è possibile segnalare qualsiasi errore dall'ultima volta che è stato effettuato l'accesso. Non verrà richiesto di inviare report di errori più di una volta ogni tre giorni. **queue** è l'impostazione predefinita se si compila un'applicazione dalla riga di comando.  
  
 **send**  
 Invia automaticamente a Microsoft le segnalazioni di errori interni del compilatore. Per abilitare questa opzione, è necessario prima di tutto accettare i Criteri per la raccolta dati Microsoft. La prima volta che si specifica **/errorreport:send** con un computer, viene visualizzato un messaggio del compilatore che indirizza a un sito Web contenente questi criteri.  
  
 Questa opzione dipende dalle impostazioni del Registro di sistema. Per informazioni su come impostare i valori appropriati nel Registro di sistema, vedere [How to Turn on Automatic Error Reporting in Visual Studio 2008 Command-line Tools](http://go.microsoft.com/fwlink/?LinkID=184695) (Come attivare la segnalazione automatica degli errori per gli strumenti da riga di comando di Visual Studio 2008) nel sito Web MSDN.  
  
## <a name="remarks"></a>Note  
 Se il compilatore non è in grado di elaborare un file del codice sorgente, viene restituito un errore interno del compilatore (ICE, Internal Compiler Error). Quando si verifica un ICE, il compilatore non genera né un file di output né informazioni di diagnostica utili per correggere il codice.  
  
 Nelle versioni precedenti, quando si riceveva un ICE si riceveva anche l'invito a contattare il Servizio supporto tecnico Microsoft per segnalare il problema. Con **/errorreport** è possibile fornire informazioni sugli errori interni del compilatore al team Visual C#. Le segnalazioni degli errori consentono di migliorare le versioni future del compilatore.  
  
 La capacità di un utente di inviare report dipende dalle autorizzazioni relative ai criteri utente e computer.  
  
 Per altre informazioni sul debugger degli errori, vedere [Descrizione dello strumento Dr. Watson per Windows (Drwtsn32.exe)](http://go.microsoft.com/fwlink/?LinkId=147286).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto. Per altre informazioni, vedere [Pagina Compilazione, Creazione progetti (C#)](https://docs.microsoft.com/visualstudio/ide/reference/build-page-project-designer-csharp).  
  
2.  Fare clic sulla pagina della proprietà **Compilazione**.  
  
3.  Fare clic su **Avanzate** .  
  
4.  Modificare la proprietà **Segnalazione errori interni del compilatore**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.ErrorReport%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni del compilatore C#](../../../csharp/language-reference/compiler-options/index.md)
