---
id: smart-contract-protocol
title: Протокол смарт-контракта
slug: /protocol/social-data-network/smart-contract-protocol
sidebar_label: Протокол смарт-контракта
sidebar_position: 2
description: Протокол смарт-контракта
---

Хотя инфраструктуры данных обеспечивают решение проблем суверенитета данных и интероперабельности, нам все еще нужен способ для пользователей монетизировать свои социальные данные, такие как контент и связи. Кроме того, разработчикам может понадобиться сетевая вычислительная среда для создания своих децентрализованных приложений и сообществ.

Например, децентрализованное приложение, ориентированное на предоставление премиум-сервиса определенным членам NFT сообщества, может захотеть создать социальную сеть с токенами, или платформа публикации может захотеть предоставить пользователям возможность монетизировать свой высококачественный контент. Мы разработали протокол смарт-контрактов, развернутый на блокчейнах, совместимых с EVM, чтобы сделать возможными все эти требования.

## Основные концепции

Протокол смарт-контрактов состоит из генеративных смарт-контрактов, что означает, что он будет генерировать набор новых смарт-контрактов, связанных с децентрализованными приложениями или пользователями, когда они взаимодействуют с протоколом. Этот шаблон аналогичен протоколу Uniswap, где набор смарт-контрактов пары ликвидности будет сгенерирован, когда люди создадут новый пул ликвидности.

В CyberConnect эти сгенерированные смарт-контракты позволяли приложениям создавать свои контекстно-зависимые on-chain социальные сети или пользователям выпускать свои настраиваемые NFT для монетизации своих социальных данных. На высоком уровне протокол представляет социальные данные, используя концепцию ProfileNFT, EssenceNFT и SubsrcibeNFT в формате токенов ERC-721.

### ProfileNFT

ProfileNFT представляет профиль каждого пользователя в виде NFT. Это служит предварительным условием для пользователей, которые хотят выпустить свой настроенный EssenceNFT или SubscribeNFT. Кроме того, развернутый контракт ProfileNFT используется в качестве шлюза для пользователей для выполнения таких действий, как сбор сущностей, создание профиля и подписка на профиль в определенном контексте децентрализованного приложения.

### SubscribeNFT

SubscribeNFT представляет собой однонаправленную связь между адресом и ProfileNFT. Каждый владелец ProfileNFT может оформить только одну уникальную подписку. Каждый подписчик может быть настроен с помощью таких правил, как pay-to-follow (платные подписчики), hold-to-follow (сообщество с закрытыми токенами) и т.д.

### EssenceNFT

EssenceNFT представляет собой общий NFT, который отдельные владельцы ProfileNFT могут выдавать для выражения произвольных отношений, таких как инвестор, покровитель, член команды, участник сообщества и т.д. Каждый EssenceNFT может быть настроен с помощью таких правил, как pay-to-mint (краудфандинг), hold-to-mint (участники сообщества) и т.д. Он также может быть сконфигурирован как торгуемый NFT или непередаваемый Soulbound токен (SBT).

## Составные Middleware

Хотя вычислительные условия сильно различаются в разных приложениях, многие часто встречающиеся шаблоны могут быть обобщены в многоразовые и расширяемые модули. Например, децентрализованное приложение A хочет создать BAYC клуб, установив условие, что только владельцы BAYC могут чеканить свой профиль для конкретного приложения, а децентрализованное приложение B хочет сделать то же самое для владельцев CloneX. Базовая схема та же, и единственным отличием является закрытый адрес контракта ERC-721.

Протокол использует составной уровень промежуточных программ до и после того, как пользователь применяет свои действия по чеканке (например, подписывается на профиль или собирает сущность). Промежуточные программы могут быть созданы для выражения общих ограничений, таких как разрешение проходить проверку только определенным владельцам ERC-721. Таким образом, сообщество может совместно создавать широкий спектр многоразовых промежуточных программ, а разработчики приложений могут легко выбирать подходящие из них для подключения к своему децентрализованному приложению.

Однако важно отметить, что, хотя промежуточные программы являются мощным средством, когда используются для установки ограничений на текущее состояние блокчейна или для сбора on-chain активов, они имеют ограниченную полезность при использовании для проверки исторического состояния или off-chain данных. Одним из возможных решений является вызов контрактов оракулов внутри промежуточной программы для получения потоков данных от off-chain индексаторов.

## Архитектура

![gp_sm](/img/v2/gp_sm.png)