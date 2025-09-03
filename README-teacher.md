# pour les profs

## mise en place

* trouvez votre numéro de groupe - disons ici par exemple: `groupe2`

* clonez le repo de référence

  ```
  git clone git@github.com:ue12-p25/git-tp-clone-pull-for-teacher.git groupe2
  cd groupe2
  ```

* **IMPORTANT** débarrassez-vous du remote `origin`

  ```bash
  git remote remove origin
  ```

  car le script va publier avec `git push --force` **dans votre repo de groupe**, et il ne faut pas que ça se mélange avec le repo de référence

* créez sur github un repo public qui s'appelle genre  
  <https://github.com/ue12-p25/git-tp-clone-pull-groupe2>  
  si vous pratiquez github sur la ligne de commande, ça donne

  ```bash
  gh repo create --public ue12-p25/git-tp-clone-pull-groupe2
  ```

* et pour le remplir:

  ```bash
  git remote add origin git@github.com:ue12-p25/git-tp-clone-pull-groupe2.git
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
