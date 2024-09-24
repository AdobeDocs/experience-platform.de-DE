---
title: Versionshinweise für die Adobe Experience Platform Cloud-Connector-Erweiterung
description: Aktuelle Versionshinweise zur Cloud-Connector-Erweiterung in Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '128'
ht-degree: 100%

---

# Versionshinweise zur Adobe Experience Platform Cloud-Connector-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## 17. Januar 2023

v1.0.1

* Es wurde ein Problem behoben, bei dem eine gültige JSON, die in den Textbereich „Body Raw“ eingefügt wurde, als Zeichenfolge statt als JSON gespeichert wurde.
* Lassen Sie nicht zu, dass der Textkörper für GET- oder HEAD-Anfragen festgelegt wird.
* Es wurde ein Fehler behoben, bei dem das Speichern einer Antwort, die größer als 5 KB ist, zu einem Fehlschlagen der Regelausführung führte.
