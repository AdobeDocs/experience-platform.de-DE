---
description: Um Destination SDK verwenden zu können, muss ein Partnerunternehmen die in diesem Dokument aufgeführten Voraussetzungen erfüllen.
title: Voraussetzungen für die Integration
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: 6ff5fd0e80f7ca1015969e91cc23c88251509b61
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# Voraussetzungen für die Integration

Um Destination SDK zu verwenden, stellen Sie sicher, dass Sie die in den folgenden Abschnitten aufgelisteten technischen und partnerschaftlichen Voraussetzungen erfüllen.

## Technische/API-Voraussetzungen

1. Sie verfügen über einen REST-API-Endpunkt, an den Adobe Experience Platform die folgenden Datentypen bereitstellen kann:
   * Segmentzugehörigkeitsinformationen;
   * Profilidentitätsdaten;
   * (Optional) Zusätzliche Attribute für die Profilanreicherung.
2. Ihr REST-API-Endpunkt unterstützt die Authentifizierung von API-Token-Bearer oder das OAuth 2.0-Authentifizierungsprotokoll.
3. (Optional) Sie haben einen API- oder API-Endpunkt zum Erstellen/Aktualisieren/Löschen von Segmenten für die programmatische Metadatenverwaltung.

## Voraussetzungen für die Partnerschaft

Wenn Sie ein unabhängiger Software-Anbieter (ISV) oder Systemintegrator (SI) sind und Destination SDK verwenden möchten, lesen Sie die Partnerschaftserfordernisse für ISVs und SIs im Abschnitt [Zugriffsabschnitt abrufen](./overview.md#get-access).
