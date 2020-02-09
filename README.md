# :eyeglasses: Carte_Capteurs_2020
------------------------------------------------------------------------

Code pour la carte capteur du robot de la CDR 2020

Le but de cette carte est de récolter toutes les informations envoyées par les différents capteurs, d'en faire la synthèse et d'envoyer le bilan à la carte principale. Elle permet d'avoir une représentation précise de l'environnement du robot.

Il y a différents types de capteurs : les capteurs embarqués sur le robots et les capteurs déportés.

-----

**:clipboard: ToDo:**
-
- [x] Récupérer les données du lidar
- [ ] Récupérer les données de la caméra
- [ ] Récupérer les données des Tofs
- [ ] Déduire la position d'un robot
- [ ] Envoyer la position des robots et des gobelets à la carte principale
- [ ] Transferrer les informations de la caméra vers la carte principale
- [ ] Envoyer les distances tofs 
- [ ] Arrêter le robot en cas de danger immédiat
- [ ] Tracking des robots pour anticiper leurs déplacements

-----

**:trophy: Goal:**
-
- Connaître la position des robots et des gobelets à tout instant 
- Recalibrer le robot de façon efficace
- Empêcher les collisions entre robots

---
**:memo: Liste des capteurs:**
- 
**Caméra:**
Posée sur le mat central elle a une vision globale sur le terrain. Elle repère la position des différents robots et des gobelets. Elle vérifie que les actions ont bien été réussies.

- communication sans fils avec les robots via XBee
- traitement du flux vidéo avec une raspberry pi
- technique de comparaison d'image avec et sans robot pour détecter sa position

Il y a un repository dédié au code de la rasberry pi

**Lidar:**
Situé sur le robot, il scanne les alentours de celui-ci à hauteur du support balise. Grâce à lui, on peut croiser les informations de la caméra avec un capteur embarqué. Il faut analyser les points reçus afin de déterminer s'ils sont dant le terrain ou non. De plus, en détectant le support central il peut donner une information supplémentaire sur la position du robot

- ref du lidar : RPLidar a1
- communication avec la carte capteur via une liaison série
- résolution angulaire : ~ 1°

**Time of Flight:**
Ce sont des télémètres laser que nous utiliseront principalement dans la fonction de recalibrage du robot. En les plaçants a des positions stratégiques, il peuvent nous donner des informations sur l'angle du robot par rapport aux murs et ainsi corriger l'erreur cumulée des codurs incrémentaux.

- ref des capteurs : GY-VL53L0XV2
- communication avec la carte capteur via un bus i2c + 1pin digital de mise en route


                                                Camera
                                              _________
                                                |   |
                                                |   |
                                                |   |
                                                |   |   Système de repérage
                                                |   |   central
                                                |   | 
               lidar                            |   |
              _______                           |   |
             |       |                          |   |
             | Robot |                          |   | 
             |_______|                          |___|
---


**:pushpin: Bilan des ports utilisés:**
-
- 4 liaisons séries : caméra, lidar, carte principale, débug
- 1 i2c : tofs
- 6 digital output : tofs
- 5V moteur : lidar

