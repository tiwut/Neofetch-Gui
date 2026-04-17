project('neofetch-gui', 'cpp', version: '1.0.0')

gtk_dep = dependency('gtk4')
vte_dep = dependency('vte-2.91-gtk4')

executable('neofetch-gui',
           'main.cpp',
           dependencies: [gtk_dep, vte_dep],
           install: true)

install_data('org.tiwut.NeofetchGui.desktop', 
             install_dir: join_paths(get_option('datadir'), 'applications'))

install_data('org.tiwut.NeofetchGui.metainfo.xml', 
             install_dir: join_paths(get_option('datadir'), 'metainfo'))

install_data('org.tiwut.NeofetchGui.png', 
            install_dir: join_paths(get_option('datadir'), 'icons/hicolor/128x128/apps'))
