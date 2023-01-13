---
title: Freigeben einer Erweiterung
description: Erfahren Sie, wie Sie eine Tag-Erweiterung in Adobe Experience Platform privat oder öffentlich freigeben.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 8862a911f09d47c3a2260faba045f3c79826b52c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 98%

---

# Freigeben einer Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Sobald Testing und Dokumentation abgeschlossen sind, kann die Erweiterung freigegeben werden. Es gibt derzeit zwei Arten von Freigaben, die Sie ausführen können:

- **Private Freigabe**: Die fertige Erweiterung steht allen Eigenschaften in Ihrer Firma zur Verfügung, nicht aber anderen Firmen in Adobe Experience Platform.
- **Öffentliche Version**: Die fertige Erweiterung ist im Online-Marktplatz für alle Benutzer von Adobe Experience Platform verfügbar.

>[!NOTE]
>
>Nachdem Sie Ihre Erweiterung freigegeben haben, können Sie keine Änderungen mehr daran vornehmen und die Freigabe nicht aufheben.  Nach der Freigabe können Sie Fehlerkorrekturen und Funktionserweiterungen vornehmen, indem Sie mit `POST` eine neue Version des Erweiterungspakets veröffentlichen und die oben genannten Test- und Freigabeschritte für diese neue Version ausführen.

Sie müssen Ihre Erweiterung als private Erweiterung freigeben, bevor Sie sie öffentlich freigeben können.

## Private Freigabe

Die einfachste Möglichkeit, Ihre Erweiterung mit privater Verfügbarkeit freizugeben, ist die Verwendung des [Freigabeprogramms für Tag-Erweiterungen](https://www.npmjs.com/package/@adobe/reactor-releaser). Weitere Anweisungen finden Sie in der zugehörigen Dokumentation.

Wenn Sie Ihre Erweiterung mit privater Verfügbarkeit direkt über die API freigeben möchten, finden Sie weitere Details im Beispielaufruf für die [private Freigabe eines Erweiterungspakets](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) in den API-Dokumenten.

## Öffentliche Freigabe

Sobald Sie die private Freigabe abgeschlossen haben, können Sie Adobe um die öffentliche Freigabe bitten.  Dadurch wird Ihre Erweiterung im öffentlichen Katalog verfügbar gemacht. Jeder Nutzer der Datenerfassung kann Ihre Erweiterung für jede Eigenschaft installieren.

Bitte füllen Sie das [Anfrageformular für eine öffentliche Freigabe](https://experiencecloudpanel.adobe.com/c/r/DCExtensionReleaseRequest) aus, um den Freigabeprozess zu starten.
