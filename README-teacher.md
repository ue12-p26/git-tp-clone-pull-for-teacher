# pour les profs

## mise en place

* trouvez votre numéro de groupe - disons ici par exemple: `groupe6`

* en vous basant sur ce script bash, clonez le repo de référence et recréez en une copie pour votre groupe; celui-ci va s'appeler par exemple  
<https://github.com/ue12-p26/git-tp-clone-pull-groupe6>  


  ```
  GRP=6
  cd /tmp
  git clone git@github.com:ue12-p26/git-tp-clone-pull-for-teacher.git git-tp-clone-pull-groupe${GRP}
  cd git-tp-clone-pull-groupe${GRP}
  # important: débarrassez-vous du remote `origin`
  git remote remove origin
  
  gh repo create --public ue12-p26/git-tp-clone-pull-groupe${GRP}

  git remote add origin git@github.com:ue12-p26/git-tp-clone-pull-groupe${GRP}.git
  git branch -M main
  git push -u origin main
  ```

* ensuite dans le repo il y a un petit script qui s'appelle `publish.sh`
  pour que le prof puisse facilement faire avancer le repo

  le TP est censé démarrer à l'étape 0, donc vous faites **avant** que les élèves ne clonent:

  ```bash
  ./publish.sh 0
  # ou bien, c'est pareil
  ./publish.sh step0
  ```

* à ce stade vous pouvez donner l'URL aux élèves pour qu'ils clonent
  ils regardent le README qui leur dit quoi faire

*  quand tout le monde est en phase, le prof publie les étapes au fur et à mesure
   en faisant

   ```
   ./publish.sh 1
   # etc..
   ```

  et à chaque étape le README est augmenté pour passer à la phase suivante

## synopsis

le README contient les instructions pour passer d'une étape à l'autre, mais voici un résumé

* `step0`: l'enseignant expose un repo
  * les élèves le clonent

* `step1`: l'enseignant publie une modification
  * les élèves tirent - **sans souci** car pas de modification locale

* `step2`: les élèves modifient un truc localement (`file1`)
  * l'enseignant publie une mise à jour dans un **nouveau** fichier (`file2`)
  * les élèves tirent - **sans souci**

* `step3`: l'enseignant publie une mise à jour dans `file1` mais à un autre endroit que les élèves
  * les élèves essaient de tirer => **boom**
  * les élèves **committent**
  * puis ils tirent => **merge successful**

* `step4`: l'enseignant publie un changement sur la ligne 6 de `file1`
  * l'élève fait un changement sur **cette même ligne**
  * il essaie de tirer : **boom**
  * il committe
  * il tire: CONFLIT
  * montrer l'état du fichier (les deux versions)
  * montrer l'état du repo (unfinished merge)
  * résoudre le confilt manuellement
  * finir le merge

## historique

dans une version plus ancienne, le repo de référence était privé,
mais ça ne semble pas utile en fait
