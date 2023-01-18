---
title: Versionshinweise für die Adobe Experience Platform Cloud Connector-Erweiterung
description: Die aktuellen Versionshinweise für die Cloud Connector-Erweiterung in Adobe Experience Platform.
source-git-commit: e232ad7a9b581e65f7f4240bbc06155aec409eb7
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

