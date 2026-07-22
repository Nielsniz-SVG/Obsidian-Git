==Enregistrement terminal==

*Accès sécurisé....
Veuillez entrer une commande*

ger.agent5

*Bonjour agent Gérard, veuillez entrer votre mot de passe...*

vxestunepourriture

*Mot de passe correct !
Veuillez entrer une commande...*

access p-r /5

*Accès en cours...
Demande d'authentification requise,
Veuillez re-entrer vos identifiants...*

ger.agent5 vxestunepourriture 

*Téléchargement du dossier....
Accès en cours...*
> [!FAIL]
> ERREUR 753: vx stopped this action
> Admin MSG: action dangereuse détécté stoppée !
> bug proofed not pour prouver que ce n'était pas dangereux.

bug proofed not 

*Désolé, il manque la raison.*

bug proofed not "Je voulais juste accéder au fichier p-r j'ai un niveau d'accréditation 5"

*Envoi du message à VX...
Réponse !*
> [! SUCCESS]
> Désolé agent Gérard, vous pouvez maintenant accéder au fichier p-r ! ;)

access -proofed p-r /5

*Téléchargement du dossier en cours... [DONE]*
> [!WARNING]
> Fichier p-r
> ## Paradoxe de Rupture
> 
> Le paradoxe de rupture est le moment ou toutes les dimensions sont détruites.
> Comme une dimension est crée dès que quelqu'un ou quelque chose pense à un univers, chaque univers crée d'autres dimension etc et quand le "créateur" de la dimension meurt, sa dimension disparaît. Voilà ce qu'est le paradoxe de rupture. Le moment où il ne reste plus que le point A.

dnwld p-r /5

*Téléchargement du fichier sur votre appareil... [DONE]*

msg drzed "C'est bon j'ai le fichier !" --wait-answer

*Waiting...*
> [!SUCCESS]
> Parle pas ici ! Parle dans un canal privé ! VX vois tout !! -drzed

msg prvt drzed --ntf

=================================
              Canal privé


ger.agent5:
C'est bon j'ai le fichier
p-r ! J'te l'envoi ?

                         drzed:
                        Ouais donne
                        le moi !

ger.agent5:
Ok !
/exit

=================================

snd p-r.aaxfile t drzed

*......
Envoyé !!*

logout

*Aurevoir agent Gérard !*

exit


