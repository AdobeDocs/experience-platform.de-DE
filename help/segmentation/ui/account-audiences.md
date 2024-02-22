---
title: Kontozielgruppen
description: Erfahren Sie, wie Sie Zielgruppen für Konten erstellen und verwenden, um Kontoprofile in nachgelagerten Zielen auszuwählen.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 2%

---

# Kontozielgruppen

>[!AVAILABILITY]
>
>Kontozielgruppen sind nur im [B2B Edition von Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) und [B2P Edition von Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p).

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

## Anhang {#appendix}

Im folgenden Abschnitt finden Sie weitere Informationen zu Kontozielgruppen.

### Validierung der Kontosegmentierung {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Maximaler Lookback-Fensterfehler"
>abstract="Das maximale Lookback-Fenster für Erlebnisereignisse beträgt 30 Tage."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Maximaler verschachtelter Behältertiefenfehler"
>abstract="Die maximale Tiefe verschachtelter Container beträgt **5**. Das bedeutet, dass Sie **cannot** haben beim Erstellen Ihrer Audience mehr als fünf verschachtelte Container."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Maximaler Regelzahlenfehler"
>abstract="Die maximale Anzahl von Regeln in einem einzelnen Container beträgt **5**. Das bedeutet, dass Sie **cannot** mehr als fünf Regeln in einem Container enthalten, wenn Sie Ihre Zielgruppe erstellen."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Maximaler Wert der Entität"
>abstract="Die maximale Anzahl von Entitäten, die in einer Audience verwendet werden können, beträgt **5**. Eine übergreifende Entität ist der Fall, wenn Sie zwischen verschiedenen Entitäten in Ihrer Zielgruppe wechseln. So können Sie beispielsweise von einem Konto zu einer Person zu einer Marketingliste wechseln."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Benutzerdefinierter Entitätsfehler"
>abstract="Benutzerdefinierte Entitäten sind **not** erlaubt."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Ungültiger B2B-Entitätsfehler"
>abstract="Nur die folgenden B2B-Entitäten dürfen verwendet werden: `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member`, und `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Maximaler Wertefehler"
>abstract="Die maximale Anzahl von Werten, die für ein einzelnes Feld überprüft werden können, beträgt **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="inSegment-Ereignisfehler"
>abstract="inSegment -Ereignisse sind **not** erlaubt."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="inSegment-Ereignisfehler"
>abstract="inSegment -Ereignisse sind **not** erlaubt."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Sequenzieller Ereignisfehler"
>abstract="Sequenzielle Ereignisse sind **not** erlaubt."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Eigenschaftsfehler &quot;Map-type&quot;"
>abstract="Eigenschaften vom Typ Zuordnung sind **not** erlaubt."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Maximaler verschachtelter Entitätstiefenfehler"
>abstract="Die maximale Tiefe verschachtelter Arrays beträgt **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Maximaler Fehler bei verschachtelter Objektmenge"
>abstract="Die maximal zulässige Anzahl verschachtelter Objekte ist **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Beschränkungsverletzung"
>abstract="Die Zielgruppe verstößt gegen eine Einschränkung. Weitere Informationen finden Sie im entsprechenden Dokument."

Bei Verwendung von Kontozielgruppen wird die Zielgruppe **must** die folgenden Einschränkungen einhalten:

>[!NOTE]
>
>Die folgende Liste zeigt die **default** Einschränkungen für Zielgruppen. Diese Werte **kann** ändern, abhängig von den vom Administrator Ihres Unternehmens implementierten Einstellungen.

- Das maximale Lookback-Fenster für Erlebnisereignisse ist **30 Tage**.
- Die maximale Tiefe verschachtelter Container beträgt **5**.
   - Das bedeutet, dass Sie **cannot** haben beim Erstellen Ihrer Audience mehr als fünf verschachtelte Container.
- Die maximale Anzahl von Regeln in einem einzelnen Container beträgt **5**.
   - Das bedeutet, dass Ihre Zielgruppe **cannot** haben mehr als fünf Regeln, aus denen sich Ihre Zielgruppe zusammensetzt.
- Die maximale Anzahl von Entitäten, die verwendet werden können, lautet **5**.
   - Eine übergreifende Entität ist der Fall, wenn Sie zwischen verschiedenen Entitäten in Ihrer Zielgruppe wechseln. So können Sie beispielsweise von einem Konto zu einer Person zu einer Marketingliste wechseln.
- Benutzerdefinierte Entitäten **cannot** verwendet werden.
- Die maximale Anzahl von Werten, die für ein einzelnes Feld überprüft werden können, beträgt **50**.
   - Wenn Sie beispielsweise das Feld &quot;Stadt&quot;haben, können Sie diesen Wert mit 50 Stadtnamen vergleichen.
- Kontozielgruppen **cannot** use `inSegment` -Ereignisse.
- Kontozielgruppen **cannot** sequenzielle Ereignisse verwenden.
- Kontozielgruppen **cannot** Verwenden Sie Maps.
- Die maximale Tiefe verschachtelter Arrays beträgt **5**.
- Die maximale Anzahl verschachtelter Objekte beträgt **10**.
