---
solution: Experience Platform
title: Bekannte Einschränkungen bei Playbooks
description: Erfahren Sie mehr über bekannte Probleme und häufige Probleme mit Playbooks und deren Fehlerbehebung
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# Bekannte Einschränkungen {#known-limitations}

Erfahren Sie, wie Sie Fehler beheben können, wenn Sie mit Anwendungsfall-Playbooks arbeiten, und lernen Sie die bekannten Einschränkungen der allgemeinen Verfügbarkeit kennen.

## Bekannte Einschränkungen

Wenn Sie eine Instanz eines Playbooks erstellen und Assets generieren, treten einige bekannte Einschränkungen auf.

* Wenn bei generierten Schemata ein Schema in einer Instanz eines Playbooks generiert wird und Sie es bearbeiten, wird kein anderes Schema *wird nicht* generiert, wenn Sie eine andere Instanz des Playbooks aktivieren. Verwenden Sie stattdessen weiterhin das Schema, das Sie in der Instanz bearbeitet haben.

* Bei Verwendung der Funktion [Datenbewusstsein](/help/use-case-playbooks/playbooks/data-awareness.md) zum Hochstufen des Schemas von der inspirierenden Sandbox zur Entwicklungs-Sandbox werden möglicherweise einige Fehler angezeigt, die den folgenden ähneln:

![Fehler, die im Workflow für die Schemazuordnung angezeigt werden.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Der Grund dafür ist, dass einige der aus Ihrem Schema generierten Felder nicht im Schema in der Entwicklungs-Sandbox vorhanden sind, in die Sie kopieren. Schlagen Sie nach, was diese Felder sind. Gehen Sie dann zurück zur Entwicklungs-Sandbox, in der Sie Folgendes tun können:

* Erstellen Sie entweder eine neue Feldergruppe, die diese Felder enthält, oder
* Nehmen Sie in Ihr Schema eine standardmäßige, vordefinierte Feldergruppe auf, die die fehlenden Felder enthält.

Nachdem Sie diese Felder in das Schema in die Entwicklungs-Sandbox aufgenommen haben, gehen Sie zurück zum Workflow, um die Schemafelder aus der inspirierenden Sandbox in die Entwicklungs-Sandbox zu kopieren. Die Fehler sind jetzt verschwunden.

Weitere Informationen zum Erstellen von Schemafeldgruppen finden Sie im folgenden Video.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
