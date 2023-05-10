---
title: Versionshinweise für die Adobe Experience Platform Cloud Connector-Erweiterung
description: Die aktuellen Versionshinweise für die Cloud Connector-Erweiterung in Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 36%

---

# Versionshinweise zur Adobe Experience Platform Cloud Connector-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## 17. Januar 2023

v1.0.1

* Es wurde ein Problem behoben, bei dem eine gültige JSON, die in den Textbereich &quot;Body Raw&quot;eingefügt wurde, als Zeichenfolge statt als JSON gespeichert wurde.
* Setzen Sie den Body nicht bei GET- oder HEAD-Anfragen ein.
* Behebung eines Fehlers, durch den das Speichern einer Antwort, die größer als 5 KB ist, dazu führte, dass die Regelausführung fehlschlug.
