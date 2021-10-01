---
title: Sortieren von Antworten in der Reactor-API
description: Hier erfahren Sie, wie Sie bei der Auflistung von Ressourcen in der Reactor-API Ergebnisse filtern können.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 100%

---

# Sortieren von Antworten in der Reactor-API

Auflistungs-Endpunkte in der Reactor-API ermöglichen es Ihnen, zurückgegebene Ressourcen basierend auf angegebenen Attributen zu sortieren. Sie können die Sortierreihenfolge der Antwort konfigurieren, indem Sie im Anfragepfad einen Parameter `sort` angeben.

## Aufsteigende Sortierung

Die Ressourcen können nach einem Attribut in aufsteigender Reihenfolge sortiert werden, indem Sie das Attribut angeben, nach dem sortiert werden soll, und es mit einem Präfix `+` versehen:

`GET /companies/:company_id/properties?sort=+name`

## Absteigende Sortierung

Die Ressourcen können nach einem Attribut in absteigender Reihenfolge sortiert werden, indem Sie das Attribut angeben, nach dem sortiert werden soll, und es mit einem Präfix `-` versehen:

`GET /companies/:company_id/properties?sort=-name`

## Mehrfaches Sortieren

Um nach mehreren Werten zu sortieren, geben Sie die Sortierrichtlinien als kommagetrennte Liste an:

`GET /companies/:company_id/properties?sort=+name,-org_id`
