####################################
Mon début avec MIPS
####################################

:date: 2019-02-10 16:52
:modified: 2019-02-10 16:52
:tags: os3
:category: uqam
:slug: mips-premier-contact
:authors: Yu-Chiang Hsu
:summary: ma première installation de mips

But initial
##############################
Mon but initial est d'utiliser la ligne de commande pour compiler et exécuter des programmes mips. En effet, il n'est pas très facile d'utiliser vim par l'insterface graphique du gui Mars_.

.. _Mars: http://courses.missouristate.edu/KenVollmar/mars/

Le plan est simple:

1. Installer mips sur ubuntu (s'appelle SIPS)
2. Trouver un tutoriel sur youtube
3. Exécuter le programme simultanément sur les deux platforms SIPS (ligne de commande) et Mars (gui)


Installation sur ubuntu
#######################

basé sur ce site: https://askubuntu.com/questions/367168/getting-spim-mips-compiler-on-ubuntu-12-04

pour installer sur ubuntu il suffit de:
sudo apt-get install spim


Rouler premier script
#####################

basé sur cette video: https://www.youtube.com/watch?v=-BUJXKsqcoI
titre vidéo: Spim run script demo,
par: Gego/XAREN

run.sh::
  #!/bin/bash

  ###
  #Just run a .asm file in spim with the correct settings.
  ###


  spim -delayed_branches -delayed_loads -quiet -file $1


Pour donner les permission d'exécution
chmod u+x run.sh

hello.asm::
  
  .data
    hw: .asciiz "Hello World!\n"

  .text
  main:
    la $a0,hw
    li $v0,4
    syscall

    li $v0, 10
    syscall

Pour rouler hello.asm:
./run.sh hello.asm

Fichier qui lit et recrache ce qui a été lu.
read.asm::

  #begin code
    .data
  
  i_str_input:
  .word 4

  o_str_ask_input:
    .asciiz: "Enter a string: "

  o_str_tell_input:
    .asciiz: "The input was: "

  o_str_newline:
    .asciiz: "\n"

    .text
  main:
    la $a0, o_str_ask_input
    li $v0, 4


Merci Gego/XAREN!


J'ai rencontré comme erreur avec Syntastic, mon validateur de syntaxe. Il se met en folie. Afin de cacher les messages d'erreur aggressives j'ai décidé de désactiver la validation de syntaxe jusqu'à ce que j'en ai besoin.

source: https://stackoverflow.com/questions/20030603/vim-syntastic-how-to-disable-the-checker

dans vimrc::
  let g:syntastic_mode_map = { 'mode': 'passive', 'active_filetypes':   [],'passive_filetypes': []  }
  noremap <C-w>e :SyntasticCheck<CR>
  noremap <C-w>f :SyntasticToggleMode<CR>

J'ai aussi découvert que Alt+Backspace agit comme esc, ce sera utile pour mes laboratoires ou je ne peux pas mettre capslock à <esc>.
