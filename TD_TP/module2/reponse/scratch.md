# Révision et Analyse de Code

---

## Extrait 1 : Refactoring et Clean Code
### a) État Initial (Abstractions)
* **Propriétés :** `p`, `d1`, `d2`, `d3`
* **Méthode :**
    * **Paramètres :** `m`, `d`
    * **Corps :** `r`, `t`

### b) Renommage (Clean Code)
* **Propriétés :**
    * `p` → `penaltyRatio`
    * `d1`, `d2`, `d3` → (Supprimer)
* **Méthode :**
    * **Paramètres :** `m` → `member`, `d` → `dayOverdue`
    * **Corps :** `r` → `result`, `t` → `memberType`

### c) Analyse Technique
* **Nom suggéré :** `calculatePenalty(...)`
* **Types de membres :** Utilisation d'un `ENUM` pour `STUDENT` & `TEACHER`.
* **Problème :** Violation du principe **OCP** (Open/Closed Principle).
* **Code source :**
    ```java
    public double calculatePenalty(Member member, int dayOverdue) {
        String type = member.getType();
        if (type.equals("STUDENT")) return dayOverdue * penaltyRatio * 0.5;
        if (type.equals("TEACHER")) return 0;
        return dayOverdue * penaltyRatio;
    }
    ```

---

## Extrait 2 : Validation de Prêt
* **a) Nombre de responsabilités :** 5
* **b) Méthodes identifiées :**
    * `getMemberId(memberID)`
    * `checkIsActive(member)`
    * `checkIfNotExpiryDateNotPast(membershipExpiryDate)`
    * `checkIfMemberHasAcceptableUnpaidPenalties(member)`
    * `checkMemberLoanQuotaRespected(member)`
* **c) Principe :** Single Responsibility Principle (SRP)

---

## Extrait 3 : Architecture des Services
* **a) Nombre de composants :** 7
* **b) Responsabilités :**
  | Service | Rôle |
  | :--- | :--- |
  | **BookService** | Gestion des livres (CRUD) |
  | **MemberService** | Gestion des membres (CRUD) |
  | **LoanService** | Gestion des emprunts (CRUD) |
  | **PenaltyCalculator** | Calcul des pénalités d'emprunt |
  | **NotificationService** | Envoi des notifications |
  | **ReportGenerator** | Génération des rapports |
  | **ReservationService** | Création / Suppression des réservations |

---

## Extrait 4 : Design Patterns
* **a) Problème :** Duplication du code et manque d'extensibilité.
* **b) Principe violé :** OCP (Open/Closed Principle).
* **c) Solution :** Utilisation d'une interface via le **Design Pattern Strategy**.