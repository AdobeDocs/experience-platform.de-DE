---
title: Kontozielgruppen
description: Erfahren Sie, wie Sie Zielgruppen für Konten erstellen und verwenden, um Kontoprofile in nachgelagerten Zielen auszuwählen.
badgeLimitedAvailability: label="Eingeschränkte Verfügbarkeit" type="Caution"
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 5%

---

# Kontozielgruppen

>[!AVAILABILITY]
>
>Kontozielgruppen sind nur im [B2B Edition von Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). Darüber hinaus befindet sich die Funktion für die Zielgruppe von Konten derzeit in **begrenzte Verfügbarkeit**. Wenden Sie sich an die Adobe-Kundenunterstützung oder Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern.

Mit der Kontosegmentierung können Sie mit Adobe Experience Platform die gesamte Einfachheit und Komplexität der Marketing-Segmentierungserfahrung von benutzerbezogenen Zielgruppen zu kontobasierten Zielgruppen bringen.

Kontozielgruppen können als Eingabe für kontobasierte Ziele verwendet werden, sodass Sie die Personen innerhalb dieser Konten in nachgelagerten Diensten ansprechen können. Beispielsweise können Sie kontobasierte Zielgruppen verwenden, um Datensätze aller Konten abzurufen, die **not** Kontaktinformationen für alle Personen mit dem Titel Chief Operating Officer (COO) oder Chief Marketing Officer (CMO).

## Terminologie {#terminology}

Bevor Sie mit Kontozielgruppen beginnen, sollten Sie sich die Unterschiede zwischen den verschiedenen Zielgruppentypen ansehen:

- **Kontozielgruppen**: Eine Zielgruppe eines Kontos ist eine Zielgruppe, die mithilfe von **account** Profildaten. Kontoprofildaten können verwendet werden, um Zielgruppen zu erstellen, die Personen in nachgelagerten Konten ansprechen. Weitere Informationen zu Kontoprofilen finden Sie im Abschnitt [Übersicht über Kontoprofile](../../rtcdp/accounts/account-profile-overview.md).
- **Zielgruppen**: Eine Zielgruppe ist eine Zielgruppe, die mit **customer** Profildaten. Kundenprofildaten können verwendet werden, um Zielgruppen zu erstellen, die auf die Kundengruppe Ihres Unternehmens ausgerichtet sind. Weiterführende Informationen zu Kundenprofilen finden Sie im Abschnitt [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).
- **Interessensgruppen**: Eine Interessenten-Zielgruppe ist eine Zielgruppe, die mithilfe von **Interessent** Profildaten. Mit potenziellen Profildaten können Sie Zielgruppen von nicht authentifizierten Benutzern erstellen. Weitere Informationen zu potenziellen Profilen finden Sie im Abschnitt [Interessenten-Profil - Übersicht](../../profile/ui/prospect-profile.md).

## Zugriff auf {#access}

Um auf Kontozielgruppen zuzugreifen, wählen Sie **[!UICONTROL Zielgruppen]** im **[!UICONTROL Konten]** Abschnitt.

![Die Schaltfläche Zielgruppen wird im Abschnitt Konten hervorgehoben.](../images/ui/account-audiences/select.png)

Die [!UICONTROL Durchsuchen] angezeigt, auf der eine Liste aller Zielgruppen des Kontos für die Organisation angezeigt wird.

![Daraufhin werden die Zielgruppen des Kontos der Organisation angezeigt.](../images/ui/account-audiences/browse.png)

Diese Ansicht listet Informationen zur Zielgruppe auf, einschließlich Name, Profilanzahl, Ursprung, Lebenszyklusstatus, Erstellungsdatum und Datum der letzten Aktualisierung.

## Zielgruppe erstellen {#create}

Um eine Konto-Audience zu erstellen, wählen Sie **[!UICONTROL Erstellen einer Zielgruppe]** auf [!UICONTROL Durchsuchen] Seite.

![Die [!UICONTROL Erstellen einer Zielgruppe] auf der Seite zum Durchsuchen der Zielgruppe des Kontos markiert ist.](../images/ui/account-audiences/select-create-audience.png)

Der Segment Builder wird angezeigt. Die Kontoattribute werden in der linken Navigationsleiste angezeigt.

![Der Segment Builder wird angezeigt. Beachten Sie, dass nur die Attribute angezeigt werden.](../images/ui/account-audiences/segment-builder.png)

Beachten Sie beim Erstellen von Kontozielgruppen, dass Ereignisse unter **[!UICONTROL Personen]**, anstatt ihre eigene Registerkarte zu sein, da diese Attribute mit Personen verknüpft sind.

![Der Ort, an dem Ereignisse gefunden werden sollen, der sich im [!UICONTROL Personen] -Ordner, hervorgehoben ist.](../images/ui/account-audiences/attributes.png)

Weitere Informationen zur Verwendung von Segment Builder finden Sie im [Handbuch zur Benutzeroberfläche von Segment Builder](./segment-builder.md).

## Aktivieren der Zielgruppe {#activate}

>[!NOTE]
>
>Nur eine begrenzte Anzahl von Zielen unterstützt Kontozielgruppen. Stellen Sie sicher, dass das Ziel, das Sie aktivieren möchten, um Kontozielgruppen zu unterstützen, bevor Sie diesen Prozess fortsetzen.

Nachdem Sie Ihre Zielgruppe erstellt haben, können Sie die Zielgruppe für andere nachgelagerte Dienste aktivieren.

Wählen Sie die zu aktivierende Audience aus, gefolgt von **[!UICONTROL Auf Ziel aktivieren]**.

![Die [!UICONTROL Auf Ziel aktivieren] im Schnellaktionsmenü der ausgewählten Audience hervorgehoben.](../images/ui/account-audiences/activate.png)

Die [!UICONTROL Ziel aktivieren] angezeigt. Weitere Informationen zum Aktivierungsprozess, einschließlich unterstützter Ziele und Details zu Feldzuordnungen, finden Sie im Abschnitt [Kontozielgruppen aktivieren](/help/destinations/ui/activate-account-audiences.md) Tutorial.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Handbuchs erhalten Sie jetzt ein besseres Verständnis dafür, wie Sie Ihre Kontozielgruppen in Adobe Experience Platform erstellen und verwenden. Informationen zur Verwendung anderer Zielgruppentypen in Platform finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](./overview.md).
