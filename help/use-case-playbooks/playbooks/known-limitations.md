---
solution: Experience Platform
title: Bekannte Einschränkungen bei Playbooks
description: Erfahren Sie mehr über bekannte Probleme und häufige Probleme mit Playbooks und wie Sie diese beheben können.
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# Bekannte Einschränkungen {#known-limitations}

Erfahren Sie, wie Sie Fehler beim Arbeiten mit &quot;Anwendungsfall-Playbooks&quot;beheben können, und lernen Sie die bekannten Einschränkungen der allgemeinen Verfügbarkeit kennen.

## Bekannte Einschränkungen

Beim Erstellen einer Instanz eines Playbooks und Generieren von Assets werden einige bekannte Einschränkungen angezeigt.

* Wenn bei generierten Schemata ein Schema in einer Instanz eines Playbooks generiert und Sie es bearbeiten, wird kein weiteres Schema *1} generiert, wenn Sie eine andere Instanz des Playbooks aktivieren.* Verwenden Sie stattdessen weiterhin das Schema, das Sie in der Instanz bearbeitet haben.

* Wenn Sie die [Datenerfassungsfunktion](/help/use-case-playbooks/playbooks/data-awareness.md) verwenden, um das Schema von der inspirierenden Sandbox in die Entwicklungs-Sandbox zu leiten, treten möglicherweise einige Fehler auf, die in etwa wie folgt aussehen:

![ Fehler, die im Workflow für die Schemazuordnung angezeigt werden.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Dies liegt daran, dass einige der aus Ihrem Schema generierten Felder nicht im Schema in der Entwicklungs-Sandbox vorhanden sind, in die Sie kopieren. Suchen Sie nach diesen Feldern. Gehen Sie dann zurück zur Entwicklungs-Sandbox, in der Sie Folgendes ausführen können:

* Erstellen Sie entweder eine neue Feldergruppe mit diesen Feldern oder
* Schließen Sie in Ihr Schema eine standardmäßige, vordefinierte Feldergruppe ein, die die fehlenden Felder enthält.

Nachdem Sie diese Felder in das Schema in die Entwicklungs-Sandbox eingefügt haben, kehren Sie zum Workflow zurück, um die Schemafelder aus der inspirierenden Sandbox in die Entwicklungs-Sandbox zu kopieren. Die Fehler sind nun vorbei.

Weitere Informationen finden Sie im folgenden Video zum Erstellen von Schemafeldgruppen.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
