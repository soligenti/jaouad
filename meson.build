project('compiz', 'c', version : '0.8.15')

gettext_package = meson.project_name()

lib_dir = join_paths(get_option('prefix'), get_option('libdir'), 'compiz')
share_dir = join_paths(get_option('prefix'), 'share', 'compiz')
po_dir = join_paths(meson.source_root(), 'po')

add_global_arguments('-DHAVE_CONFIG_H=1', language : 'c')
add_global_arguments('-DPLUGINDIR="' + lib_dir + '"', language : 'c')
add_global_arguments('-DIMAGEDIR="' + share_dir + '"', language : 'c')
add_global_arguments('-DMETADATADIR="' + share_dir + '"', language : 'c')
add_global_arguments('-DLOCALEDIR="' + share_dir + '"', language : 'c')
add_global_arguments('-DGETTEXT_PACKAGE="' + gettext_package + '"', language: 'c')

cc = meson.get_compiler('c')

compiz_version = meson.project_version()

version_numbers = compiz_version.split('.')

compiz_version_major = version_numbers[0]
compiz_version_minor = version_numbers[1]
compiz_version_micro = version_numbers[2]

dependency('pkg-config', required : true)

intltool_merge = find_program('intltool-merge', required : true)

use_gtk = get_option('use_gtk')

if use_gtk == 'gtk-3'
	gtk_dep = dependency('gtk+-3.0', required : false)
	if gtk_dep.found()
        message('Using GTK 3')
    else
	    gtk_dep = dependency('gtk+-2.0', required : false)
	    if gtk_dep.found()
            message('Using GTK 2')
	        use_gtk = 'gtk-2'
	    else
            message('Could not find gtk 2 or 3. GTK disabled')
	        use_gtk = 'disabled'
	    endif
	endif
elif use_gtk == 'gtk-2'
	gtk_dep = dependency('gtk+-2.0', required : false)
	if gtk_dep.found()
        message('Using GTK 2')
    else
	    gtk_dep = dependency('gtk+-3.0', required : false)
	    if gtk_dep.found()
            message('Using GTK 3')
	        use_gtk = 'gtk-3'
	    else
            message('Could not find gtk 2 or 3. GTK disabled')
	        use_gtk = 'disabled'
	    endif
	endif
else
    message('GTK disabled')
	use_gtk = 'disabled'
endif

use_marco = get_option('use_marco')

if use_gtk == 'gtk-2'
    if use_marco
        marco_dep = dependency('libmarco-private', required : false)
        if marco_dep.found()
            message('Marco support enabled')
        else
            message('libmarco-private not found, disabling marco support')
            use_marco = false
        endif
    else
        message('Marco support disabled')
    endif
else
    use_marco = false
endif

use_gsettings = get_option('use_gsettings')
glib_2_dep = dependency('glib-2.0', version : '>=2.32', required : false)
gio_2_dep = dependency('gio-2.0', version : '>=2.25.0', required : false)

if use_gtk != 'disabled'
    if use_gsettings
		if not glib_2_dep.found() or not gio_2_dep.found()
            message('Could not find glib-2.0 or gio-2.0, disabling gsettings')
		    use_gsettings = false
		else
            message('Gsettings enabled')
		endif
    endif
endif

conf_data = configuration_data()
conf_data.set('project_name', meson.project_name())
conf_data.set('version', compiz_version)
conf_data.set('decor_interface_version', '20110504')

configure_file(input : 'config.h.meson',
  output : 'config.h',
  configuration : conf_data)

compiz_common_data = configuration_data()
compiz_common_data.set('version_major', compiz_version_major)
compiz_common_data.set('version_minor', compiz_version_minor)
compiz_common_data.set('version_micro', compiz_version_micro)

configure_file(input : join_paths('include', 'compiz-common.h.meson'),
  output : 'compiz-common.h',
  configuration : compiz_common_data)

run_command('cp', join_paths(meson.build_root(), 'compiz-common.h'), 'include')
run_command('cp', join_paths(meson.build_root(), 'config.h'), 'include')

compiz_include_dirs = include_directories('include')

compiz_deps = ['x11',
               'xcomposite',
               'xext',
               'xfixes',
               'xdamage',
               'xrandr',
               'xi',
               'xinerama',
               'xcursor',
               'ice',
               'sm',
               'libxml-2.0',
               'libstartup-notification-1.0 >= 0.7']

m_dep = cc.find_library('m', required : true)
dl_dep = cc.find_library('dl', required : true)
gl_dep = dependency('GL', required : true)
x11_dep = dependency('x11', required : true)
xcomposite_dep = dependency('xcomposite', required : true)
xext_dep = dependency('xext', required : true)
xfixes_dep = dependency('xfixes', required : true)
xdamage_dep = dependency('xdamage', required : true)
xrandr_dep = dependency('xrandr', required : true)
xrender_dep = dependency('xrender', required : true)
xi_dep = dependency('xi', required : true)
xinerama_dep = dependency('xinerama', required : true)
xcursor_dep = dependency('xcursor', required : true)
ice_dep = dependency('ice', required : true)
sm_dep = dependency('sm', required : true)
libxml_2_dep = dependency('libxml-2.0', required : true)
libstartup_notification_1_dep = dependency('libstartup-notification-1.0', version : '>=0.7', required : true)

compiz_dep_list = [m_dep, dl_dep, x11_dep, xcomposite_dep, xext_dep, xfixes_dep, xdamage_dep, xrandr_dep, xi_dep, xinerama_dep, xcursor_dep, ice_dep, sm_dep, libxml_2_dep, libstartup_notification_1_dep]

compiz_sources = files('src/main.c',
                       'src/privates.c',
                       'src/object.c',
                       'src/core.c',
                       'src/texture.c',
                       'src/display.c',
                       'src/screen.c',
                       'src/window.c',
                       'src/event.c',
                       'src/paint.c',
                       'src/option.c',
                       'src/plugin.c',
                       'src/session.c',
                       'src/fragment.c',
                       'src/matrix.c',
                       'src/cursor.c',
                       'src/match.c',
                       'src/metadata.c')

executable(meson.project_name(), compiz_sources,
                     install : true,
                     dependencies : compiz_dep_list,
                     include_directories : compiz_include_dirs,
                     link_args : ['-lGL', '-Wl,-export-dynamic'])

custom_target('core.xml',
               input : join_paths('metadata', 'core.xml.in.in'),
               output : 'core.xml',
               command : [intltool_merge, '-x', po_dir, '@INPUT@', '@OUTPUT@'],
               install : true,
               install_dir : share_dir)

subdir('libdecoration')
subdir('plugins')
subdir('include')
if use_gtk != 'disabled'
    subdir('gtk-window-decorator')
endif

pkg = import('pkgconfig')
cflags = ['-I/usr/include/libxml2', '-I/usr/include/startup-notification-1.0']

pkg.generate(name : 'compiz',
             extra_cflags : cflags,
             libraries : '',
             subdirs : 'compiz',
             version : compiz_version,
             requires : compiz_deps,
             description : 'OpenGL compositing manager')

pkg.generate(name : 'compiz-cube',
             extra_cflags : cflags,
             libraries : '',
             subdirs : 'compiz',
             version : compiz_version,
             requires : 'compiz',
             description : 'Cube plugin for compiz')

pkg.generate(name : 'compiz-scale',
             extra_cflags : cflags,
             libraries : '',
             subdirs : 'compiz',
             version : compiz_version,
             requires : 'compiz',
             description : 'Scale plugin for compiz')

pkg.generate(name : 'libdecoration',
             libraries : '-lXrender -lX11 -L${libdir} -ldecoration',
             subdirs : 'compiz',
             version : compiz_version,
             requires : 'xrender',
             description : 'Window decoration library')

