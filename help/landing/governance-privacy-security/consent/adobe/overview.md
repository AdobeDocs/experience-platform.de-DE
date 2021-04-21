---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Verarbeitung von Genehmigungen in Adobe Experience Platform
topic-legacy: getting started
description: Erfahren Sie, wie Sie mit dem Adobe 2.0-Standard Kundenbestätigungssignale in Adobe Experience Platform verarbeiten.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---

# Verarbeitung von Genehmigungen in Adobe Experience Platform

Mit Adobe Experience Platform können Sie die von Ihren Kunden gesammelten Einwilligungsdaten verarbeiten und in Ihre gespeicherten Profil integrieren. Diese Daten können dann von nachgelagerten Prozessen verwendet werden, um festzustellen, ob die Datenerfassung für einen bestimmten Kunden erfolgt oder ob ihre Profil für bestimmte Zwecke verwendet werden. Beispielsweise können die Genehmigungsdaten für ein bestimmtes Profil bestimmen, ob es in ein exportiertes Audiencen-Segment aufgenommen werden kann oder ob es an bestimmten Marketing-Kanälen wie E-Mail, Textnachrichten oder Push-Benachrichtigungen teilnehmen kann.

Dieses Dokument gibt einen Überblick darüber, wie Sie Ihren Plattformdatenbetrieb so konfigurieren können, dass von einer Plattform für das Zustimmungsmanagement (CMP) generierte Daten zur Kundeneinwilligung erfasst und diese Daten in Profil für den nachgelagerten Einsatz integriert werden.

>[!NOTE]
>
>Dieses Dokument konzentriert sich auf die Verarbeitung von Genehmigungsdaten unter Verwendung des Adobe-Standards. Wenn Sie die Genehmigungsdaten gemäß dem IAB-Transparenz- und -Zustimmung-Framework (TCF) 2.0 verarbeiten, finden Sie weitere Informationen im Handbuch [TCF 2.0-Unterstützung in der Echtzeit-Kundendatenplattform](../iab/overview.md).

## Voraussetzungen

Dieser Leitfaden erfordert ein Verständnis der verschiedenen Experience Platformen, die an der Verarbeitung von Genehmigungsdaten beteiligt sind:

* [Erlebnisdatenmodell (XDM)](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform-Identitätsdienst](../../../../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Profil](../../../../profile/home.md): Verwendet  [!DNL Identity Service] Funktionen zum Erstellen detaillierter Kundendaten aus Ihren Datensätzen in Echtzeit. Echtzeit-Profil ruft Daten aus dem Data Lake ab und behält Profil in einem eigenen Datenspeicher bei.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Eine clientseitige JavaScript-Bibliothek, mit der Sie verschiedene Plattformdienste in Ihre kundenorientierte Website integrieren können.
   * [SDK-Zustimmungsbefehle](../../../../edge/consent/supporting-consent.md): Eine Gebrauchsanweisung zu den einwilligungsbezogenen SDK-Befehlen, die in diesem Handbuch gezeigt werden.
* [Adobe Experience Platform-Segmentierungsdienst](../../../../segmentation/home.md): Ermöglicht die Unterteilung von Echtzeit-Kundendaten in Gruppen von Einzelpersonen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.

## Zusammenfassung des Verarbeitungsablaufs für Zustimmung {#summary}

Im Folgenden wird beschrieben, wie die Daten zur Zustimmung verarbeitet werden, nachdem das System ordnungsgemäß konfiguriert wurde:

1. Ein Kunde gibt seine Einwilligung in die Datenerfassung durch einen Dialog auf Ihrer Website.
1. Bei jedem Laden der Seite (oder wenn Ihr CMP eine Änderung der Voreinstellungen für die Zustimmung erkennt) ordnet ein benutzerdefiniertes Skript auf Ihrer Site die aktuellen Voreinstellungen einem Standard-XDM-Objekt zu. Dieses Objekt wird dann an den Befehl Platform Web SDK `setConsent` übergeben.
1. Wenn `setConsent` aufgerufen wird, prüft das Plattform-Web-SDK, ob sich die Werte für die Zustimmung von denen unterscheiden, die es zuletzt erhalten hat. Wenn die Werte unterschiedlich sind (oder kein vorheriger Wert vorliegt), werden die strukturierten Daten zur Zustimmung/Voreinstellung an Adobe Experience Platform gesendet.
1. Die Daten zur Einwilligung/Voreinstellung werden in einen [!DNL Profile]-aktivierten Dataset eingeschlossen, dessen Schema die Felder für die Einwilligung/Voreinstellung enthält.

Zusätzlich zu den SDK-Befehlen, die durch CMP-Zugriffs-/Änderungshaken ausgelöst werden, können Genehmigungsdaten auch über kundengenerierte XDM-Daten in die Experience Platform fließen, die direkt in ein [!DNL Profile]-aktiviertes Dataset hochgeladen werden.

### Vollstreckung zustimmen

In der aktuellen Version der Unterstützung für die Verarbeitung der Zustimmung in Platform wird nur die Datenerfassungsberechtigung (`collect.val`) automatisch vom Plattform Web SDK erzwungen. Während in Kundenprozessen granulärere Einwilligungen und Präferenzen gesammelt und beibehalten werden können, müssen diese zusätzlichen Profile in Ihren eigenen nachgelagerten Prozessen manuell erzwungen werden.

>[!NOTE]
>
>Weitere Informationen zur Struktur der oben erwähnten XDM-Einwilligungsfelder finden Sie im Handbuch zum Datentyp [Einwilligungen und Voreinstellungen](../../../../xdm/data-types/consents.md).

Sobald das System konfiguriert wurde, interpretiert das Platform Web SDK den Datenerfassungs-Zustimmungswert für den aktuellen Benutzer, um festzustellen, ob die Daten an das Adobe Experience Platform Edge Network gesendet, vom Client gelöscht oder bestehen bleiben sollen, bis die Datenerfassungsberechtigung auf &quot;Ja&quot;oder &quot;Nein&quot;eingestellt ist.

## Ermitteln Sie, wie Daten zur Kundengenehmigung in Ihrem CMP generiert werden.{#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie die beste Methode festlegen, um Ihren Kunden die Zustimmung zu geben, während sie mit Ihrem Service interagieren. Eine gängige Möglichkeit, dies zu erreichen, ist die Verwendung eines Cookie-Einwilligungsdialogs, ähnlich dem folgenden Beispiel:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Dieser Dialog sollte es dem Kunden ermöglichen, bestimmte Anwendungsfälle für Marketing und Personalisierung für seine Daten zu Opt-in oder zu beenden. Diese Zustimmungen und Voreinstellungen sollten mit dem Datenmodell übereinstimmen, das Sie im nächsten Schritt für den [!DNL Profile]-aktivierten Datensatz definieren.

## hinzufügen standardisierte Felder für die Zustimmung zu einem [!DNL Profile]-aktivierten Datensatz {#dataset}

Die Daten zur Kundengenehmigung müssen an einen [!DNL Profile]-aktivierten Datensatz gesendet werden, dessen Schema Zustimmungsfelder enthält. Diese Felder müssen in demselben Schema und demselben Datensatz enthalten sein, mit dem Sie Attributinformationen über einzelne Kunden erfassen können.

Weitere Informationen zum Hinzufügen dieser erforderlichen Felder zu einem [!DNL Profile]-aktivierten Datensatz finden Sie im Lernprogramm [Konfigurieren eines Datensatzes zum Erfassen von Genehmigungsdaten](./dataset.md), bevor Sie mit diesem Handbuch fortfahren.

## [!DNL Profile]-Zusammenführungsrichtlinien aktualisieren, um Einwilligungsdaten einzuschließen {#merge-policies}

Nachdem Sie einen [!DNL Profile]-aktivierten Datensatz für die Verarbeitung von Genehmigungsdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass in jedem Profil stets die Felder für die Zustimmung enthalten sind. Hierzu gehört die Festlegung der Priorität von Datasets, sodass Ihr Dataset für die Einwilligung Vorrang vor anderen möglicherweise widersprüchlichen Datensätzen hat.

>[!NOTE]
>
>Wenn keine in Konflikt stehenden Datensätze vorhanden sind, sollten Sie stattdessen die Zeitstempelpriorität für Ihre Zusammenführungsrichtlinie festlegen. Dadurch wird sichergestellt, dass die von einem Kunden angegebene letzte Zustimmung die verwendete Einstellung für die Zustimmung ist.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie im Benutzerhandbuch [Richtlinien zusammenführen](../../../../profile/ui/merge-policies.md). Beim Einrichten der Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Profil alle erforderlichen Zustimmungsattribute enthalten, die vom Mixin &quot;Einwilligungen und Voreinstellungen&quot;bereitgestellt werden, wie im Handbuch [Dataset-Vorbereitung](./dataset.md) beschrieben.

## Genehmigungsdaten in Plattform übernehmen

Sobald Sie über Ihre Datasets verfügen und Richtlinien zusammenführen, um die erforderlichen Felder für die Zustimmung in Ihren Profilen zu repräsentieren, besteht der nächste Schritt darin, die Genehmigungsdaten selbst in die Plattform zu übertragen.

In erster Linie sollten Sie das Adobe Experience Platform Web SDK verwenden, um Zustimmungsdaten an Platform zu senden, wenn Ereignisse zur Änderung der Zustimmung von Ihrem CMP erkannt werden. Wenn Sie Daten zur Einwilligung auf einer mobilen Plattform erfassen, sollten Sie das Adobe Experience Platform Mobile SDK verwenden. Sie können sich auch dafür entscheiden, Ihre gesammelten Einwilligungsdaten direkt zu erfassen, indem Sie sie dem XDM-Schema Ihres Datasets für die Einwilligung zuordnen und durch Stapelverarbeitung an Platform senden.

Einzelheiten zu diesen Methoden finden Sie in den Unterabschnitten unten.

### Experience Platform Web SDK für die Verarbeitung von Genehmigungsdaten {#web-sdk} konfigurieren

Nachdem Sie Ihren CMP so konfiguriert haben, dass er auf Ereignis zur Änderung der Einwilligung auf Ihrer Website überwacht, können Sie das Experience Platform Web SDK integrieren, um die aktualisierten Einwilligungseinstellungen zu erhalten und sie bei jedem Seitenladevorgang und bei jedem Ereignis zur Änderung der Einwilligung an die Plattform zu senden. Weitere Informationen finden Sie im Handbuch [Konfigurieren des Web SDK zur Verarbeitung von Daten zur Kundengenehmigung](./sdk.md).

### Konfigurieren Sie das Experience Platform Mobile SDK für die Verarbeitung von Genehmigungsdaten {#mobile-sdk}

Wenn in Ihrer mobilen Anwendung die Voreinstellungen für die Kundengenehmigung erforderlich sind, können Sie das Experience Platform Mobile SDK integrieren, um die Einstellungen für die Zustimmung abzurufen und zu aktualisieren, und diese bei jedem Aufruf der API an die Plattform senden.

Weitere Informationen finden Sie in der Mobile SDK-Dokumentation für [Konfigurieren der mobilen Erweiterung Zustimmung](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent) und [mit der API für Zustimmung](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent/edge-consent-api-reference). Weitere Informationen zum Umgang mit Datenschutzbelangen mit dem Mobile SDK finden Sie im Abschnitt [Datenschutz und PDF](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/resources/privacy-and-gdpr).

### XDM-konforme Einwilligungsdaten direkt einholen {#batch}

Sie können XDM-konforme Einwilligungsdaten aus einer CSV-Datei mithilfe der Stapelverarbeitung erfassen. Dies kann nützlich sein, wenn Sie einen Rückstand der zuvor erfassten Daten zur Einwilligung haben, die noch nicht in Ihre Profil integriert werden müssen.

Folgen Sie dem Lernprogramm unter [Zuordnen einer CSV-Datei zu XDM](../../../../ingestion/tutorials/map-a-csv-file.md), um zu erfahren, wie Sie Ihre Datenfelder in XDM konvertieren und in Plattform aufnehmen. Wählen Sie bei Auswahl von [!UICONTROL Ziel] für die Zuordnung die Option **[!UICONTROL Vorhandenen Datensatz]** verwenden und wählen Sie den zuvor erstellten [!DNL Profile]-aktivierten Genehmigungsdataset.

## Testen Sie Ihre Implementierung {#test-implementation}

Nachdem Sie Daten zur Kundeneinwilligung in Ihren [!DNL Profile]-aktivierten Datensatz eingegeben haben, können Sie Ihre aktualisierten Profil überprüfen, um zu sehen, ob sie Zustimmungsattribute enthalten.

>[!IMPORTANT]
>
>Zur Ansicht der Attribute eines vorhandenen Profils in der Benutzeroberfläche müssen Sie mindestens einen Identitätswert (und den zugehörigen Namensraum) kennen, der mit diesem Profil verknüpft ist.
>
>Wenn Sie keinen Zugriff auf diese Informationen haben, können Sie Ihre eigenen Testbestätigungsdaten erfassen und sie mit einem Identitätswert/Namensraum verbinden, der Ihnen bekannt ist.

Im Abschnitt [Durchsuchen von Profilen nach Identität](../../../../profile/ui/user-guide.md#browse) im [!DNL Profile]-UI-Handbuch finden Sie spezifische Schritte zum Nachschlagen der Details eines Profils.

Die neuen Attribute für die Zustimmung werden nicht standardmäßig auf dem Dashboard eines Profils angezeigt. Daher müssen Sie auf der Detailseite eines Profils zur Registerkarte **[!UICONTROL Attribute]** navigieren, um zu bestätigen, dass die Daten erwartungsgemäß aufgenommen wurden. Informationen zum Anpassen des Dashboards an Ihre Anforderungen finden Sie im Dashboard [Profil](../../../../profile/ui/profile-dashboard.md).

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Ihre Plattformoperationen so konfigurieren, dass Daten zur Kundeneinwilligung unter Verwendung des Adobe-Standards verarbeitet werden und dass diese Attribute in den Profilen der Kunden dargestellt werden. Sie können jetzt Voreinstellungen für die Kundengenehmigung als entscheidenden Faktor in die Segmentqualifizierung und andere nachgelagerte Anwendungsfälle integrieren.

Weitere Informationen zu den datenschutzbezogenen Funktionen der Experience Platform finden Sie im Überblick über [Verwaltung, Datenschutz und Sicherheit in Platform](../../overview.md).
