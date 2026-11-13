# 04. Relire le code

Inspiré de : les *Engineering Practices* publiques de Google, les Conventional Comments.

## À quoi sert une revue

D'abord à partager la connaissance : après une revue, deux personnes comprennent le changement au lieu d'une. Ensuite à attraper ce que l'auteur ne pouvait pas voir. En dernier seulement, à faire respecter des conventions, et un outil de formatage s'en charge mieux que nous.

## Le critère d'approbation

Google le formule bien : on approuve dès que le changement **améliore l'état général du code**, même s'il n'est pas parfait. Chercher la perfection bloque les équipes et décourage les petites demandes de fusion, celles qu'on veut justement encourager.

## Ce que le relecteur regarde, dans cet ordre

1. Le changement fait-il ce qu'il prétend faire ? Le relecteur lit la demande d'origine avant le code.
2. Que se passe-t-il quand ça échoue ? Timeout, doublon, valeur absente, appel rejoué.
3. Les tests prouvent-ils quelque chose, ou se contentent-ils d'exécuter des lignes ?
4. Quelqu'un comprendra-t-il ce code dans un an sans l'auteur à côté ?
5. Le reste.

## Dire ce qu'on veut dire

Chaque commentaire annonce sa nature :

- **bloquant** : la fusion attend ;
- **question** : je ne comprends pas, explique-moi ;
- **suggestion** : à toi de voir ;
- **détail** : sans importance, à ignorer si tu es pressé.

Un commentaire sans étiquette est lu comme bloquant. C'est rarement l'intention, et c'est ainsi que naissent les revues qui durent une semaine.

## Les délais

Une demande de fusion attend une première réponse en moins d'une demi-journée ouvrée. Relire passe avant commencer autre chose : un travail fini et bloqué vaut moins qu'un travail jamais commencé.
