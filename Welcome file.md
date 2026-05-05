dossier de mise en place d'un réseau BACnet/IP pour un centre hospitalier universitaire au quebec

# Dossier de mise en place d'un réseau BACnet/IP — Centre hospitalier universitaire (Québec)

Ce dossier présente les grandes lignes d'un projet de déploiement BACnet/IP dans un contexte hospitalier québécois. Il peut servir de canevas pour un appel d'offres, un mémoire technique ou un document de conception préliminaire.

----------

## 1. Contexte et objectifs

### 1.1 Portée du projet

-   Établissement : Centre hospitalier universitaire (CHU) — préciser le nom, le campus et les bâtiments visés.
-   Systèmes à intégrer : CVC (chauffage, ventilation, climatisation), éclairage, contrôle d'accès, détection incendie (si permis par le Code), gestion de l'énergie, équipements biomédicaux compatibles.
-   Objectifs :
    -   Interopérabilité entre équipements de fabricants différents.
    -   Supervision centralisée (poste opérateur GTB/GTC).
    -   Conformité aux exigences réglementaires québécoises et aux normes ASHRAE/CSA.
    -   Résilience et cybersécurité adaptées au secteur de la santé.

### 1.2 Cadre normatif et réglementaire

Domaine

Références

Protocole BACnet

ANSI/ASHRAE 135-2020, ISO 16484-5

Cybersécurité réseau

CSA C22.1 (Code canadien de l'électricité), MSSS — Cadre de gestion de la sécurité de l'information, NIST SP 800-82 (ICS)

Construction

Code de construction du Québec (CCQ), LEED v4.1 Santé (si visé)

Électricité/CVC

RBQ, normes CSA B52, ASHRAE 170 (ventilation en milieu de santé)

----------

## 2. Architecture réseau proposée

### 2.1 Topologie générale

### 2.2 Segmentation et adressage

-   VLAN dédié GTB isolé du réseau clinique et administratif.
-   Plage IP privée réservée (ex. : 10.200.x.x/16).
-   Ports UDP 47808 (BACnet) et 47809 (BACnet/SC si chiffrement requis) ouverts uniquement à l'intérieur du VLAN.
-   Passerelles BACnet/IP ↔ MS/TP dans les locaux techniques pour les équipements existants.

### 2.3 Redondance et disponibilité

-   Double alimentation (UPS) sur commutateurs cœur et contrôleurs critiques.
-   Liens fibre redondants entre bâtiments (anneau ou maillage).
-   Basculement automatique des contrôleurs principaux (hot standby) pour les zones vitales (bloc opératoire, soins intensifs).

----------

## 3. Spécifications techniques

### 3.1 Profils BACnet exigés

Rôle

Profil PICS minimal

Poste opérateur

B-OWS (Operator Workstation)

Contrôleur d'immeuble

B-BC (Building Controller)

Contrôleur d'application

B-AAC (Advanced Application Controller)

Passerelle MS/TP

B-RTR (Router)

Capteur intelligent

B-ASC (Application Specific Controller)

### 3.2 Services BACnet obligatoires

-   ReadProperty / WriteProperty (lecture/écriture de points)
-   SubscribeCOV (abonnement aux changements de valeur)
-   Alarming (GetAlarmSummary, AcknowledgeAlarm)
-   Trending (CreateObject, ReadRange)
-   DeviceCommunicationControl (maintenance)
-   ReinitializeDevice (redémarrage à distance)

### 3.3 Exigences de performance

-   Temps de scrutation des points critiques : ≤ 1 s.
-   Taux de disponibilité du réseau GTB : ≥ 99,9 %.
-   Latence réseau intra-VLAN : < 10 ms.

----------

## 4. Cybersécurité

### 4.1 Mesures réseau

1.  Segmentation stricte — VLAN GTB isolé, ACL sur commutateurs et pare-feu.
2.  BACnet/SC (Secure Connect) recommandé pour les liaisons traversant des zones moins sécurisées ou l'extérieur.
3.  Authentification — Certificats TLS pour BACnet/SC; mots de passe forts pour les interfaces web des contrôleurs.
4.  Journalisation — Syslog centralisé vers le SIEM hospitalier.

### 4.2 Gestion des accès

-   Comptes nominatifs pour les techniciens GTB; pas de compte générique partagé.
-   Principe du moindre privilège (lecture seule par défaut).
-   Révocation immédiate des accès des sous-traitants à la fin du contrat.

### 4.3 Mises à jour et correctifs

-   Processus de validation des micrologiciels avant déploiement.
-   Fenêtres de maintenance planifiées hors heures critiques.

----------

## 5. Intégration et tests

### 5.1 Phases du projet

Phase

Livrables

Critères de réussite

Conception détaillée

Plans réseau, liste de points, spécifications PICS

Approbation du comité technique

Installation

Infrastructure filaire, commutateurs, contrôleurs

Certificat d'installation

Mise en service

Programmation, test point par point

100 % des points lus/écrits sans erreur

Intégration GTB

Graphiques, alarmes, tendances

Validation opérateur

Tests d'acceptation (FAT/SAT)

Scénarios fonctionnels, tests de charge

Conformité au cahier des charges

Formation et transfert

Documentation, formation du personnel

Attestation de formation

### 5.2 Tests de conformité BACnet

-   Utilisation d'un outil certifié BTL (BACnet Testing Laboratories) pour valider l'interopérabilité.
-   Test de reprise après coupure réseau (fail-over, reprise COV).

----------

## 6. Exploitation et maintenance

-   Documentation : schémas à jour, registre de points (base de données), procédures d'exploitation.
-   Contrat de maintenance : SLA avec temps de réponse maximal (ex. : 4 h pour alarme critique).
-   Sauvegarde : Export régulier des configurations contrôleurs et du serveur SCADA.
-   Audits périodiques : Revue annuelle de cybersécurité et de conformité.

----------

## 7. Annexes suggérées

1.  Liste des points BACnet (Excel ou base de données).
2.  Fiches techniques des équipements (PICS constructeur).
3.  Schémas unifilaires réseau.
4.  Matrices d'alarmes et priorités.
5.  Plan de formation.
6.  Grille d'évaluation des soumissionnaires (appel d'offres).

----------

Ce dossier constitue une base de travail. Il devra être adapté aux particularités de l'établissement, aux équipements existants et aux exigences précises du donneur d'ouvrage (MSSS, SQI, ou régie interne). Si tu veux que je développe une section en particulier — par exemple la liste de points ou les scénarios de test — dis-le-moi.

dossier complet de conception et de configuration d'un réseau BACnet/IP pour un centre hospitalier universitaire au quebec

# Dossier complet de conception et de configuration d'un réseau BACnet/IP — Centre hospitalier universitaire (Québec)

----------

## Table des matières

1.  [Introduction et contexte](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#1-introduction-et-contexte)
2.  [Cadre normatif et réglementaire](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#2-cadre-normatif-et-r%C3%A9glementaire)
3.  [Analyse des besoins](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#3-analyse-des-besoins)
4.  [Architecture réseau](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#4-architecture-r%C3%A9seau)
5.  [Spécifications techniques BACnet](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#5-sp%C3%A9cifications-techniques-bacnet)
6.  [Adressage et configuration IP](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#6-adressage-et-configuration-ip)
7.  [Sécurité et cybersécurité](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#7-s%C3%A9curit%C3%A9-et-cybers%C3%A9curit%C3%A9)
8.  [Intégration des systèmes](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#8-int%C3%A9gration-des-syst%C3%A8mes)
9.  [Supervision et interface opérateur](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#9-supervision-et-interface-op%C3%A9rateur)
10.  [Plan de mise en œuvre](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#10-plan-de-mise-en-%C5%93uvre)
11.  [Tests et mise en service](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#11-tests-et-mise-en-service)
12.  [Formation et transfert de connaissances](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#12-formation-et-transfert-de-connaissances)
13.  [Exploitation et maintenance](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#13-exploitation-et-maintenance)
14.  [Annexes techniques](https://use.ai/fr/ac077848-a3da-4e74-bb6d-6e68732cf0aa#14-annexes-techniques)

----------

## 1. Introduction et contexte

### 1.1 Présentation du projet

Établissement : Centre hospitalier universitaire de [Nom] — Québec

Objectif général : Déployer une infrastructure de gestion technique du bâtiment (GTB) basée sur le protocole BACnet/IP permettant l'intégration, la supervision et le contrôle centralisé de l'ensemble des systèmes techniques du complexe hospitalier.

Portée géographique :

Bâtiment

Superficie (m²)

Niveaux

Vocation principale

Pavillon principal

45 000

SS + 8

Soins aigus, urgences, bloc opératoire

Pavillon ambulatoire

18 000

SS + 4

Cliniques externes, imagerie

Centre de recherche

12 000

SS + 6

Laboratoires, bureaux

Services techniques

5 000

SS + 2

Chaufferie, électricité, ateliers

Stationnement étagé

25 000

5

Stationnement, accès

Superficie totale : ~105 000 m²

### 1.2 Objectifs spécifiques

1.  Interopérabilité — Intégrer des équipements de fabricants multiples via un protocole ouvert et normalisé.
2.  Centralisation — Permettre la supervision unifiée depuis un poste opérateur GTB et un centre de contrôle 24/7.
3.  Performance énergétique — Soutenir les cibles de réduction de consommation (Plan d'action gouvernemental, LEED v4.1 Santé).
4.  Résilience — Assurer la continuité des systèmes critiques (blocs opératoires, soins intensifs, laboratoires BSL-3).
5.  Cybersécurité — Protéger les infrastructures selon les directives du MSSS et les bonnes pratiques NIST.
6.  Évolutivité — Permettre l'ajout de nouveaux systèmes sans refonte majeure.

### 1.3 Parties prenantes

Rôle

Responsabilité

Maître d'ouvrage (MSSS / SQI / Régie)

Validation des livrables, financement

Chargé de projet GTB

Coordination technique, suivi d'avancement

Firme d'ingénierie

Conception, plans et devis

Intégrateur GTB

Installation, programmation, mise en service

Équipe TI hospitalière

Infrastructure réseau, cybersécurité

Service d'entretien

Exploitation, maintenance préventive

Fabricants / Fournisseurs

Équipements, support technique

----------

## 2. Cadre normatif et réglementaire

### 2.1 Normes BACnet

Norme

Description

ANSI/ASHRAE 135-2020

Spécification complète du protocole BACnet

ISO 16484-5

Équivalent international

ISO 16484-6

Tests de conformité

Addendum BACnet/SC

BACnet Secure Connect (chiffrement TLS)

### 2.2 Normes de construction et CVC

Norme

Application

Code de construction du Québec (CCQ)

Exigences générales

ASHRAE 170-2021

Ventilation des établissements de santé

ASHRAE 90.1-2019

Performance énergétique

CSA Z317.2

Systèmes de chauffage, ventilation et conditionnement d'air dans les établissements de santé

CSA Z32

Sécurité électrique en milieu clinique

NFPA 99

Installations de soins de santé

### 2.3 Cybersécurité et TI

Référence

Portée

Cadre de gestion de la sécurité de l'information — MSSS

Politique provinciale

NIST SP 800-82 Rev. 3

Sécurité des systèmes de contrôle industriels

IEC 62443

Cybersécurité des systèmes d'automatisation

ISO 27001 / 27002

Gestion de la sécurité de l'information

### 2.4 Exigences contractuelles types

-   Tous les équipements BACnet doivent être certifiés BTL (BACnet Testing Laboratories).
-   Les intégrateurs doivent fournir un PICS (Protocol Implementation Conformance Statement) pour chaque famille d'appareils.
-   Les plans et la documentation finale doivent être livrés en format BIM (niveau LOD 350 minimum) et en format natif éditable.

----------

## 3. Analyse des besoins

### 3.1 Systèmes à intégrer

### 3.2 Inventaire estimatif des points

Système

Points physiques

Points logiques

Total estimé

CVC

8 500

4 200

12 700

Éclairage

2 400

1 100

3 500

Énergie

650

350

1 000

Protection incendie

300

150

450

Contrôle d'accès

200

100

300

Transport vertical

80

40

120

Équipements critiques

400

200

600

Total

12 530

6 140

~18 670

### 3.3 Exigences par zone critique

Zone

Classification

Exigences particulières

Blocs opératoires

ISO 5-7

Pression positive, redondance totale, alarmes prioritaires

Soins intensifs

ISO 7

Surveillance continue température/humidité

Laboratoires BSL-3

Confinement

Pression négative, verrouillage séquences

Pharmacie

Contrôlé

Chaîne de froid, alarmes température

Imagerie (IRM)

Spécial

Blindage, refroidissement dédié

Chambres patients

Standard

Confort, économie d'énergie

Urgences

Variable

Flexibilité, temps de réponse rapide

### 3.4 Exigences de performance

Paramètre

Cible

Disponibilité réseau GTB

≥ 99,95 %

Temps de scrutation points critiques

≤ 1 s

Temps de scrutation points standard

≤ 5 s

Latence réseau intra-VLAN

< 10 ms

Temps d'affichage alarme critique

< 3 s

Historisation

1 an en ligne, 7 ans archivés

Capacité d'expansion

+20 % sans modification majeure

----------

## 4. Architecture réseau

### 4.1 Topologie générale

### 4.2 Infrastructure physique

#### 4.2.1 Câblage

Segment

Type de câble

Débit

Remarques

Cœur ↔ Distribution

Fibre monomode OS2

10 Gbps

Liens redondants

Distribution ↔ Contrôleurs

Cat 6A blindé

1 Gbps

PoE+ si requis

MS/TP (legacy)

Câble torsadé 22 AWG

76,8 kbps

Max 4 000 pi / segment

#### 4.2.2 Commutateurs

Niveau

Modèle type

Caractéristiques

Cœur

Cisco Catalyst 9500 / Aruba 8400

Redondance, VSS/VSX, L3

Distribution

Cisco Catalyst 9300 / Aruba 6300

PoE+, IGMP snooping

Accès (si requis)

Cisco IE-4000 / Hirschmann

Industriel, DIN rail

#### 4.2.3 Redondance et résilience

-   Cœur : Paire de commutateurs en configuration empilée virtuelle (VSS/VSX/MLAG).
-   Liens inter-bâtiments : Topologie en anneau ERPS (G.8032) ou RSTP rapide.
-   Alimentation : Double alimentation sur équipements critiques, UPS dédiés dans chaque local technique.
-   Contrôleurs critiques : Configuration maître-esclave avec basculement automatique < 30 s.

### 4.3 Segmentation logique

VLAN

Nom

Plage IP

Usage

200

GTB-CTRL

10.200.10.0/24 à 10.200.49.0/24

Contrôleurs BACnet

201

GTB-SUPERVISION

10.200.1.0/24

Serveurs, postes opérateurs

202

GTB-MSTP

10.200.50.0/24 à 10.200.59.0/24

Routeurs MS/TP

203

GTB-ENERGIE

10.200.60.0/24

Compteurs, analyseurs

204

GTB-SECURITE

10.200.70.0/24

Passerelles incendie, accès

205

GTB-MAINTENANCE

10.200.80.0/24

Laptops techniciens

----------

## 5. Spécifications techniques BACnet

### 5.1 Profils de conformité exigés

Type d'équipement

Profil BIBB minimum

Certification

Serveur GTB

B-OWS

BTL obligatoire

Contrôleur d'immeuble

B-BC

BTL obligatoire

Contrôleur d'application avancé

B-AAC

BTL obligatoire

Contrôleur unitaire

B-ASC

BTL recommandé

Routeur IP/MS/TP

B-RTR

BTL obligatoire

Passerelle tierce

B-GW

PICS requis

### 5.2 Services BACnet requis

#### 5.2.1 Services obligatoires

Catégorie

Services

Accès aux données

ReadProperty, ReadPropertyMultiple, WriteProperty, WritePropertyMultiple

Abonnement

SubscribeCOV, ConfirmedCOVNotification, UnconfirmedCOVNotification

Alarmes

GetAlarmSummary, GetEnrollmentSummary, AcknowledgeAlarm, GetEventInformation

Historiques

ReadRange, CreateObject (Trend Log)

Gestion

DeviceCommunicationControl, ReinitializeDevice, TimeSynchronization, Who-Is, I-Am

Fichiers

AtomicReadFile, AtomicWriteFile

#### 5.2.2 Services recommandés

-   SubscribeCOVProperty (granularité fine)
-   AddListElement / RemoveListElement
-   ConfirmedPrivateTransfer (si intégration propriétaire)

### 5.3 Types d'objets standards

Objet

Code

Usage typique

Analog Input

AI

Température, pression, humidité

Analog Output

AO

Commande de vanne, variateur

Analog Value

AV

Consigne, paramètre calculé

Binary Input

BI

État contact, alarme

Binary Output

BO

Commande marche/arrêt

Binary Value

BV

Mode, état logique

Multi-State Input

MSI

Mode de fonctionnement

Multi-State Output

MSO

Sélection de vitesse

Multi-State Value

MSV

État machine

Schedule

SCH

Horaires hebdomadaires

Calendar

CAL

Jours fériés, exceptions

Trend Log

TL

Historisation locale

Notification Class

NC

Routage des alarmes

Event Enrollment

EE

Définition d'alarme

Loop

LOOP

Boucle PID

Accumulator

ACC

Compteur énergie

### 5.4 Convention de nommage des objets

Format : `[BÂT]-[SYS]-[ZONE]-[ÉQUIP]-[POINT]`

Segment

Description

Exemple

BÂT

Code bâtiment (2 car.)

PP (Pavillon principal)

SYS

Code système (3 car.)

CTA (Centrale traitement d'air)

ZONE

Numéro de zone (3 car.)

301 (3e étage, zone 1)

ÉQUIP

Numéro équipement (2 car.)

01

POINT

Nom du point (abrégé)

TAL (Temp. air local)

Exemple complet : `PP-CTA-301-01-TAL` → Température d'air local, CTA #1, zone 301, Pavillon principal

### 5.5 Numérotation des instances

Plage

Attribution

1 – 999

Objets Device

1000 – 9999

CVC

10000 – 19999

Éclairage

20000 – 29999

Énergie

30000 – 39999

Incendie

40000 – 49999

Contrôle d'accès

50000 – 59999

Transport vertical

60000 – 69999

Équipements critiques

70000+

Réserve

----------

## 6. Adressage et configuration IP

### 6.1 Plan d'adressage détaillé

#### 6.1.1 Serveurs et supervision (VLAN 201)

Équipement

Adresse IP

Masque

Passerelle

Serveur GTB primaire

10.200.1.10

/24

10.200.1.1

Serveur GTB secondaire

10.200.1.11

/24

10.200.1.1

Serveur historique

10.200.1.20

/24

10.200.1.1

Serveur alarmes

10.200.1.21

/24

10.200.1.1

Poste opérateur 1

10.200.1.100

/24

10.200.1.1

Poste opérateur 2

10.200.1.101

/24

10.200.1.1

Poste opérateur 3

10.200.1.102

/24

10.200.1.1

#### 6.1.2 Contrôleurs par bâtiment (VLAN 200)

Pavillon principal :

Contrôleur

Adresse IP

Device Instance

Zone couverte

PP-BC-001

10.200.10.10

101

SS à Niv. 2

PP-BC-002

10.200.10.11

102

Niv. 3 à 5

PP-BC-003

10.200.10.12

103

Niv. 6 à 8

PP-BC-004

10.200.10.13

104

Bloc opératoire

PP-BC-005

10.200.10.14

105

Soins intensifs

PP-AAC-010

10.200.10.20

110

Éclairage

PP-RTR-001

10.200.50.10

151

Routeur MS/TP

Pavillon ambulatoire :

Contrôleur

Adresse IP

Device Instance

PA-BC-001

10.200.11.10

201

PA-BC-002

10.200.11.11

202

PA-AAC-010

10.200.11.20

210

Centre de recherche :

Contrôleur

Adresse IP

Device Instance

CR-BC-001

10.200.12.10

301

CR-BC-002

10.200.12.11

302

CR-AAC-010

10.200.12.20

310

Services techniques :

Contrôleur

Adresse IP

Device Instance

ST-BC-001

10.200.13.10

401

ST-BC-002

10.200.13.11

402

ST-BC-003

10.200.13.12

403

### 6.2 Configuration BACnet/IP

#### 6.2.1 Paramètres réseau

Paramètre

Valeur

Port UDP BACnet/IP

47808 (0xBAC0)

Port UDP BACnet/SC

47809

Adresse de diffusion

10.200.255.255

BBMD activé

Oui (sur serveur GTB)

Foreign Device

Non requis (VLAN unique)

Intervalle BBMD

60 s

#### 6.2.2 Configuration BBMD (BACnet Broadcast Management Device)

Le serveur GTB primaire agit comme BBMD principal :

```
BBMD Address: 10.200.1.10BDT (Broadcast Distribution Table):  - 10.200.1.10/24 (local)  - 10.200.10.0/24 (contrôleurs PP)  - 10.200.11.0/24 (contrôleurs PA)  - 10.200.12.0/24 (contrôleurs CR)  - 10.200.13.0/24 (contrôleurs ST)
```

### 6.3 Configuration des segments MS/TP

Routeur

Adresse MAC MS/TP

Vitesse

Équipements

PP-RTR-001

Segment 1 : 0-127

76,8 kbps

VAV Niv. SS-2 (32 unités)

PP-RTR-001

Segment 2 : 0-127

76,8 kbps

VAV Niv. 3-5 (48 unités)

PP-RTR-001

Segment 3 : 0-127

76,8 kbps

VAV Niv. 6-8 (40 unités)

----------

## 7. Sécurité et cybersécurité

### 7.1 Architecture de sécurité

### 7.2 Segmentation réseau

#### 7.2.1 Règles de pare-feu (ACL)

Source

Destination

Port

Action

Description

VLAN 201

VLAN 200

UDP 47808

Autoriser

Supervision → Contrôleurs

VLAN 200

VLAN 201

UDP 47808

Autoriser

Contrôleurs → Supervision

VLAN 205

VLAN 200

UDP 47808

Autoriser

Maintenance → Contrôleurs

VLAN 200

VLAN IT

*

Bloquer

Isolation GTB

VLAN GTB

NTP (IT)

UDP 123

Autoriser

Synchronisation temps

VLAN GTB

SIEM (IT)

TCP 514

Autoriser

Journalisation

Tout

Tout

*

Bloquer

Règle par défaut

#### 7.2.2 Politique 802.1X

-   Authentification par certificat pour les contrôleurs et serveurs.
-   Authentification MAB (MAC Authentication Bypass) pour les équipements legacy.
-   Profil de sécurité assigné dynamiquement selon le type d'équipement.

### 7.3 BACnet Secure Connect (BACnet/SC)

#### 7.3.1 Déploiement recommandé

Segment

BACnet/IP

BACnet/SC

Serveurs ↔ Contrôleurs principaux

✓

✓ (prioritaire)

Contrôleurs ↔ Contrôleurs

✓

Optionnel

Contrôleurs ↔ Équipements MS/TP

N/A

N/A

Accès maintenance à distance

✗

✓ (obligatoire)

#### 7.3.2 Configuration PKI

-   Autorité de certification (CA) interne dédiée GTB.
-   Certificats X.509 v3, RSA 2048 bits minimum.
-   Durée de validité : 2 ans pour les équipements, 5 ans pour la CA.
-   Liste de révocation (CRL) publiée sur serveur interne.

### 7.4 Gestion des accès

#### 7.4.1 Rôles et privilèges

Rôle

Lecture

Écriture

Configuration

Administration

Opérateur

✓

Limité

✗

✗

Technicien

✓

✓

Limité

✗

Ingénieur

✓

✓

✓

✗

Administrateur

✓

✓

✓

✓

Intégrateur (temporaire)

✓

✓

✓

✗

#### 7.4.2 Politique de mots de passe

-   Longueur minimale : 12 caractères.
-   Complexité : majuscules, minuscules, chiffres, caractères spéciaux.
-   Expiration : 90 jours (comptes utilisateurs), 365 jours (comptes de service).
-   Historique : 12 mots de passe.
-   Verrouillage après 5 tentatives échouées.

### 7.5 Surveillance et journalisation

#### 7.5.1 Événements à journaliser

Catégorie

Événements

Authentification

Connexions réussies/échouées, déconnexions

Configuration

Modifications de paramètres, téléversement de programmes

Alarmes

Toutes les alarmes et acquittements

Réseau

Connexions/déconnexions d'équipements, erreurs de communication

Système

Redémarrages, mises à jour firmware

#### 7.5.2 Rétention des journaux

-   Conservation en ligne : 90 jours.
-   Archivage sécurisé : 7 ans (exigence légale).
-   Format : Syslog vers SIEM hospitalier.

### 7.6 Plan de réponse aux incidents

Phase

Actions

Détection

Alertes SIEM, anomalies trafic réseau, alarmes système

Confinement

Isolation du segment affecté, désactivation des comptes compromis

Éradication

Analyse forensique, suppression des menaces

Récupération

Restauration depuis sauvegarde, revalidation des systèmes

Leçons apprises

Rapport d'incident, mise à jour des procédures

----------

## 8. Intégration des systèmes

### 8.1 CVC (Chauffage, Ventilation, Climatisation)

#### 8.1.1 Centrales de traitement d'air (CTA)

Points typiques par CTA :

Point

Type BACnet

Unité

Description

TAE

AI

°C

Température air extérieur

TAM

AI

°C

Température air mélangé

TAS

AI

°C

Température air soufflé

TAR

AI

°C

Température air repris

HR-S

AI

%

Humidité relative soufflage

PS

AI

Pa

Pression statique gaine

CO2

AI

ppm

Concentration CO2 retour

CMD-VE

AO

%

Commande volet air extérieur

CMD-VR

AO

%

Commande volet recirculation

CMD-VV

AO

%

Commande vanne chauffage

CMD-VF

AO

%

Commande vanne refroidissement

CMD-HUM

AO

%

Commande humidificateur

VIT-VS

AO

%

Vitesse ventilateur soufflage

VIT-VR

AO

%

Vitesse ventilateur retour

ET-VS

BI

—

État ventilateur soufflage

ET-VR

BI

—

État ventilateur retour

AL-FILTRE

BI

—

Alarme filtre colmaté

AL-GEL

BI

—

Alarme gel

MODE

MSV

—

Mode (Arrêt/Auto/Manuel)

CONS-TAS

AV

°C

Consigne température soufflage

CONS-PS

AV

Pa

Consigne pression statique

#### 8.1.2 Unités terminales VAV

Points typiques par VAV :

Point

Type BACnet

Unité

Description

TAL

AI

°C

Température air local

POS-VLT

AI

%

Position volet

DEBIT

AI

L/s

Débit d'air

CMD-VLT

AO

%

Commande volet

CMD-RHC

AO

%

Commande réchauffage

OCC

BI

—

Occupation

CONS-T

AV

°C

Consigne température

CONS-DMIN

AV

L/s

Débit minimum

CONS-DMAX

AV

L/s

Débit maximum

MODE

MSV

—

Mode (Chauffage/Refroid./Mort)

#### 8.1.3 Chaufferie centrale

Équipements :

-   3 chaudières à condensation (6 MW total)
-   4 pompes de distribution (2 actives, 2 secours)
-   Échangeurs de chaleur
-   Systèmes de traitement d'eau

Points critiques :

Point

Type

Description

T-EAU-D

AI

Température eau départ

T-EAU-R

AI

Température eau retour

P-EAU-D

AI

Pression eau départ

DEBIT-EAU

AI

Débit eau circuit

ET-CHAUD-x

BI

État chaudière x

AL-FLAMME-x

BI

Alarme flamme chaudière x

CONS-T-D

AV

Consigne température départ

CMD-CHAUD-x

BV

Commande chaudière x

SEQ-POMPES

MSV

Séquence pompes active

### 8.2 Éclairage

#### 8.2.1 Architecture d'intégration

#### 8.2.2 Points typiques

Point

Type

Description

NIV-ECL

AV

Niveau d'éclairage (0-100%)

CMD-ECL

AO

Commande gradation

ET-ECL

BV

État marche/arrêt

OCC

BI

Détection de présence

LUX

AI

Niveau de luminosité naturelle

SCENE

MSV

Scène active

MODE

MSV

Mode (Auto/Manuel/Nuit)

### 8.3 Gestion de l'énergie

#### 8.3.1 Compteurs et analyseurs

Équipement

Protocole natif

Intégration

Compteurs électriques

Modbus TCP

Passerelle Modbus/BACnet

Compteurs de gaz

Impulsions

Entrée contrôleur

Compteurs d'eau

M-Bus

Passerelle M-Bus/BACnet

Analyseurs de puissance

Modbus TCP

Passerelle Modbus/BACnet

#### 8.3.2 Points de sous-comptage

Point

Type

Unité

Description

KWH

ACC

kWh

Énergie active totale

KVARH

ACC

kVArh

Énergie réactive

KW

AI

kW

Puissance active instantanée

KVAR

AI

kVAr

Puissance réactive

PF

AI

—

Facteur de puissance

V-AB

AI

V

Tension ligne A-B

I-A

AI

A

Courant phase A

THD-V

AI

%

Distorsion harmonique tension

THD-I

AI

%

Distorsion harmonique courant

### 8.4 Protection incendie

#### 8.4.1 Règles d'intégration

-   Lecture seule — Aucune commande ne peut être envoyée au système incendie via BACnet.
-   Isolation galvanique — Passerelle avec séparation optique.
-   Certification — La passerelle doit être listée ULC pour usage avec le panneau incendie.

#### 8.4.2 Points disponibles

Point

Type

Description

ETAT-SYSTEME

MSI

État global (Normal/Alarme/Dérangement)

ZONE-x-ALARME

BI

Alarme zone x

ZONE-x-DERANG

BI

Dérangement zone x

EVACUATE

BI

Signal d'évacuation actif

POMPIER

BI

Mode pompier actif

#### 8.4.3 Désenfumage

Contrôlé via des contrôleurs BACnet dédiés (distincts du panneau incendie) :

Point

Type

Description

CMD-VD-x

BO

Commande volet désenfumage x

POS-VD-x

BI

Position volet (ouvert/fermé)

ET-VENT-DES

BI

État ventilateur désenfumage

CMD-VENT-DES

BO

Commande ventilateur désenfumage

P-CAGE-ESC

AI

Pression cage d'escalier

### 8.5 Contrôle d'accès

#### 8.5.1 Niveau d'intégration

Fonctionnalité

BACnet

Système natif

État des portes

✓

✓

Verrouillage/Déverrouillage portes techniques

✓

✓

Gestion des badges

✗

✓

Configuration

✗

✓

#### 8.5.2 Points BACnet

Point

Type

Description

ETAT-PORTE

BI

État porte (ouverte/fermée)

VERROU

BI

État verrou

CMD-VERROU

BO

Commande verrouillage

FORCEE

BI

Porte forcée

MAINTENUE

BI

Porte maintenue ouverte

### 8.6 Transport vertical

#### 8.6.1 Interface avec ascenseurs

Point

Type

Description

POSITION

MSI

Étage actuel

DIRECTION

MSI

Direction (Haut/Bas/Arrêt)

MODE

MSI

Mode (Normal/Incendie/Maintenance)

EN-SERVICE

BI

Ascenseur en service

ALARME

BI

Alarme cabine

SURCHARGE

BI

Surcharge

### 8.7 Équipements critiques

#### 8.7.1 Groupes électrogènes

Point

Type

Description

ETAT-GEN

MSI

État (Arrêt/Préchauffage/Marche/Refroidissement)

V-GEN

AI

Tension générée

I-GEN

AI

Courant généré

KW-GEN

AI

Puissance active

FREQ

AI

Fréquence

T-MOTEUR

AI

Température moteur

P-HUILE

AI

Pression huile

NIV-CARB

AI

Niveau carburant

HEURES

AI

Heures de fonctionnement

AL-DEFAUT

BI

Alarme défaut

AL-SURCHARGE

BI

Alarme surcharge

#### 8.7.2 Onduleurs (UPS)

Point

Type

Description

MODE

MSI

Mode (Normal/Batterie/Bypass)

CHARGE

AI

Charge (%)

BATT-AUTON

AI

Autonomie batterie (min)

BATT-TEMP

AI

Température batteries

V-ENTREE

AI

Tension entrée

V-SORTIE

AI

Tension sortie

AL-BATT

BI

Alarme batterie faible

AL-SURCH

BI

Alarme surcharge

#### 8.7.3 Air médical et vide

Point

Type

Description

P-AIR-MED

AI

Pression air médical

P-VIDE

AI

Pression vide

P-N2O

AI

Pression N₂O

P-O2

AI

Pression O₂

AL-P-BASSE

BI

Alarme pression basse

AL-P-HAUTE

BI

Alarme pression haute

ET-COMP-x

BI

État compresseur x

ET-POMPE-x

BI

État pompe vide x

----------

## 9. Supervision et interface opérateur

### 9.1 Architecture logicielle

### 9.2 Exigences fonctionnelles

#### 9.2.1 Affichage graphique

-   Graphiques vectoriels (SVG) avec symboles normalisés.
-   Navigation hiérarchique : Site → Bâtiment → Système → Équipement.
-   Temps de chargement d'une page < 3 secondes.
-   Rafraîchissement automatique des valeurs ≤ 5 secondes.
-   Affichage adaptatif (responsive) pour tablettes et mobiles.

#### 9.2.2 Gestion des alarmes

Priorité

Couleur

Délai d'acquittement

Notification

Critique (1)

Rouge clignotant

Immédiat

SMS + Appel

Urgente (2)

Rouge fixe

< 5 min

SMS

Normale (3)

Orange

< 30 min

Courriel

Informative (4)

Jaune

< 4 h

Journal

Fonctionnalités requises :

-   Acquittement avec commentaire obligatoire.
-   Escalade automatique si non acquittée.
-   Historique complet avec horodatage.
-   Filtrage et recherche multicritères.
-   Rapport d'alarmes quotidien/hebdomadaire automatique.

#### 9.2.3 Historisation et tendances

-   Stockage de toutes les valeurs analogiques à intervalle configurable (défaut : 15 min).
-   Stockage sur changement d'état pour les points binaires.
-   Historisation des alarmes et événements.
-   Interface de consultation avec graphiques interactifs.
-   Export en CSV, Excel, PDF.

#### 9.2.4 Horaires et calendriers

-   Horaires hebdomadaires avec 8 périodes par jour minimum.
-   Calendrier d'exceptions (jours fériés, événements spéciaux).
-   Horaires par zone, système ou équipement.
-   Interface de modification conviviale.

#### 9.2.5 Rapports automatisés

Rapport

Fréquence

Contenu

Consommation énergétique

Quotidien

kWh, gaz, eau par bâtiment

Bilan climatique

Hebdomadaire

DJC, DJR, heures de fonctionnement

Performance CVC

Mensuel

Efficacité, anomalies, maintenance

Alarmes

Quotidien

Résumé par priorité et système

Disponibilité

Mensuel

Uptime réseau et systèmes

### 9.3 Postes opérateurs

#### 9.3.1 Configuration matérielle

Composant

Spécification

Processeur

Intel Core i7 ou équivalent

Mémoire

16 Go RAM

Stockage

SSD 512 Go

Écrans

2 × 27" 4K minimum

Réseau

Gigabit Ethernet

#### 9.3.2 Emplacements

Poste

Emplacement

Fonction

GTB-WS-01

Salle de contrôle, Services techniques

Supervision principale 24/7

GTB-WS-02

Bureau chef mécanicien

Gestion et configuration

GTB-WS-03

Salle de garde, Sécurité

Consultation alarmes

----------

## 10. Plan de mise en œuvre

### 10.1 Phases du projet

### 10.2 Livrables par phase

Phase

Livrables

Études préliminaires

Rapport d'audit existant, analyse des besoins

Conception détaillée

Plans réseau, liste de points, spécifications, devis

Infrastructure

Certificat d'installation câblage, rapport de tests

Contrôleurs

PICS, programmes sources, rapports de tests unitaires

Supervision

Manuel d'exploitation, graphiques, configurations

Intégration

Rapport de tests FAT/SAT, procès-verbal de réception

Formation

Supports de formation, attestations

Mise en service

Documentation finale (DOE), manuel d'entretien

### 10.3 Jalons clés

Date

Jalon

2026-08-15

Approbation de la conception détaillée

2026-10-01

Attribution des contrats

2027-01-15

Infrastructure réseau complétée

2027-05-15

Installation contrôleurs terminée

2027-09-15

Tests d'acceptation réussis

2027-11-15

Mise en service complète

----------

## 11. Tests et mise en service

### 11.1 Tests d'usine (FAT - Factory Acceptance Test)

#### 11.1.1 Tests des contrôleurs

Test

Critère de réussite

Conformité PICS

100 % des services déclarés fonctionnels

Communication BACnet/IP

Who-Is/I-Am réussi

Lecture/Écriture

Tous les points accessibles

COV

Notifications reçues dans les 5 s

Alarmes

Génération et routage corrects

Tendances

Historisation fonctionnelle

Horaires

Exécution aux heures prévues

Séquences

Comportement conforme à la description

#### 11.1.2 Tests de la plateforme GTB

Test

Critère de réussite

Découverte réseau

Tous les contrôleurs détectés

Import base de données

Tous les points importés

Affichage graphique

Valeurs temps réel correctes

Commandes

Écriture effective sur les points

Alarmes

Affichage < 3 s après génération

Historiques

Données consultables

Rapports

Génération automatique fonctionnelle

### 11.2 Tests sur site (SAT - Site Acceptance Test)

#### 11.2.1 Tests de communication

Test

Procédure

Critère

Connectivité

Ping de chaque équipement

100 % de réponse

Latence

Mesure temps aller-retour

< 10 ms intra-VLAN

Bande passante

Test iperf entre segments

> 100 Mbps

Redondance

Coupure lien principal

Basculement < 30 s

BBMD

Who-Is global

Tous les devices visibles

#### 11.2.2 Tests fonctionnels par système

CVC :

Test

Procédure

Critère

Démarrage CTA

Commande via GTB

Ventilateurs en marche < 60 s

Régulation température

Modification consigne

Stabilisation ± 0,5 °C en 15 min

Pression statique

Modification consigne

Stabilisation ± 5 Pa en 5 min

Alarme filtre

Simulation pression différentielle

Alarme générée < 10 s

Séquence gel

Simulation T < 4 °C

Arrêt CTA, ouverture vannes

Éclairage :

Test

Procédure

Critère

Gradation

Commande 0-100 %

Variation linéaire

Scène

Activation scène

Niveaux conformes

Détection présence

Entrée/sortie zone

Allumage/extinction

Horaire

Hors horaire occupation

Extinction automatique

Énergie :

Test

Procédure

Critère

Lecture compteurs

Comparaison affichage local

Écart < 1 %

Accumulation

Suivi sur 24 h

Cohérence avec facturation

Alarme surconsommation

Simulation dépassement

Alarme générée

#### 11.2.3 Tests de performance globale

Test

Procédure

Critère

Charge réseau

Scrutation simultanée 10 000 points

Latence < 100 ms

Rafale d'alarmes

Génération 100 alarmes/min

Affichage sans perte

Historisation

Enregistrement 5 000 points/15 min

Aucune perte de données

Récupération

Coupure serveur primaire

Basculement < 60 s

### 11.3 Tests de cybersécurité

Test

Procédure

Critère

Scan de ports

Nmap depuis VLAN IT

Seuls ports autorisés ouverts

Authentification

Tentative accès sans identifiants

Refus d'accès

Chiffrement

Capture trafic BACnet/SC

Données chiffrées

Journalisation

Actions diverses

Événements dans SIEM

Mots de passe

Test dictionnaire

Résistance > 10⁸ essais

### 11.4 Documentation des tests

Procès-verbal de test (contenu minimal) :

1.  Identification du test (numéro, nom, date)
2.  Équipements testés
3.  Procédure détaillée
4.  Résultats attendus
5.  Résultats obtenus
6.  Écarts et correctifs
7.  Conclusion (Réussi / Réussi avec réserves / Échoué)
8.  Signatures (Intégrateur, Maître d'œuvre, Client)

----------

## 12. Formation et transfert de connaissances

### 12.1 Programme de formation

Module

Durée

Public cible

Contenu

Sensibilisation BACnet

4 h

Tous

Concepts de base, terminologie

Exploitation GTB

16 h

Opérateurs

Navigation, alarmes, commandes, rapports

Maintenance niveau 1

24 h

Techniciens

Diagnostic, remplacement équipements

Maintenance niveau 2

40 h

Techniciens seniors

Programmation, configuration réseau

Administration

24 h

Ingénieurs

Gestion utilisateurs, sauvegarde, sécurité

Cybersécurité OT

8 h

TI + GTB

Bonnes pratiques, réponse incidents

### 12.2 Documentation à remettre

Document

Format

Quantité

Manuel d'exploitation

PDF + papier

3 copies

Manuel de maintenance

PDF + papier

3 copies

Guide de dépannage

PDF

Électronique

Plans réseau à jour

DWG + PDF

Électronique

Liste de points

Excel + CSV

Électronique

Configurations contrôleurs

Fichiers natifs

Électronique

Programmes sources

Fichiers natifs

Électronique

PICS de tous les équipements

PDF

Électronique

Procès-verbaux de tests

PDF

Électronique

### 12.3 Transfert de connaissances

-   Accompagnement sur site pendant les 30 premiers jours suivant la mise en service.
-   Ligne d'assistance téléphonique 24/7 pendant 90 jours.
-   Sessions de perfectionnement après 6 mois d'exploitation.

----------

## 13. Exploitation et maintenance

### 13.1 Organisation

### 13.2 Niveaux de support

Niveau

Responsable

Délai intervention

Exemples

1

Opérateur interne

Immédiat

Acquittement alarmes, commandes

2

Technicien interne

< 4 h

Remplacement capteur, reset contrôleur

3

Ingénieur / Intégrateur

< 24 h

Modification programme, diagnostic avancé

4

Fabricant

Selon contrat

Défaut matériel, mise à jour firmware

### 13.3 Maintenance préventive

#### 13.3.1 Calendrier

Tâche

Fréquence

Responsable

Vérification des alarmes actives

Quotidien

Opérateur

Revue des tendances

Hebdomadaire

Technicien

Sauvegarde configurations

Hebdomadaire

Automatique

Vérification communication

Mensuel

Technicien

Test des redondances

Trimestriel

Ingénieur

Mise à jour firmware

Semestriel

Intégrateur

Audit cybersécurité

Annuel

TI + Externe

Calibration capteurs critiques

Annuel

Technicien

Revue des performances

Annuel

Ingénieur

#### 13.3.2 Procédure de sauvegarde

1.  Configurations contrôleurs : Export automatique hebdomadaire vers serveur de fichiers.
2.  Base de données GTB : Sauvegarde quotidienne incrémentale, hebdomadaire complète.
3.  Historiques : Archivage mensuel vers stockage long terme.
4.  Rétention :
    -   En ligne : 90 jours
    -   Archive : 7 ans

### 13.4 Gestion des modifications

Étape

Description

Demande

Formulaire de demande de modification

Évaluation

Analyse d'impact par l'ingénieur GTB

Approbation

Validation par le chef de service

Planification

Fenêtre de maintenance, communication

Exécution

Réalisation avec sauvegarde préalable

Test

Vérification du bon fonctionnement

Documentation

Mise à jour plans et listes de points

Clôture

Rapport de modification

### 13.5 Indicateurs de performance (KPI)

Indicateur

Cible

Fréquence de suivi

Disponibilité réseau GTB

≥ 99,95 %

Mensuel

Temps moyen de résolution alarme critique

< 30 min

Mensuel

Nombre d'alarmes non acquittées > 24 h

0

Quotidien

Points en défaut de communication

< 0,5 %

Hebdomadaire

Sauvegarde réussie

100 %

Hebdomadaire

Formation du personnel à jour

100 %

Annuel

----------

## 14. Annexes techniques

### Annexe A — Liste de points type (extrait)

Nom du point

Description

Type

Unité

Plage

COV

Tendance

PP-CTA-301-01-TAE

Temp. air extérieur CTA-301-01

AI

°C

-40 à 50

0,5

15 min

PP-CTA-301-01-TAS

Temp. air soufflé CTA-301-01

AI

°C

5 à 35

0,2

15 min

PP-CTA-301-01-CMD-VV

Cmd vanne chauff. CTA-301-01

AO

%

0 à 100

2

15 min

PP-CTA-301-01-ET-VS

État ventilateur soufflage

BI

—

0/1

—

Sur chgmt

PP-CTA-301-01-AL-GEL

Alarme gel CTA-301-01

BI

—

0/1

—

Sur chgmt

PP-CTA-301-01-CONS-TAS

Consigne T soufflage

AV

°C

10 à 30

0,5

Sur chgmt

PP-CTA-301-01-MODE

Mode CTA-301-01

MSV

—

0-4

—

Sur chgmt

PP-VAV-301-01-TAL

Temp. air local VAV-301-01

AI

°C

15 à 30

0,2

15 min

PP-VAV-301-01-POS-VLT

Position volet VAV-301-01

AI

%

0 à 100

5

15 min

PP-VAV-301-01-DEBIT

Débit VAV-301-01

AI

L/s

0 à 500

10

15 min

### Annexe B — Matrice d'alarmes (extrait)

Code

Description

Priorité

Délai

Escalade

Actions

AL-GEL

Alarme gel

1

Imm.

Chef méc. 15 min

Arrêt CTA, ouverture vannes

AL-INCENDIE

Signal incendie

1

Imm.

Sécurité

Modes évacuation

AL-PANNE-GEN

Panne génératrice

1

Imm.

Chef élec. 10 min

Basculement secours

AL-FILTRE

Filtre colmaté

3

4 h

Technicien

Planifier remplacement

AL-T-HORS-LIM

Température hors limites

2

30 min

Technicien

Diagnostic CVC

AL-COMM

Perte communication

2

15 min

Ingénieur

Diagnostic réseau

### Annexe C — Schéma unifilaire réseau (simplifié)

```
┌─────────────────────────────────────────────────────────────────────────┐│                           PARE-FEU EXTERNE                              │└────────────────────────────────┬────────────────────────────────────────┘                                 │                                 ▼┌─────────────────────────────────────────────────────────────────────────┐│                              DMZ                                         ││  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐              ││  │   VPN/RAS    │    │   Serveur    │    │   Reverse    │              ││  │              │    │   de rebond  │    │    Proxy     │              ││  └──────────────┘    └──────────────┘    └──────────────┘              │└────────────────────────────────┬────────────────────────────────────────┘                                 │                                 ▼┌─────────────────────────────────────────────────────────────────────────┐│                         PARE-FEU INTERNE                                │└────────────────────────────────┬────────────────────────────────────────┘                                 │         ┌───────────────────────┼───────────────────────┐         │                       │                       │         ▼                       ▼                       ▼┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐│   CŒUR RÉSEAU   │   │   CŒUR RÉSEAU   │   │  PARE-FEU GTB   ││       IT        │   │       IT        │   │                 ││  (Primaire)     │◄──►│  (Secondaire)   │   │                 │└────────┬────────┘   └────────┬────────┘   └────────┬────────┘         │                     │                      │         └──────────────────────────────────────┐     │                                                │     │                                                ▼     ▼                              ┌─────────────────────────────────────┐                              │     COMMUTATEURS CŒUR GTB           │                              │       (Stack VSS/MLAG)              │                              │                                     │                              │  ┌───────┐         ┌───────┐       │                              │  │SW-GTB │◄────────►│SW-GTB │       │                              │  │  -01  │         │  -02  │       │                              │  └───┬───┘         └───┬───┘       │                              └──────┼─────────────────┼───────────┘                                     │                 │         ┌───────────┬───────────────┼─────────────────┼───────────────┐         │           │               │                 │               │         ▼           ▼               ▼                 ▼               ▼   ┌─────────┐ ┌─────────┐    ┌─────────┐       ┌─────────┐     ┌─────────┐   │ Serveur │ │ Serveur │    │SW-DIST  │       │SW-DIST  │     │SW-DIST  │   │GTB Prim.│ │GTB Sec. │    │  PP     │       │  PA     │     │  CR     │   └─────────┘ └─────────┘    └────┬────┘       └────┬────┘     └────┬────┘                                   │                  │               │                              ┌────┴────┐        ┌────┴────┐     ┌────┴────┐                              │         │        │         │     │         │                              ▼         ▼        ▼         ▼     ▼         ▼                         ┌────────┐┌────────┐┌────────┐┌────────┐┌────────┐                         │BC-001  ││BC-002  ││BC-001  ││BC-001  ││BC-002  │                         │(CVC)   ││(CVC)   ││(CVC)   ││(CVC)   ││(Labo)  │                         └────────┘└────────┘└────────┘└────────┘└────────┘
```

### Annexe D — Gabarit PICS (Protocol Implementation Conformance Statement)

```
================================================================BACNET PROTOCOL IMPLEMENTATION CONFORMANCE STATEMENT (PICS)================================================================Date: ____________________Vendor: __________________Product Name: ____________Model Number: ____________Firmware Version: ________BACnet Protocol Revision: 24 (ANSI/ASHRAE 135-2020)DEVICE PROFILE: [ ] B-OWS  [ ] B-BC  [ ] B-AAC  [ ] B-ASC  [ ] B-RTRNETWORK OPTIONS:[ ] BACnet/IP (Annex J)    [ ] BBMD    [ ] Foreign Device[ ] BACnet/SC (Addendum BJ)[ ] MS/TP (Annex G)    [ ] Master    [ ] SlaveSEGMENTATION:[ ] Segmented requests supported[ ] Segmented responses supportedMax APDU: _________STANDARD OBJECT TYPES SUPPORTED:[ ] Analog Input      [ ] Analog Output     [ ] Analog Value[ ] Binary Input      [ ] Binary Output     [ ] Binary Value[ ] Multi-State Input [ ] Multi-State Output[ ] Multi-State Value[ ] Calendar          [ ] Schedule          [ ] Trend Log[ ] Loop              [ ] Notification Class[ ] Event Enrollment[ ] Accumulator       [ ] Device            [ ] FileSTANDARD APPLICATION SERVICES:Read Property Services:[ ] ReadProperty      [ ] ReadPropertyMultiple [ ] ReadRangeWrite Property Services:[ ] WriteProperty     [ ] WritePropertyMultipleObject Management:[ ] CreateObject      [ ] DeleteObjectAlarm & Event Services:[ ] AcknowledgeAlarm  [ ] GetAlarmSummary  [ ] GetEnrollmentSummary[ ] GetEventInformation[ ] SubscribeCOV    [ ] SubscribeCOVPropertyDevice Management:[ ] Who-Is            [ ] I-Am             [ ] Who-Has            [ ] I-Have[ ] TimeSynchronization[ ] UTCTimeSynchronization[ ] DeviceCommunicationControl [ ] ReinitializeDeviceFile Services:[ ] AtomicReadFile    [ ] AtomicWriteFilePrivate Transfer:[ ] ConfirmedPrivateTransfer [ ] UnconfirmedPrivateTransfer================================================================
```

### Annexe E — Checklist de mise en service

Phase 1 — Infrastructure réseau

-   Câblage conforme aux spécifications
-   Tests de certification câblage (rapport)
-   Commutateurs installés et sous tension
-   VLANs configurés
-   Adressage IP vérifié
-   Connectivité entre segments confirmée
-   Redondance testée

Phase 2 — Contrôleurs BACnet

-   Contrôleurs installés et alimentés
-   Adresses IP assignées
-   Device Instance uniques
-   Communication BACnet vérifiée (Who-Is/I-Am)
-   Points accessibles en lecture/écriture
-   Câblage terrain vérifié
-   E/S testées individuellement

Phase 3 — Programmation

-   Séquences programmées
-   Paramètres de régulation ajustés
-   Horaires configurés
-   Alarmes définies
-   Tendances activées
-   Tests fonctionnels réussis

Phase 4 — Supervision GTB

-   Serveurs installés et configurés
-   Communication avec tous les contrôleurs
-   Base de données de points importée
-   Graphiques créés
-   Alarmes routées correctement
-   Historiques fonctionnels
-   Rapports configurés
-   Utilisateurs et droits créés

Phase 5 — Tests d'acceptation

-   Tests de conformité BACnet réussis
-   Tests fonctionnels par système réussis
-   Tests de performance réussis
-   Tests de cybersécurité réussis
-   Procès-verbaux signés

Phase 6 — Formation et documentation

-   Formation opérateurs complétée
-   Formation techniciens complétée
-   Documentation finale remise
-   Plans à jour remis
-   Sauvegardes initiales effectuées

### Annexe F — Contacts et ressources

Ressource

Contact

Usage

BACnet International

Normes, certification BTL

ASHRAE

Standard 135, guides

Régie du bâtiment du Québec

Réglementation

MSSS - Sécurité de l'information

Intranet RSSS

Politiques cybersécurité

Intégrateur GTB

[À compléter]

Support technique

Fabricant contrôleurs

[À compléter]

Support produit

Fabricant GTB

[À compléter]

Support logiciel

----------

## Signatures et approbations

Rôle

Nom

Signature

Date

Chargé de projet

Ingénieur mécanique

Ingénieur électrique

Responsable TI

Représentant du client

----------

_Document préparé conformément aux exigences du Ministère de la Santé et des Services sociaux du Québec et aux bonnes pratiques de l'industrie._

_Version : 1.0_ _Date : Mai 2026_

----------

Ce dossier couvre les principaux aspects d'un projet BACnet/IP en milieu hospitalier. Certaines sections devront être adaptées aux spécificités de l'établissement (superficie réelle, équipements existants, exigences particulières du donneur d'ouvrage). Si tu souhaites approfondir une section — par exemple les séquences de contrôle détaillées, les gabarits de graphiques, ou les procédures de test spécifiques — je peux développer davantage.

La recherche approfondie est en cours d'initialisation

### Sources

Aucune source trouvée
