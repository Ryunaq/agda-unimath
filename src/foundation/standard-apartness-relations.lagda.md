---
title: Standard apartness relations
---

```agda
module foundation.standard-apartness-relations where

open import foundation.apartness-relations
open import foundation.coproduct-types
open import foundation.decidable-types
open import foundation.dependent-pair-types
open import foundation.identity-types
open import foundation.law-of-excluded-middle
open import foundation.logical-equivalences
open import foundation.negation
open import foundation.tight-apartness-relations
open import foundation.universe-levels
```

## Idea

An apartness relation `#` is said to be standard if the law of excluded middle implies that `#` is equivalent to negated equality.

## Definition

```agda
is-standard-Apartness-Relation :
  {l1 l2 : Level} (l3 : Level) {A : UU l1} (R : Apartness-Relation l2 A) →
  UU (l1 ⊔ l2 ⊔ lsuc l3)
is-standard-Apartness-Relation {l1} {l2} l3 {A} R =
  LEM l3 → (x y : A) → (¬ (x ＝ y)) ↔ type-rel-Apartness-Relation R x y 
```

## Properties

### Any tight apartness relation is standard

```agda
is-standard-is-tight-Apartness-Relation :
  {l1 l2 : Level} {A : UU l1} (R : Apartness-Relation l2 A) →
  is-tight-Apartness-Relation R → is-standard-Apartness-Relation l2 R
pr1 (is-standard-is-tight-Apartness-Relation R H lem x y) np =
  dn-elim-is-decidable
    ( lem (rel-Apartness-Relation R x y))
    ( map-neg (H x y) np)
pr2 (is-standard-is-tight-Apartness-Relation R H lem x .x) r refl =
  antirefl-Apartness-Relation R x r
```