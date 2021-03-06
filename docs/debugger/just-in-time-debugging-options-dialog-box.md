---
title: Just-in-Time, Debuggen, Dialog Feld "Optionen" | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Debugger.JIT
- vs.debug.options.JIT
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Just-In-Time debugging, setting options
- Options dialog box, debugging
ms.assetid: 7f11b2e3-3fb5-449d-b07c-6ecf1d6a487d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c27ec66c8165995c6877b9a9e65802813140c7f2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72731611"
---
# <a name="just-in-time-debugging-options-dialog-box"></a>Just-In-Time, Debuggen, Dialogfeld "Optionen"
Um die Seite **Just-In-Time** zu öffnen, klicken Sie im Menü **Extras** auf **Optionen**. Erweitern Sie im Dialogfeld **Optionen** den Knoten **Debuggen**, und klicken Sie auf **Just-In-Time**. Auf dieser Seite können Sie das Just-In-Time-Debuggen für verwalteten Code, nativen Code und Skripts aktivieren. Weitere Informationen hierzu finden Sie unter [Just-In-Time-Debuggen](../debugger/just-in-time-debugging-in-visual-studio.md).

 Sie können Just-In-Time-Debuggen für folgende Programmtypen aktivieren:

- Verwaltet

- Systemeigen

- Skript

  Just-In-Time-Debuggen ist ein Verfahren zum Debuggen eines Programms, das außerhalb von [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] gestartet wurde. Sie können ein in [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] erstelltes Programm außerhalb der [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]-Umgebung ausführen. Wenn Sie Just-In-Time-Debuggen aktiviert haben, wird bei einem Absturz ein Dialogfeld angezeigt, das Ihnen die Möglichkeit zum Debuggen bietet.

## <a name="associated-warnings"></a>Zugeordnete Warnungen
 Wenn Sie diese Seite des Dialogfelds **Optionen** anzeigen, wird möglicherweise folgende Warnmeldung angezeigt:

 **Ein anderer Debugger hat sich selbst als Just-in-Time-Debugger registriert. Aktivieren Sie zur Reparatur das Just-in-Time-Debugging, oder führen Sie die Visual Studio-Reparatur aus.**

 Diese Meldung wird angezeigt, wenn Sie einen anderen Debugger (möglicherweise eine ältere Version des [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]-Debuggers) als Just-In-Time-Debugger festgelegt haben.

 Eine andere Meldung, die Sie sehen könnten, ist:

 **Registrierungsfehler für Just-in-Time-Debugging erkannt. Aktivieren Sie zur Reparatur das Just-in-Time-Debugging, oder führen Sie die Visual Studio-Reparatur aus.**

 Wenn eine dieser Warnmeldungen angezeigt wird, sind für das Just-In-Time-Debuggen mit [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] Administratorrechte erforderlich, bis Sie das Problem behoben haben. Wenn Sie versuchen, Just-In-Time-Debuggen unter diesen Bedingungen zu aktivieren, obwohl Sie kein Administrator sind, wird die folgende Fehlermeldung angezeigt:

 **Der Zugriff wurde verweigert. Lassen Sie einen Administrator das Just-in-Time-Debuggen aktivieren, oder reparieren Sie die Installation von Visual Studio.**

## <a name="see-also"></a>Siehe auch
- [Debuggen, Dialogfeld "Optionen"](../debugger/debugging-options-dialog-box.md)
- [Gewusst wie: Angeben von Debuggereinstellungen](../debugger/how-to-specify-debugger-settings.md)