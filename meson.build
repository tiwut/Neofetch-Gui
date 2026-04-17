project('neofetch-gui', 'cpp', version: '1.0.0')

gtk_dep = dependency('gtk4')
vte_dep = dependency('vte-2.91-gtk4')

executable('neofetch-gui',
           'main.cpp',
           dependencies: [gtk_dep, vte_dep],
           install: true)
