---
title: Freigeben einer Erweiterung
description: Erfahren Sie, wie Sie eine Tag-Erweiterung in Adobe Experience Platform privat oder öffentlich veröffentlichen.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 58%

---

# Freigeben einer Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Sobald die Tests und die Dokumentation abgeschlossen sind, kann die Erweiterung veröffentlicht werden. Es gibt derzeit zwei Arten von Freigaben, die Sie ausführen können:

- **Private Freigabe**: Die fertige Erweiterung steht allen Eigenschaften in Ihrer Firma zur Verfügung, nicht aber anderen Firmen in Adobe Experience Platform.
- **Öffentliche Freigabe**: Die fertige Erweiterung ist im öffentlichen Marketplace für alle Adobe Experience Platform-Benutzer verfügbar.

>[!NOTE]
>
>Nachdem Sie Ihre Erweiterung veröffentlicht haben, können Sie keine Änderungen mehr daran vornehmen und die Freigabe nicht rückgängig machen.  Nach der Freigabe können Sie Fehlerkorrekturen und Funktionserweiterungen vornehmen, indem Sie mit `POST` eine neue Version des Erweiterungspakets veröffentlichen und die oben genannten Test- und Freigabeschritte für diese neue Version ausführen.

Sie müssen Ihre Erweiterung als private Erweiterung freigeben, bevor Sie sie öffentlich freigeben können.

## Private Freigabe

Die einfachste Möglichkeit, Ihre Erweiterung mit privater Verfügbarkeit freizugeben, besteht darin, den [Tag-Erweiterungs-Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) zu verwenden. Weitere Anweisungen finden Sie in der zugehörigen Dokumentation.

Wenn Sie Ihre Erweiterung mit privater Verfügbarkeit direkt über die API freigeben möchten, finden Sie weitere Informationen im Beispielaufruf für [privates Freigeben eines Erweiterungspakets](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) in den API-Dokumenten.

## Öffentliche Freigabe

Sobald Sie die private Freigabe abgeschlossen haben, können Sie Adobe um die öffentliche Freigabe bitten.  Dadurch wird Ihre Erweiterung im öffentlichen Katalog verfügbar gemacht. Jeder Datenerfassungsbenutzer kann Ihre Erweiterung in jeder Eigenschaft installieren.

Bitte füllen Sie das [Anfrageformular für eine öffentliche Freigabe](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U) aus, um den Freigabeprozess zu starten.
