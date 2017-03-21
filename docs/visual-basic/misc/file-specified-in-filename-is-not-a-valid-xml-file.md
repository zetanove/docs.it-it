---
title: "File specificato nel nome file non è un file XML valido | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
caps.latest.revision: 12
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2fa595ab411fdd300327db9e1fcca1e3156c7eed
ms.lasthandoff: 03/13/2017

---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a>Il file specificato in FileName non è un file XML valido
Il nome file fornito non è un file XML valido. Per specificare la struttura e il contenuto consentito di un documento XML, è possibile usare una definizione DTD (Document Type Definition), uno schema XDR (XML-Data Reduced) o uno schema XSD (XML Schema Definition Language). Gli schemi XSD sono il modo migliore per specificare le grammatiche XML nel [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
> [!NOTE]
>  Nelle precedenti versioni di Visual Studio, **Progettazione XML** è la finestra di progettazione per i dataset tipizzati e lo schema XML. È ancora possibile usare **Progettazione XML** per creare e modificare i file di schema XML. Tuttavia, in [!INCLUDE[vs_current_long](../../csharp/misc/includes/vs_current_long_md.md)], la finestra di progettazione per la creazione e modifica di dataset tipizzati il **Progettazione Dataset**. Per ulteriori informazioni, vedere [creazione e modifica di dataset tipizzati](https://docs.microsoft.com/visualstudio/data-tools/creating-and-editing-typed-datasets).  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Verificare che il nome file fornito sia corretto.  
  
-   Accertarsi che il file specificato contenga XML valido, caricando il file XML che si vuole verificare in **Progettazione XML**. Scegliere **Convalida dati XML** dal menu **XML**. Gli errori sono visualizzati nell' **Elenco attività**.  
  
-   Se il file XML ha uno schema XML associato, verificare che gli elementi appaiano nella struttura definita e che il contenuto dei singoli elementi sia conforme ai tipi di dati dichiarati specificati nello schema.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml></xref:System.Xml>   
 [Procedura: analizzare percorsi di file](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
