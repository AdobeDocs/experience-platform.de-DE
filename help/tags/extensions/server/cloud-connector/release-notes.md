---
title: Versionshinweise für die Adobe Experience Platform Cloud-Connector-Erweiterung
description: Aktuelle Versionshinweise zur Cloud-Connector-Erweiterung in Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 100%

---

# Versionshinweise zur Adobe Experience Platform Cloud-Connector-Erweiterung

## &#x200B;17. Januar 2023

v1.0.1

* Es wurde ein Problem behoben, bei dem eine gültige JSON, die in den Textbereich „Body Raw“ eingefügt wurde, als Zeichenfolge statt als JSON gespeichert wurde.
* Lassen Sie nicht zu, dass der Textkörper für GET- oder HEAD-Anfragen festgelegt wird.
* Es wurde ein Fehler behoben, bei dem das Speichern einer Antwort, die größer als 5 KB ist, zu einem Fehlschlagen der Regelausführung führte.
