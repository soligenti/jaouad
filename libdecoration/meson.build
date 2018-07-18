libdecor_include_dirs = include_directories('../include')

xrender_dep = dependency('xrender', required : true)

libdecor = shared_library('decor', 'decoration.c',
                install : true,
                version : '0.0.0',
                dependencies : [m_dep, xrender_dep],
                include_directories : libdecor_include_dirs)
