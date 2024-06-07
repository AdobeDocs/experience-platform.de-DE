---
title: Verschlüsselte Daten in der Quellen-Benutzeroberfläche in Workspace erfassen
description: Erfahren Sie, wie Sie verschlüsselte Daten im Arbeitsbereich der Quellenbenutzeroberfläche erfassen.
hide: true
hidefromtoc: true
source-git-commit: f2a0a9b84dfd3c1d32c8049148d38ef4d2ec822e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 9%

---

# Verschlüsselte Daten in der Quell-Benutzeroberfläche erfassen

In diesem Handbuch erfahren Sie, wie Sie verschlüsselte Daten mithilfe von Cloud-Speicher-Quellen für Batch-Daten in Adobe Experience Platform erfassen können.

## Voraussetzungen

* Daten verschlüsseln

## Aufnehmen verschlüsselter Daten {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Ist die Datei verschlüsselt?"
>abstract="Aktivieren Sie diese Option, wenn Sie bereits verschlüsselte Dateien aufnehmen."


>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Beispieldatei auswählen"
>abstract="Sie müssen beim Erfassen verschlüsselter Daten eine Beispieldatei erfassen, um eine Zuordnung zu erstellen."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_createCustomKey"
>title="Benutzerdefinierten Schlüssel erstellen"
>abstract="Sie können optional ein Schlüsselpaar für die Signierüberprüfung erstellen und einen benutzerdefinierten Schlüssel für Ihre verschlüsselten Daten erstellen."