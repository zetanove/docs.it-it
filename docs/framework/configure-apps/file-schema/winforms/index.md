---
title: Sezione di configurazione di Windows Form | Microsoft Docs
ms.custom: 
ms.date: 04/07/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6eb142d5-fc98-40e2-9d90-84733f2a27ba
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
translationtype: Human Translation
ms.sourcegitcommit: 9ff485d8791960f24f727cfc60fbc5ab77203a92
ms.openlocfilehash: fc062bf205db5b2f8883785eb2656eb9d3d8ca16
ms.lasthandoff: 04/15/2017

---
# <a name="windows-forms-configuration-section"></a>Sezione di configurazione di Windows Form
Le impostazioni di configurazione di Windows Form consentono a un'app Windows Form di archiviare e recuperare informazioni sulle impostazioni dell'applicazione personalizzate, ad esempio il supporto di più monitor, il supporto di valori DPI alti e altre impostazioni di configurazione predefinite.

Le impostazioni di configurazione dell'applicazione Windows Form sono archiviate in un elemento `System.Windows.Forms.ConfigurationSection` del file di configurazione.

## <a name="syntax"></a>Sintassi

```xml
<configuration>
  \<System.Windows.Forms.ConfigurationSection>
  ...
  \</System.Windows.Forms.ConfigurationSection>
</configuration>
```

## <a name="attributes-and-elements"></a>Attributi ed elementi

Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.

### <a name="attributes"></a>Attributi

Nessuno.

### <a name="child-elements"></a>Elementi figlio

Elemento  |Descrizione |
---------|---------|
[`<add>`](../../../../../docs/framework/configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md) | Aggiunge una chiave per l'impostazione di configurazione con un valore specificato |

### <a name="parent-elements"></a>Elementi padre

Elemento  |Descrizione |
---------|---------|
[\<configuration>](../configuration-element.md) | Elemento radice in ogni file di configurazione usato in Common Language Runtime e nelle applicazioni Windows Form |

## <a name="remarks"></a>Note

A partire da .NET Framework 4.7, l'elemento `<System.Windows.Forms.ConfigurationSection>` consente di configurare le applicazioni Windows Form in modo da sfruttare i vantaggi delle funzionalità aggiunte nelle versioni recenti di .NET Framework. 

L'elemento `<System.Windows.Forms.ConfigurationSection>` può includere uno o più elementi [ `<add>` ](../../../../../docs/framework/configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md) figlio, ognuno dei quali definisce un'impostazione di configurazione specifica.

## <a name="see-also"></a>Vedere anche

[Schema del file di configurazione](../index.md)
[Supporto di valori DPI alti in Windows Form](../../../../../docs/framework/winforms/high-dpi-support-in-windows-forms.md)

