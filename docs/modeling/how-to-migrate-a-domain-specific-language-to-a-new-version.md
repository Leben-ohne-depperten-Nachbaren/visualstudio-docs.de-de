---
title: 'Gewusst wie: Migrieren einer domänenspezifischen Sprache zu einer neuen Version'
ms.date: 11/04/2016
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6be4a8205935d131d880923e721e342ea904134d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747554"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>Gewusst wie: Migrieren einer domänenspezifischen Sprache zu einer neuen Version
Sie können Projekte, die domänenspezifische Sprache definieren und verwenden, [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] aus der Version von [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] migrieren, die mit [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] verteilt wurde.

 Ein Migrationstool wird als Teil [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] bereitgestellt. Das Tool konvertiert Visual Studio-Projekte und-Projektmappen, die DSL-Tools verwenden oder definieren.

 Das Migrationstool muss explizit ausgeführt werden: Es wird nicht automatisch gestartet, wenn Sie eine Projekt Mappe in Visual Studio öffnen. Das Tool und das ausführliche Leit Faden Dokument finden Sie unter diesem Pfad:

 **%Programme%\Microsoft Visual Studio 2010 sdk\visualstudiointegration\tools\dsltools\dslprojectionmigrationtool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>Vor dem Migrieren Ihrer DSL-Projekte
 Das Migrationstool ändert Visual Studio-Projektdateien ( **. csproj**) und Projektmappendateien ( **. sln**).

#### <a name="to-prepare-projects-for-migration"></a>So bereiten Sie Projekte für die Migration vor

- Stellen Sie sicher, dass die **csproj** -und **sln** -Dateien geschrieben werden können. Wenn Sie sich unter Quell Code Verwaltung befinden, stellen Sie sicher, dass Sie ausgecheckt sind.

- Erstellen Sie eine Kopie der Ordner, die Sie migrieren möchten.

## <a name="migrating-a-collection-of-projects"></a>Migrieren einer Projekt Sammlung

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>So migrieren Sie DSL-Projekte und-Lösungen zu Visual Studio 2010

1. Starten Sie das DSL-Migrations Tool.

   - Sie können auf das Tool im Windows-Explorer (oder Datei-Explorer) doppelklicken oder das Tool an einer Eingabeaufforderung starten. Das Tool befindet sich an diesem Speicherort:

        **%ProgramFiles%\Microsoft Visual Studio 2010 sdk\visualstudiointegration\tools\dsltools\dslprojectionmigrationtool.exe**

2. Wählen Sie einen Ordner aus, der Projektmappen und Projekte enthält, die Sie konvertieren möchten.

   - Geben Sie den Pfad im Feld am Anfang des Tools ein, oder klicken Sie auf **Durchsuchen**.

     Das Migrationstool zeigt eine Struktur von Projekten an, die DSLs definieren oder verwenden. Die Struktur enthält jedes Projekt, das die Assemblys " **Microsoft. VisualStudio. Modeling. SDK** " oder " **TextTemplating** " verwendet.

3. Überprüfen Sie die Struktur von Projekten, und deaktivieren Sie die Projekte, die nicht konvertiert werden sollen.

   - Wählen Sie ein Projekt oder eine Projekt Mappe aus, um eine Liste der Änderungen anzuzeigen, die das Tool vornehmen soll.

       > [!NOTE]
       > Die Kontrollkästchen, die neben Ordnernamen angezeigt werden, haben keine Auswirkung. Sie müssen die Ordner erweitern, um die Projekte und Projektmappen zu überprüfen.

4. Konvertieren der Projekte.

   1. Klicken Sie auf **konvertieren**.

        Bevor jede Projektdatei konvertiert wird, wird eine Kopie von _Project_ **. csproj** als _Project_ **. VS2008. csproj** gespeichert.

        Eine Kopie _der einzelnen Projekt_Mappen **. sln** wird als _Solution_ **. VS2008. sln** gespeichert.

   2. Untersuchen Sie alle gemeldeten fehlgeschlagenen Konvertierungen.

        Fehler werden im Fenster Text angezeigt. Außerdem wird in der Strukturansicht ein rotes Flag für jeden Knoten angezeigt, der nicht konvertiert werden konnte. Sie können auf den Knoten klicken, um weitere Informationen zu diesem Fehler zu erhalten.

5. **Transformieren Sie alle Vorlagen** in Projektmappen mit erfolgreich konvertierten Projekten.

   1. Öffnen Sie die Projekt Mappe.

   2. Klicken Sie im Header der Projektmappen-Explorer auf die Schaltfläche **alle Vorlagen transformieren** .

       > [!NOTE]
       > Sie können diesen Schritt unnötig durchführen. Weitere Informationen finden Sie unter [Automatisieren der Transformation für alle Vorlagen](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\)).

6. Aktualisieren Sie den benutzerdefinierten Code in den konvertierten Projekten.

   - Versuchen Sie, die Projekte zu erstellen, und untersuchen Sie alle Fehler.

   - Testen Sie den Designer.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>Siehe auch

- [Verwandte Blogbeiträge](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)