---
title: Aktivieren von Zielgruppen für kuratierte Ziele basierend auf LiveRamp-IDs
type: Tutorial
description: Erfahren Sie, wie Sie mit der LiveRamp-Ramp-ID Zielgruppen aus Adobe Experience Platform für verbundene TV- und Audioziele und andere Integrationen aktivieren können.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 1%

---

# Aktivieren von Zielgruppen für kuratierte Ziele basierend auf LiveRamp-IDs

Verwenden Sie die Adobe Real-Time CDP-Integration mit [!DNL LiveRamp] , um Zielgruppen für eine kuratierte Liste von Zielen zu aktivieren, die [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) für die Aktivierung verwenden, einschließlich verbundener TV- und Audioziele, wie z. B. die unten aufgeführten.

>[!IMPORTANT]
>
>Sie müssen LiveRamp-Ramp-IDs nicht in der Experience Platform-Oberfläche erfassen oder in irgendeiner Weise verwenden.
>
> Sie können Identitäten aus Real-Time CDP exportieren, z. B. personenbasierte Kennungen, bekannte Kennungen und benutzerdefinierte Kennungen, wie in der offiziellen [LiveRamp-Dokumentation](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers) beschrieben. Diese Identitäten werden dann im weiteren Verlauf des Aktivierungsprozesses mit [!DNL LiveRamp RampIDs] abgeglichen.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppen aus Real-Time CDP für die oben aufgeführten Ziele direkt über die Real-Time CDP-Benutzeroberfläche erforderlich ist.

## Aktivierungs-Workflow {#workflow}

Sie aktivieren Zielgruppen für verbundene TV- und Audioziele, indem Sie einen zweistufigen Prozess durchführen und die Ziele [LiveRamp - Onboarding](../catalog/advertising/liveramp-onboarding.md) und [LiveRamp - Distribution](../catalog/advertising/liveramp-distribution.md) verwenden, wie in der Abbildung unten dargestellt.

![Diagramm, das den Workflow zum Aktivieren von Zielgruppen von Real-Time CDP zu kuratierten Zielen über LiveRamp anzeigt.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Exportieren Sie zunächst Ihre Zielgruppen aus Real-Time CDP als CSV-Dateien in das Ziel &quot;[[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)&quot;.

Nachdem Sie Ihre Zielgruppen exportiert haben, aktivieren Sie sie mithilfe des [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) -Ziels.

>[!TIP]
>
>Auf diese Weise können Sie Ihre Zielgruppen für Ziele wie [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) und mehr direkt über die Real-Time CDP-Benutzeroberfläche aktivieren, ohne sich zur Aktivierung bei Ihrem [!DNL LiveRamp] -Konto anmelden zu müssen.

### Video-Tutorial {#video}

Sehen Sie sich das folgende Video an, um eine umfassende Erläuterung des auf dieser Seite beschriebenen Workflows zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### Schritt 1: Senden Sie Ihre Zielgruppen von Experience Platform an LiveRamp über das Ziel [!DNL LiveRamp - Onboarding] {#onboarding}

Das erste, was Sie tun müssen, um Ihre Zielgruppen für kuratierte Ziele basierend auf LiveRamp RampIDs zu aktivieren, ist, Ihre Zielgruppen von Experience Platform in [!DNL LiveRamp]**zu exportieren.**

Verwenden Sie dazu das Ziel **[!DNL LiveRamp - Onboarding]** .

![Experience Platform UI-Bild mit LiveRamp - Onboarding-Zielkarte](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Informationen zum Konfigurieren des [!DNL LiveRamp - Onboarding]-Ziels und zum Exportieren Ihrer Zielgruppen von Experience Platform finden Sie in der Dokumentation zum [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)-Ziel.

>[!IMPORTANT]
>
>Beim Exportieren von Dateien in das Ziel [!DNL LiveRamp - Onboarding] generiert Platform für jede Kennung der [Zusammenführungsrichtlinie](../../profile/merge-policies/overview.md) eine CSV-Datei. Detaillierte Informationen zur Validierung Ihres Datenexports zu LiveRamp finden Sie in der Dokumentation zum Ziel [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) .


Nachdem Sie Ihre Zielgruppen erfolgreich in LiveRamp exportiert haben, fahren Sie mit [Schritt 2](#distribution) fort.

>[!TIP]
>
>Bevor Sie zu [Schritt 2](#distribution) wechseln, validieren Sie [ ](../catalog/advertising/liveramp-onboarding.md#exported-data), dass Ihre Zielgruppen erfolgreich in LiveRamp exportiert wurden. Weitere Informationen finden Sie in der Dokumentation zu [Überwachung der Ziel-Datenflüsse](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) und lesen Sie die spezifischen Überwachungsdetails für [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Schritt 2: Aktivieren der integrierten Zielgruppen für verbundene TV- und Audioziele über das Ziel [!DNL LiveRamp - Distribution] {#distribution}

Nachdem Sie [validiert](../catalog/advertising/liveramp-onboarding.md#exported-data) haben, dass Ihre Zielgruppen erfolgreich in LiveRamp exportiert wurden, ist es an der Zeit, die Zielgruppen für Ihre bevorzugten Ziele wie [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) und mehr zu aktivieren.

Sie aktivieren die Zielgruppen (exportiert in [Schritt 1](#onboarding)), indem Sie das Ziel **[!DNL LiveRamp - Distribution]** verwenden.

![Experience Platform UI-Bild, das die LiveRamp - Distribution-Zielkarte anzeigt](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Informationen zum Konfigurieren des **[!DNL LiveRamp - Distribution]**-Ziels und Aktivieren der Zielgruppen, die Sie in [Schritt 1](#onboarding) exportiert haben, finden Sie in der Dokumentation zum [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md)-Ziel.

>[!IMPORTANT]
>
>Im Schritt **Zielgruppenauswahl** des Ziels **[!DNL LiveRamp - Distribution]** müssen Sie die *exakt gleichen Zielgruppen* auswählen, die Sie in [Schritt 1](#onboarding) in das Ziel [LiveRamp - Onboarding](../catalog/advertising/liveramp-onboarding.md) exportiert haben.

Wenn Sie das Ziel &quot;**[!DNL LiveRamp - Distribution]**&quot;konfigurieren, müssen Sie eine dedizierte Verbindung für jedes nachgelagerte Ziel erstellen, das Sie verwenden möchten (Roku, Disney usw.).

>[!TIP]
>
>Beim Benennen Ihres Ziels empfiehlt Adobe folgendes Format: `LiveRamp - Downstream Destination Name`. Dieses Namensmuster hilft Ihnen beim schnellen Identifizieren Ihrer Ziele auf der Registerkarte [Durchsuchen](../ui/destinations-workspace.md#browse) im Arbeitsbereich &quot;Ziele&quot;.
><br>
>Beispiel: `LiveRamp - Roku`.

![Screenshot der Platform-Benutzeroberfläche mit mehreren LiveRamp-Zielen.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Informationen zum Validieren des erfolgreichen Exports Ihrer Zielgruppen in das Ziel [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) finden Sie in der Dokumentation zu [Überwachung der Ziel-Datenflüsse](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) und lesen Sie mehr über die spezifischen Überwachungsdetails für [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Um die erfolgreiche Aktivierung Ihrer Zielgruppen auf Ihrer gewünschten Werbeplattform zu überprüfen (z. B. Roku, Disney und andere), melden Sie sich bei Ihrem Zielplattformkonto an und überprüfen Sie die Aktivierungsmetriken.
