---
title: Sortieren von Antworten in der Reactor-API
description: Erfahren Sie, wie Sie bei der Auflistung von Ressourcen in der Reactor-API Ergebnisse filtern können.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Sortieren von Antworten in der Reactor-API

Auflistungs-Endpunkte in der Reactor-API ermöglichen es Ihnen, zurückgegebene Ressourcen basierend auf angegebenen Attributen zu sortieren. Sie können die Sortierreihenfolge der Antwort konfigurieren, indem Sie im Anfragepfad einen Parameter `sort` angeben.

## Aufsteigende Sortierung

Die Ressourcen können nach einem Attribut in aufsteigender Reihenfolge sortiert werden, indem die
-Attribut, nach dem sortiert und mit einem `+`-Präfix versehen werden soll:

`GET /companies/:company_id/properties?sort=+name`

## Absteigende Sortierung

Die Ressourcen können durch ein Attribut in absteigender Reihenfolge sortiert werden, indem die
-Attribut, nach dem sortiert und mit einem `-`-Präfix versehen werden soll:

`GET /companies/:company_id/properties?sort=-name`

## Mehrere Sorten

Um nach mehreren Werten zu sortieren, geben Sie die Sortierrichtlinien als kommagetrennte Elemente an
list:

`GET /companies/:company_id/properties?sort=+name,-org_id`
