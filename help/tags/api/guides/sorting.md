---
title: Sortieren von Antworten in der Reactor-API
description: Hier erfahren Sie, wie Sie bei der Auflistung von Ressourcen in der Reactor-API Ergebnisse filtern können.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: ht
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
