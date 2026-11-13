# 08. Migrer

Inspiré de : le motif *Strangler Fig* (Martin Fowler), les tests de caractérisation (Michael Feathers).

Une migration de socle (version de langage, framework, base de données, hébergement) est le moment où une équipe perd le plus facilement la confiance de ses utilisateurs. Rien de visible ne change pour eux ; tout ce qui casse leur paraît donc gratuit.

## Règle 1 : figer le comportement

```mermaid
%%{init: {'theme':'base','themeVariables':{'primaryColor':'#FF2E88','primaryTextColor':'#ffffff','primaryBorderColor':'#FF2E88','lineColor':'#FCAF17','secondaryColor':'#2A0F3D','tertiaryColor':'#FFF0F6','clusterBkg':'#FFF0F6','clusterBorder':'#FF2E88','titleColor':'#12091F','edgeLabelBackground':'#12091F','textColor':'#12091F','transitionLabelColor':'#ffffff','fontFamily':'Segoe UI, Helvetica, Arial, sans-serif','cScale0':'#FF2E88','cScaleLabel0':'#ffffff','cScale1':'#FF7A3D','cScaleLabel1':'#ffffff','cScale2':'#FCAF17','cScaleLabel2':'#12091F','cScale3':'#2EE6A6','cScaleLabel3':'#12091F','cScale4':'#28D9E8','cScaleLabel4':'#12091F','cScale5':'#C04DFF','cScaleLabel5':'#ffffff','cScale6':'#7A5CFF','cScaleLabel6':'#ffffff','cScale7':'#FF4F70','cScaleLabel7':'#ffffff'}}}%%
flowchart LR
  A["Filet de caractérisation sur l'existant"] --> B{"Vert sur l'ancien socle ?"}
  B -->|non| A
  B -->|oui| C["Migrer un périmètre"]
  C --> D["Ancien et nouveau en parallèle"]
  D --> E{"Écarts expliqués ?"}
  E -->|non| F["Analyser, sans corriger les bugs"]
  F --> D
  E -->|oui| G["Bascule"]
  G --> H["Périmètre suivant"]
  H --> C
```

Pendant une migration, on ne corrige aucun bug. Même évident, même ancien, même gênant. On le note, on le garde pour après.

La raison est simple : si le comportement change pendant la migration, personne ne peut plus dire si l'écart vient de la migration ou de la correction. Une seule variable à la fois.

## Règle 2 : le filet se joue sur l'existant

Avant de toucher quoi que ce soit, on écrit les tests qui photographient ce que fait le système **aujourd'hui, sur sa pile actuelle**. Pas sur la cible. Le filet doit d'abord passer au vert sur l'ancien monde ; il passera ensuite sur le nouveau, ou il dira précisément ce qui a changé.

Ces tests décrivent les défauts aussi. C'est inconfortable à écrire, et c'est exactement le but.

## Règle 3 : par morceaux

On migre un périmètre à la fois, derrière une frontière claire, en gardant l'ancien chemin disponible jusqu'à ce que le nouveau ait fait ses preuves en production. Le grand soir où tout bascule d'un coup n'existe que dans les plannings.

## Règle 4 : comparer, pas supposer

Quand c'est possible, l'ancien et le nouveau tournent en parallèle sur le même trafic, et on compare les sorties. Un écart n'est pas forcément une erreur, mais il est toujours une question.

## Ce que je ne fais plus

Mélanger migration et refonte. « Tant qu'on y est » est la phrase la plus coûteuse que je connaisse en ingénierie.
