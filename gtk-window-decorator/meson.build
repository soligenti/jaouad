gtk_w_d_include_dirs = include_directories('../include')

dbus_glib_dep = dependency('dbus-glib-1', required : false)

if use_gtk == 'gtk-3'
    wnck_dep = dependency('libwnck-3.0', required : false)
elif use_gtk == 'gtk-2'
    wnck_dep = dependency('libwnck-1.0', required : false)
endif

if dbus_glib_dep.found() and wnck_dep.found()
    extra_deps = []
    gtk_w_d_c_args = []

    if use_marco
        extra_deps += marco_dep
        gtk_w_d_c_args += '-DUSE_MARCO=1'
    endif
    if use_gsettings
        extra_deps += glib_2_dep
        extra_deps += gio_2_dep
        gtk_w_d_c_args += '-DUSE_GSETTINGS=1'
    endif

    executable('gtk-window-decorator', 'gtk-window-decorator.c',
                install : true,
                dependencies : [m_dep, xrender_dep, dbus_glib_dep, gtk_dep, wnck_dep, extra_deps],
                include_directories : gtk_w_d_include_dirs,
                c_args : gtk_w_d_c_args,
                link_with : libdecor)
endif

