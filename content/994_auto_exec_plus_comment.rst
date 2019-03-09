####################################
Mips install partie 2
####################################

:date: 2019-03-08 21:08
:modified: 2019-03-08 21:08
:tags: os3
:category: uqam
:slug: mips-partie-2
:authors: Yu-Chiang Hsu
:summary: continuer à installer mips


But exécuter mips 1 touche
##############################

* :call ToMips()<br/>
  Appel manuel de :call ToMips() afin de faire coexister les raccourcis avec d'autre types de fichiers

* F7<br/>
  Raccourci d'exécution

* Ligne pour commentaire<br/>
  Vim utilise ; pour les commentaires des fichiers sous ".asm".
  Or, en mips # doit être utilisé.
  Afin de bénéficier de cette ligne vous devez utiliser le plugin tcomment
  Enlever la ligne call tcomment... si jamais vous n'avez pas le plugin nécessaire

Dans .vimrc
#######################

.vimrc::

  function MipsMainThenQuit()
    exec "w"
    exec "!./run.sh %"
  endfunction

  function ToMips()
    "bind f7 to mips execute main
    :imap <F7> <Esc>:call MipsMainThenQuit()<cr>
    :nmap <F7> :call MipsMainThenQuit()<cr>
    "asm mips uses # as comment (use this line only if you have tcomment plugin)
    call tcomment#DefineType('asm', '# %s')
  endfunction

.. |br| raw:: html

  <br/>
