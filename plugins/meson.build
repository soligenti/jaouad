plugin_include_dirs = include_directories('../include')

cairo_dep = dependency('cairo', required : false, version : '>=1.0')
dbus_1_dep = dependency('dbus-1', required : false)
#fuse_dep = dependency('fuse', required : false)
glib_2_dep = dependency('glib-2.0', required : false)
librsvg_2_dep = dependency('librsvg-2.0', required : false, version : '>=2.14.0')
glu_dep = dependency('glu', required : false)
libpng_dep = dependency('libpng', required : false)

plugin_dep_list = [libxml_2_dep, libstartup_notification_1_dep]

plugins = []

if cairo_dep.found()
    shared_module('annotate', 'annotate.c',
                   install : true,
                   install_dir : lib_dir,
                   dependencies : [cairo_dep,
                                   plugin_dep_list],
                   include_directories : plugin_include_dirs)
    plugins += 'annotate'
else
    message('cairo not found, disabling annotate plugin')
endif

if glu_dep.found()
    shared_module('blur', 'blur.c',
                   install : true,
                   install_dir : lib_dir,
                   dependencies : [glu_dep,
                                   plugin_dep_list],
                   include_directories : plugin_include_dirs,
                   link_with : libdecor)
    plugins += 'blur'
else
    message('glu not found, disabling blur plugin')
endif

shared_module('clone', 'clone.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'clone'

shared_module('commands', 'commands.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'commands'

shared_module('cube', 'cube.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'cube'

if dbus_1_dep.found()
    shared_module('dbus', 'dbus.c',
                   install : true,
                   install_dir : lib_dir,
                   dependencies : [dbus_1_dep,
                                   plugin_dep_list],
                   include_directories : plugin_include_dirs)
    plugins += 'dbus'
else
    message('dbus-1 not found, disabling dbus plugin')
endif

shared_module('decoration', 'decoration.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs,
               link_with : libdecor)
plugins += 'decoration'

shared_module('fade', 'fade.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'fade'

#if fuse_dep.found()
#shared_module('fuse', 'fuse.c',
#               install : true,
#               install_dir : lib_dir,
#               dependencies : [fuse_dep,
#                               plugin_dep_list],
#               include_directories : plugin_include_dirs)
#plugins += 'fuse'
#else
#    message('fuse not found, disabling fuse plugin')
#endif

if glib_2_dep.found()
    shared_module('glib', 'glib.c',
                   install : true,
                   install_dir : lib_dir,
                   dependencies : [glib_2_dep,
                                   plugin_dep_list],
                   include_directories : plugin_include_dirs)
    plugins += 'glib'
else
    message('glib-2.0 not found, disabling glib plugin')
endif

shared_module('ini', 'ini.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'ini'

shared_module('inotify', 'inotify.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'inotify'

shared_module('matecompat', 'matecompat.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'matecompat'

shared_module('minimize', 'minimize.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'minimize'

shared_module('move', 'move.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'move'

shared_module('obs', 'obs.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'obs'

shared_module('place', 'place.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'place'

if libpng_dep.found()
    shared_module('png', 'png.c',
                   install : true,
                   install_dir : lib_dir,
                   dependencies : [libpng_dep, plugin_dep_list],
                   include_directories : plugin_include_dirs)
    plugins += 'png'
else
    message('libpng not found, disabling png plugin')
endif

shared_module('regex', 'regex.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'regex'

shared_module('rotate', 'rotate.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'rotate'

shared_module('resize', 'resize.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'resize'

shared_module('scale', 'scale.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'scale'

shared_module('screenshot', 'screenshot.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'screenshot'

if cairo_dep.found() and librsvg_2_dep.found()
    shared_module('svg', 'svg.c',
                   install : true,
                   install_dir : lib_dir,
                   dependencies : [cairo_dep,
                                   librsvg_2_dep,
                                   plugin_dep_list],
                   include_directories : plugin_include_dirs)
    plugins += 'svg'
else
    if not cairo_dep.found()
        message('cairo not found, disabling svg plugin')
    elif not librsvg_2_dep.found()
        message('librsvg-2.0 not found, disabling svg plugin')
    endif
endif

shared_module('switcher', 'switcher.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'switcher'

if cairo_dep.found()
    shared_module('wall', 'wall.c',
                   install : true,
                   install_dir : lib_dir,
                   dependencies : [cairo_dep,
                                   plugin_dep_list],
                   include_directories : plugin_include_dirs)
    plugins += 'wall'
else
    message('cairo not found, disabling wall plugin')
endif

shared_module('water', 'water.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'water'

shared_module('wobbly', 'wobbly.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'wobbly'

shared_module('zoom', 'zoom.c',
               install : true,
               install_dir : lib_dir,
               dependencies : [plugin_dep_list],
               include_directories : plugin_include_dirs)
plugins += 'zoom'

foreach p : plugins
    custom_target(p + '.xml',
                   input : join_paths('../metadata/', p + '.xml.in'),
                   output : p + '.xml',
                   command : [intltool_merge, '-x', po_dir, '@INPUT@', '@OUTPUT@'],
                   install : true,
                   install_dir : share_dir)
endforeach

install_data('compiz-decorator', install_dir : join_paths(get_option('prefix'), 'bin'))

# fails because msgfmt can't find 'its' files
#i18n = import('i18n')
#i18n.merge_file(input : 'metadata/annotate.xml.in',
#                output : 'annotate.xml',
#                po_dir : 'po',
#                data_dirs: meson.source_root(),
#                install : true,
#                install_dir : get_option('prefix') + '/share/compiz')
