---
title: Syntax Farbgebung in einem Legacy Sprachdienst | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ffa3dcadfc7774766c0e76617ce133d2c30ba2aa
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186324"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>Syntaxfarben in einem Legacysprachdienst

Visual Studio verwendet einen Farbgebung-Dienst, um Elemente der Sprache zu identifizieren und mit den angegebenen Farben in einem Editor anzuzeigen.

## <a name="colorizer-model"></a>Farbauswahl Modell
 Der Sprachdienst implementiert die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>-Schnittstelle, die dann von Editoren verwendet wird. Diese Implementierung ist ein separates Objekt vom Sprachdienst, wie in der folgenden Abbildung dargestellt:

 ![Grafik zur SVC-Farbdarstellung](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
> Der Syntax Farb Dienst ist von dem allgemeinen Visual Studio-Mechanismus zum Einfärben von Text getrennt. Weitere Informationen zum allgemeinen [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] Mechanismus zur Unterstützung der Farbgebung finden [Sie unter Verwenden von Schriftarten und Farben](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015).

 Neben der farbliche Farbgebung kann der Sprachdienst benutzerdefinierte kolorierbare Elemente bereitstellen, die vom Editor verwendet werden, indem er darauf anweist, dass er benutzerdefinierte kolorierbare Elemente bereitstellt. Hierzu können Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>-Schnittstelle für das gleiche Objekt implementieren, das die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>-Schnittstelle implementiert. Sie gibt die Anzahl der benutzerdefinierten Kolon-Elemente zurück, wenn der Editor die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A>-Methode aufruft, und gibt ein einzelnes benutzerdefiniertes färb bares Element zurück, wenn der Editor die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>-Methode aufruft.

 Die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>-Methode gibt ein Objekt zurück, das die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>-Schnittstelle implementiert. Wenn der Sprachdienst 24-Bit-oder hohe Farbwerte unterstützt, muss er die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>-Schnittstelle für das gleiche Objekt wie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>-Schnittstelle implementieren.

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>Wie ein VSPackage eine Sprachdienst Farbgebung verwendet

1. Das VSPackage muss den entsprechenden Sprachdienst erhalten, der das Sprachdienst-VSPackage benötigt, um Folgendes zu erreichen:

    1. Verwenden Sie ein Objekt, das die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>-Schnittstelle implementiert, um den Text auszufärben.

         Text wird in der Regel mithilfe eines Objekts angezeigt, das die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>-Schnittstelle implementiert.

    2. Sie erhalten den Sprachdienst, indem Sie den Dienstanbieter des VSPackage für die Sprachdienst-GUID Abfragen. Sprachdienste werden in der Registrierung nach Dateierweiterung identifiziert.

    3. Ordnen Sie den Sprachdienst dem <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> zu, indem Sie dessen <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A>-Methode aufrufen.

2. Das VSPackage kann nun das Farb-Objekt wie folgt abrufen und verwenden:

    > [!NOTE]
    > VSPackages, die den Kern-Editor verwenden, müssen die Farb ersichts Objekte eines sprach Dienstanbieter nicht explizit abrufen. Sobald eine Instanz des Kern-Editors einen passenden Sprachdienst erhält, führt Sie alle hier gezeigten farbliche Aufgaben aus.

    1. Rufen Sie das colorzer-Objekt des sprach Dienstanbieter ab, das die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>implementiert, und <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> Schnittstellen, indem Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>-Methode für das <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>-Objekt des sprach Dienstanbieter aufrufen.

    2. Rufen Sie die <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>-Methode auf, um die farbisierungsinformationen für einen bestimmten Textabschnitt zu erhalten.

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> gibt ein Array von Werten zurück, eines für jedes Zeichen in der Text Spanne, das farbig markiert wird. Bei den Werten handelt es sich um Indizes in einer Tabelle mit Aktivier barem Element, bei der es sich entweder um die standardmäßige Kolon-Elementliste handelt, die vom Kern-Editor verwaltet wird, oder um eine benutzerdefinierte, vom Sprachdienst

    3. Verwenden Sie die farbliche Informationen, die von der <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>-Methode zurückgegeben werden, um den markierten Text anzuzeigen.

> [!NOTE]
> Zusätzlich zur Verwendung der Farbauswahl eines sprach Dienstanbieter kann ein VSPackage auch den allgemeinen Text Farb Mechanismus von Visual Studio verwenden. Weitere Informationen zu diesem Mechanismus finden Sie unter [Verwenden von Schriftarten und Farben](/visualstudio/extensibility/using-fonts-and-colors?view=vs-2015).

## <a name="in-this-section"></a>In diesem Abschnitt
- [Implementieren von Syntaxfarben](../../extensibility/internals/implementing-syntax-coloring.md)

 Erläutert, wie ein Editor auf die Syntax Farbgebung eines sprach Dienstanbieter zugreift und was der Sprachdienst implementieren muss, um Syntax Farben zu unterstützen.

- [Gewusst wie: Verwenden von integrierten einfärbbaren Elementen](../../extensibility/internals/how-to-use-built-in-colorable-items.md)

 Veranschaulicht die Verwendung integrierter kolatyable-Elemente aus dem Sprachdienst.

- [Benutzerdefinierte einfärbbare Elemente](../../extensibility/internals/custom-colorable-items.md)

 Erläutert, wie benutzerdefinierte färb Bare Elemente implementiert werden.