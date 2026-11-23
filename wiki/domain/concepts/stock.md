---
title: Stock
type: concept
template-version: 1
sources: []
related: []
created: 2026-11-23
updated: 2026-11-23
owner: domain
authorship: curated
confidence: medium
---

## Definition

Stock is the number of units of an item that a shop currently holds and can sell. It is counted for each item separately, and it counts what the shop has, not what it has sold. Naming it lets a shop tell an item that is available from one that has run out. The recorded count can differ from what is on the shelf when units leave or arrive without being recorded.

## Usage

A shop checks an item's stock before it offers the item, and changes the count when units are sold, restocked, returned or lost. An item is in stock while its count is above zero and out of stock at zero.

> [!warning]
> Stock is not the quantity a shopper chooses. A chosen quantity is a wish until it is bought. Stock is what the shop has.

## Examples

- A shop holds 12 packets of chips. A shopper buys 2, and stock falls to 10.
- A delivery of 24 packets arrives, and stock rises by 24.
- A packet is dropped and thrown away. Stock falls without a sale.
- A shop counts the shelf at the end of the month and finds 9 packets where its records say 10.

## Non-examples

- The price of an item. Stock counts units and says nothing about cost.
- The quantity in a shopper's basket. Nothing has been taken from stock yet.
- The number of units sold. That is a history of sales, and stock is what remains.
- The range of different items a shop offers. That is a catalog.

## Boundaries

None.

## Related concepts

- [[entities/catalog]] — the range of items whose stock is counted.
- [[entities/item]] — the entity that carries an item's stock quantity.
