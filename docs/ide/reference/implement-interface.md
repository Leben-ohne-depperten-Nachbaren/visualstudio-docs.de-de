---
title: Implementieren einer Schnittstelle
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 7d420bd0d42e89476696966f7eda94a19893fc23
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595552"
---
# <a name="implement-an-interface-in-visual-studio"></a>Implementieren einer Schnittstelle in Visual Studio

Diese Codegenerierung gilt für:

- C#

- Visual Basic

**Beschreibung:** Hiermit können Sie sofort den für die Implementierung einer Schnittstelle erforderlichen Code generieren.

**Hintergrund:** Sie möchten von einer Schnittstelle erben.

**Vorteile**: Sie könnten nacheinander alle Schnittstellen manuell implementieren, doch bei diesem Feature werden alle Methodensignaturen automatisch generiert.

## <a name="how-to"></a>Vorgehensweise

1. Platzieren Sie den Cursor auf der Zeile mit einer roten Wellenlinie, die darauf hinweist, dass Sie auf eine Schnittstelle verwiesen, jedoch nicht alle erforderlichen Members implementiert haben.

   - C#:

       ![Hervorgehobener Code – C#](media/interface-highlight-cs.png)

   - Visual Basic:

       ![Hervorgehobener Code in Visual Basic](media/interface-highlight-vb.png)

2. Führen Sie dann eine der folgenden Aktionen aus:

   - **Tastatur**
      - Drücken Sie an einer beliebigen Stelle in einer Zeile **STRG**+ **.** , um das Menü **Schnellaktionen und Refactorings** aufzurufen.
   - **Maus**
      - Führen Sie einen Rechtsklick durch, und klicken Sie auf das Menü **Schnellaktionen und Refactorings**.
      - Zeigen Sie auf die rote Wellenlinie, und klicken Sie auf das ![Fehlerglühbirnensymbol](media/error-bulb.png) das angezeigt wird.
      - Klicken Sie auf die Schaltfläche ![Fehlerglühbirnensymbol](media/error-bulb.png) das am linken Rand angezeigt wird, sofern der Textcursor bereits in der Zeile mit der roten Wellenlinie platziert wurde.

3. Klicken Sie im Dropdownmenü auf **Schnittstelle implementieren**.

   ![Vorschauversion: Implementieren von Schnittstellen](media/interface-preview-cs.png)

   > [!TIP]
   > - Klicken Sie im unteren Bereich des Vorschaufensters auf den Link **Vorschau der Änderungen**, um vor einer Auswahl [alle Änderungen anzuzeigen](../../ide/preview-changes.md), die vorgenommen werden.
   > - Klicken Sie auf die Links **Dokument**, **Projekt** und **Projektmappe** im unteren Bereich des Vorschaufensters, um die richtigen Methodensignaturen für verschiedene Klassen zu erstellen, die die Schnittstelle implementieren.

   Die Methodensignaturen der Schnittstelle werden automatisch erstellt und stehen für die Implementierung zur Verfügung.

   - C#:

       ![Ergebnis der Implementierung einer Schnittstelle in C#](media/interface-result-cs.png)

   - Visual Basic:

       ![Ergebnis der Implementierung einer Schnittstelle in Visual Basic](media/interface-result-vb.png)

   > [!TIP]
   > (Nur C#) Verwenden Sie die Option **Schnittstelle explizit implementieren**, um jeder generierten Methode den Schnittstellennamen voranzustellen und so Namenskonflikte zu vermeiden.
   >
   > ![Schnittstelle explizit implementieren – Ergebnis](media/interface-explicitresult-cs.png);

## <a name="see-also"></a>Siehe auch

- [Codegenerierung](../code-generation-in-visual-studio.md)
- [Vorschau der Änderungen](../../ide/preview-changes.md)
