---
title: Häufig gestellte Fragen (FAQs)
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 89364175-53BA-4A09-B3E2-44AC67DD971C
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/25/2017
ms.openlocfilehash: 5a36c6ab14fdc7bfc5916456670be9c8fe4476ff
ms.sourcegitcommit: b0a1c3969ab2a7b7fe961f4f470d1aa57b1ff2c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
ms.locfileid: "34049882"
---
# <a name="frequently-asked-questions"></a>Häufig gestellte Fragen (FAQs)


## <a name="can-i-update-the-xamarinforms-default-template-to-a-newer-nuget-packageupdate-forms-templatemd"></a>[Kann ich die Xamarin.Forms-Standardvorlage auf ein neueres NuGet-Paket aktualisieren?](update-forms-template.md)
Dieses Handbuch Xamarin.Forms .NET Standard Bibliotheksvorlage als Beispiel verwendet, aber dieselbe allgemeine Methode funktioniert auch für die freigegebene Xamarin.Forms-Projektvorlage. 

## <a name="why-doesnt-the-visual-studio-xaml-designer-work-for-xamarinforms-xaml-filesforms-xaml-designermd"></a>[Warum funktioniert der Visual Studio-XAML-Designer nicht für Xamarin.Forms-XAML-Dateien?](forms-xaml-designer.md)
Xamarin.Forms unterstützt keine derzeit visuelle Designer für XAML-Dateien.

## <a name="android-build-error-the-linkassemblies-task-failed-unexpectedlyandroid-linkassemblies-errormd"></a>[Android-Buildfehler: Unerwarteter Fehler beim Task „LinkAssemblies“](android-linkassemblies-error.md)
Möglicherweise folgende Fehlermeldung `The "LinkAssemblies" task failed unexpectedly` beim Erstellen eines Projekts Xamarin.Android, verwendet Formulare. Dies geschieht, wenn der Linker aktiv ist (in der Regel auf ein *Version* Build zum Verringern der Größe des app-Pakets); und es tritt auf, da Android Zielen auf die neueste Framework aktualisiert werden. 


## <a name="why-does-my-xamarinformsmaps-android-project-fail-with-compiletodalvik--unexpected-top-level-errormaps-compiletodalvik-errormd"></a>["Warum Meine Xamarin.Forms.Maps Android-Projekt nicht mit COMPILETODALVIK: UNERWARTETER Fehler von der obersten Ebene?"](maps-compiletodalvik-error.md)
Dieser Fehler kann in das Auffüllzeichen Fehler von Visual Studio für Mac oder im Fenster Ausgabe Erstellen von Visual Studio angezeigt werden; in der Android-Projekte mit Xamarin.Forms.Maps. Es wird am häufigsten behoben, durch die Java-Heapgröße für Ihr Projekt Xamarin.Android erhöhen.

