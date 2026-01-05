# Projet de session en programmation graphique et en base de données

Par Charles Ouellet et Brayan Dyvan Lando Longmene

Application WinUI 3 permettant la gestion complète d’activités, de séances, d’adhérents et de statistiques, connectée à une base de données MySQL.


# Sommaire
--------
- [Description](#description)  
- [Fonctionnalités](#fonctionnalités)
  
# Description

Elle offre :

    une interface moderne
    
    une gestion complète des activités, séances et adhérents
    
    un système d’inscription
    
    un module de notation
    
    des statistiques avancées
    
    une gestion des rôles (admin / adhérent)
    
    L’application communique avec une base MySQL via des procédures stockées, fonctions et triggers.

# Fonctionnalités

Adhérent

    Consulter les activités
    
    Voir les séances disponibles
    
    S’inscrire à une séance (si places disponibles)
    
    Noter les séances auxquelles il a participé
    
    Voir son historique de séances
    
Administrateur

    Ajouter / modifier / supprimer :
    
    activités
    
    séances
    
    adhérents
    
    Consulter toutes les statistiques
    
    Gérer les inscriptions
    
    Accéder à des pages réservées via le menu de navigation

Statistiques

    Nombre total d’adhérents
    
    Nombre total d’activités
    
    Nombre d’adhérents par activité
    
    Activité la mieux notée
    
    Participant le plus actif
    
    Activité avec le plus de séances
    
    Moyenne des notes par activité

# Architecture du projet

Interface (XAML)

    Affichage.xaml — page principale
    
    Seances.xaml — liste des séances d’une activité
    
    ModifierSeance.xaml — modification d’une séance
    
    Connexion.xaml — connexion adhérent / admin
    
    PageStatistiques.xaml — statistiques
    
    PageNotesSeances.xaml — notation des séances
    
Logique (C#)

- Singleton.cs
  
      gestion de la base MySQL
      
      CRUD complet
      
      gestion des rôles
      
      statistiques
      
      gestion des inscriptions
  
- SingletonNavigation.cs
  
      gestion du NavigationView
      
      visibilité des pages selon le rôle
  
- Modèles
  
      Activite, ActiviteForm
      
      Seance, seanceForm
      
      Adherent
      
      SeanceNote
  
# Structure de la base de données

Tables principales

    Administrateur
    
    Activites
    
    Categories
    
    Categories_Activites
    
    Seances
    
    Adherents
    
    noteAppreciation
    
    Seances_Adherents_NoteAppreciation

Relations

    1 activité → plusieurs séances
    
    1 adhérent → plusieurs inscriptions
    
    1 séance → plusieurs participants
    
    1 participant → 1 note par séance
    
# Triggers, vues et procédures

- Triggers

    génération automatique du matricule adhérent
    
    vérification de l’âge minimum (18 ans)
    
    contrôle du nombre de places disponibles
    
    mise à jour automatique du nombre de places

- Vues

    ParticipantPlusActif
    
    PrixMoyenParParticipant
    
    NotesDesActivités
    
    MoyenneDesNotes
    
    nbParticipant
    
    nbParticipantMoyParMois

- Procédures stockées

    AffActivite
    
    AffSeance
    
    AjoutActivite, ModifActivite, SuppActivite
    
    AjoutSeance, ModifSeance, SuppSeance
    
    AjoutAdherent, ModifAdherent, SuppAdherent
    
    SeanceAdherent
    
    NoterSeance
    
    ParticipantPopulaire
    
    ActiviteMieuxNote
    
    SeancePopulaire
    
- Fonctions SQL

    f_verifier_adherent
    
    f_verifier_admin
    
    f_verifier_admin_MDP
    
    f_verifier_seance_adherent
    
    f_get_Nom
