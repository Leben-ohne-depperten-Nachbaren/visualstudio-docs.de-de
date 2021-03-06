---
title: Unterstützende Tools zum Durchsuchen von Symbolen | Microsoft-Dokumentation
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbols, symbol-browsing tools
- browsers, symbol browsers
- symbol-browsing tools
- libraries
- IVsLibrary2 interface, symbol-browsing tools
- IVsSimpleLibrary2 interface, symbol-browsing tools
- symbol-browsing tools, library manager
- symbols
- libraries, symbol-browsing tools
ms.assetid: 70d8c9e5-4b0b-4a69-b3b3-90f36debe880
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ca171fa75adda3deef5b941852fc3e6c648c84c6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723083"
---
# <a name="supporting-symbol-browsing-tools"></a>Unterstützen von Tools zum Durchsuchen von Symbolen
Die Tools " **Objektkatalog**", " **Klassenansicht**", " **Aufrufbrowser** " und " **Find Symbol Results** " bieten Funktionen für die Symbol Suche Diese Tools zeigen hierarchische Struktur Ansichten von Symbolen an und zeigen die Beziehungen zwischen den Symbolen in der Struktur an. Die Symbole können Namespaces, Objekte, Klassen, Klassenmember und andere Sprachelemente darstellen, die in verschiedenen Komponenten enthalten sind. Zu den Komponenten gehören Visual Studio-Projekte, externe .NET Framework Komponenten und Typbibliotheken (. tlb). Weitere Informationen finden Sie unter [Anzeigen der Codestruktur](../../ide/viewing-the-structure-of-code.md).

## <a name="symbol-browsing-libraries"></a>Symbole zum Durchsuchen von Bibliotheken
 Als sprach Implementierung können Sie die Funktionen zum Durchsuchen von Symbolen durch Visual Studio erweitern, indem Sie Bibliotheken erstellen, mit denen die Symbole in ihren Komponenten nachverfolgt werden, und die Listen der Symbole für den Visual Studio-Objekt-Manager über eine Reihe von Schnittstellen bereitstellen. Eine Bibliothek wird von der <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2>-Schnittstelle beschrieben. Der Objekt-Manager von Visual Studio antwortet auf Anforderungen für neue Daten aus den Tools zum Durchsuchen von Symbolen, indem er die Daten aus den Bibliotheken erhält und organisiert. Anschließend werden die Tools mit den angeforderten Daten aufgefüllt oder aktualisiert. Übergeben Sie zum Abrufen eines Verweises auf den Visual Studio-Objekt-Manager <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> die <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> Dienst-ID an die `GetService`-Methode.

 Jede Bibliothek muss beim Visual Studio-Objekt-Manager registriert werden, der die Informationen zu allen Bibliotheken sammelt. Um eine Bibliothek zu registrieren, müssen Sie die <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>-Methode aufzurufen. Abhängig vom Tool, von dem die Anforderung initiiert wird, sucht der Visual Studio-Objekt-Manager die entsprechende Bibliothek und fordert Daten an. Die Daten werden zwischen den Bibliotheken und dem [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Objekt-Manager in Listen von Symbolen übertragen, die von der <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>-Schnittstelle beschrieben werden.

 Der [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Objekt-Manager ist für die regelmäßige Aktualisierung von Symbol Suchtools verantwortlich, um die aktuellen Daten in den Bibliotheken widerzuspiegeln.

 Das folgende Diagramm enthält eine Stichprobe der Schlüsselelemente des Anforderungs-/datenaustauschprozesses zwischen einer Bibliothek und dem Visual Studio-Objekt-Manager. Die Schnittstellen im Diagramm sind Teil einer Anwendung mit verwaltetem Code.

 ![Datenfluss zwischen einer Bibliothek und dem Objekt-Manager](../../extensibility/internals/media/callbrowserdiagram.gif "Callbrowserdiagram")

 Um die Listen der Symbole für den Visual Studio-Objekt-Manager bereitzustellen, müssen Sie die Bibliothek zunächst mit dem Objekt-Manager von Visual Studio registrieren, indem Sie die <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>-Methode aufrufen. Nachdem die Bibliothek registriert wurde, fordert der Visual Studio-Objekt-Manager bestimmte Informationen zu den Funktionen der Bibliothek an. Beispielsweise werden die Bibliotheksflags und unterstützten Kategorien durch Aufrufen der Methoden <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A> und <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A> angefordert. Wenn eines der Tools zu einem bestimmten Zeitpunkt Daten aus dieser Bibliothek anfordert, fordert der Objekt-Manager die Liste der Symbole der obersten Ebene an, indem er die <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A>-Methode aufrufen. Als Antwort stellt die Bibliothek eine Liste von Symbolen her und macht Sie für den Visual Studio-Objekt-Manager über die <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>-Schnittstelle verfügbar. Der [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Objekt-Manager bestimmt, wie viele Elemente in der Liste aufgeführt sind, indem die <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A>-Methode aufgerufen wird. Alle folgenden Anforderungen beziehen sich auf ein angegebenes Element in der Liste und geben die Element Indexnummer in jeder Anforderung an. Der Objekt-Manager von Visual Studio führt die Erfassung der Informationen über den Typ, die Barrierefreiheit und andere Eigenschaften des Elements durch Aufrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A>-Methode fort.

 Der Name des Elements wird durch Aufrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A>-Methode bestimmt, und die Symbol Informationen werden durch Aufrufen der <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A>-Methode angefordert. Das Symbol wird links neben dem Elementnamen angezeigt und zeigt den Typ des Elements, die Barrierefreiheit und andere Eigenschaften an.

 Der [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Objekt-Manager ruft die <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A>-Methode auf, um zu bestimmen, ob ein bestimmtes Listenelement erweiterbar ist und über untergeordnete Elemente verfügt. Wenn die Benutzeroberfläche eine Anforderung zum Erweitern eines Elements sendet, fordert der Objekt-Manager die untergeordnete Liste von Symbolen an, indem die <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A>-Methode aufgerufen wird. Der Prozess wird mit unterschiedlichen Teilen der Struktur fortgesetzt, die Bedarfs gesteuert erstellt wird.

> [!NOTE]
> Um einen nativen Code Symbol Anbieter zu implementieren, verwenden Sie die Schnittstellen <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2> und <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2>.

## <a name="see-also"></a>Siehe auch
- [Gewusst wie: Registrieren einer Bibliothek beim Objekt-Manager](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [Gewusst wie: Verfügbarmachen der Listen von Symbolen, die von der Bibliothek für den Objekt-Manager bereitgestellt werden](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [Gewusst wie: Identifizieren von Symbolen in einer Bibliothek](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)