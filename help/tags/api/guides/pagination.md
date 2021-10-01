---
title: Paginieren von Antworten in der Reactor-API
description: Erfahren Sie, wie Sie bei der Auflistung von Ressourcen in der Reactor-API Ergebnisse paginieren.
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 100%

---

# Paginieren von Antworten in der Reactor-API

Die von der Reactor-API zurückgegebenen Antworten werden paginiert. Die standardmäßige Seitengröße beträgt 25 Elemente. Details zur Paginierung finden Sie im Abschnitt `meta.pagination `des API-Antwortobjekts:

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

Es ist möglich, eine bestimmte Seite abzurufen und die Größe einer Seite zu ändern, indem ein `page`-Abfrageparameter in den Anfragepfad aufgenommen wird.

## Abrufen einer bestimmten Seite

So rufen Sie eine bestimmte Seite ab:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## Ändern der Seitengröße

So ändern Sie die Seitengröße:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

Verschiedene Optionen können kombiniert werden:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
