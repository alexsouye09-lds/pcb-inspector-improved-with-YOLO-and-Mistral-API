PCB Inspector 
Description du projet

PCB Inspector est un pipeline intelligent de détection et d’analyse de défauts sur des cartes de circuits imprimés (PCB) pour un usage industriel. Le projet combine Computer Vision et IA conversationnelle afin de générer automatiquement un plan d’action précis pour réparer ou contrôler les cartes.

Le pipeline complet fonctionne ainsi :

Détection des défauts avec YOLO

Modèle YOLO custom entraîné pour détecter différents types de défauts :

shorts (courts-circuits)

missing holes (trous manquants)

mouse bites (morsures sur les bords)

Sortie : JSON listant chaque défaut avec sa bounding box et son niveau de confiance.

Analyse et plan d’action avec Mistral Agent

L’agent reçoit les détections YOLO + image annotée.

Génère automatiquement :

Un plan d’action étape par étape

La priorité de chaque défaut (faible / moyenne / élevée)

Une analyse visuelle détaillée pour chaque défaut.

Sortie : JSON structuré prêt à l’emploi pour reporting ou dashboard.

Pipeline multimodal

L’agent peut “voir” l’image annotée pour valider la localisation et la gravité des défauts.

Permet un contrôle précis et une analyse plus fiable qu’un simple JSON.

Fonctionnalités principales

Détection automatisée de défauts PCB avec YOLO custom

Plan d’action intelligent généré par Mistral Agent

Analyse visuelle complète avec localisation exacte des défauts

Pipeline multimodal : texte + image

JSON structuré exploitable pour dashboard ou reporting

Prêt pour proof of concept: upload image → résultat immédiat

Structure du projet
pcb-inspector-hackathon/
│
├─ README.md
├─ requirements.txt
├─ pcb_yolo_agent.ipynb      # Notebook Colab prêt à l'emploi
├─ models/
│   └─ pcb_model.pt          # Modèle YOLO custom
├─ images/
│   └─ PCB_DATASET/          # Dataset d’exemple
└─ outputs/
    └─ annotated_pcb.jpg     # Sortie YOLO
Instructions pour exécuter le projet

Installer les dépendances :

pip install -r requirements.txt

Préparer votre modèle YOLO custom et les images PCB.

Exécuter le notebook pcb_yolo_agent.ipynb :

Chargement du modèle YOLO

Détection des défauts

Analyse automatique par l’agent Mistral

Génération du JSON final prêt à l’emploi

(Optionnel) Afficher les résultats annotés et générer un rapport PDF ou un dashboard.

Technologies utilisées

YOLO (Ultralytics) pour la détection de défauts

Mistral AI Agent pour l’analyse intelligente et génération de plan d’action

Python (Colab compatible)

JSON pour la structuration des données

(Optionnel) Streamlit pour dashboard interactif

Résultat attendu

Après exécution, vous obtenez :

{
  "instructions": [
    "Inspecter immédiatement les zones identifiées comme ayant des courts-circuits.",
    "Vérifier les zones de morsure de souris pour évaluer l'impact sur la fonctionnalité du PCB.",
    "Documenter les défauts et prendre des photos pour référence.",
    "Consulter les spécifications techniques du PCB.",
    "Planifier des tests de fonctionnalité pour les zones affectées."
  ],
  "priorité": "élevée",
  "analyse_visuelle": {
    "défaut": "short",
    "description": "Trois courts-circuits détectés avec des niveaux de confiance élevés. Un défaut de morsure de souris détecté avec un niveau de confiance modéré.",
    "localisation": [
      {"défaut": "short", "bbox": [1010.32, 1369.04, 1074.22, 1426.96], "confidence": 0.76},
      {"défaut": "short", "bbox": [1491.73, 1313.68, 1552.59, 1372.44], "confidence": 0.66},
      {"défaut": "mouse_bite", "bbox": [761.91, 813.44, 838.55, 863.78], "confidence": 0.56}
    ]
  }
}
