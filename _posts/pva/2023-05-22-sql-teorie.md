---
title: SQL Teorie
date: 2023-05-04 22:29:30 -200
layout: post
categories: [Informační technologie, Programování a vývoj aplikací]
tags: [sql]
---

## Teorie - souhrn všech nutných pojmů

- Databáze → souhrn všech uložených dat, potřebných k fungování dané organizace.
- Tabulka → Data, která jsou shromažďována do databází, jsou ukládána do tabulek.
- Entita → objekt reálného světa schopný samostatné existence a jednoznačně odlišitelný od ostatních objektů (student Jan Novák, kniha Babička, ...)
- Atribut → vlastnost entity (jméno, příjmení, plat, ...)
- Primární klíč → jednoznačný identifikátor entity
- NULL → nevyplněná hodnota

## Vztahy

- 1 ku 1 Jedna entita z první tabulky je ve vztahu pouze s jednou entitou z druhé tabulky a naopak (př. Třídní učitel - třída) - Třída má jednoho třídního učitele, třídní učitele vede jen jednu třídu
- 1 ku N → Jedna entita z první tabulky je ve vztahu alespoň s jednou entitou z druhé tabulky a jedna entita z druhé tabulky je ve vztahu pouze s jednou entitou první tabulky (př. student - třída) - Třída má více studentů, student chodí do jedné třídy.
- M ku N → Jedna entita z první tabulky je ve vztahu alespoň s jednou entitou z druhé tabulky a jedna entita z druhé tabulky je ve vztahu alespoň s jednou entitou první tabulky (př. student - předmět) - Jeden předmět má více studentů, student má více předmětů.
