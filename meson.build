project(
  'rendercheck',
  'c',
  version : '1.5',
  license : 'MIT AND GPL-2.0-or-later'
)
cc = meson.get_compiler('c')

if cc.has_header('err.h')
    add_project_arguments('-DHAVE_ERR_H', language: 'c')
endif

add_project_arguments('-D_GNU_SOURCE', language: 'c')

srcs = [
    'main.c',
    'ops.c',
    'tests.c',
    't_blend.c',
    't_bug7366.c',
    't_composite.c',
    't_dstcoords.c',
    't_fill.c',
    't_gradient.c',
    't_gtk_argb_xbgr.c',
    't_libreoffice_xrgb.c',
    't_repeat.c',
    't_shmblend.c',
    't_srccoords.c',
    't_tsrccoords.c',
    't_tsrccoords2.c',
    't_triangles.c',
]

version_config = configuration_data()
version_config.set_quoted('VERSION', meson.project_version())

configure_file(
    output: 'version.h',
    configuration: version_config,
)

executable(
    'rendercheck',
    srcs,
    dependencies: [
        dependency('xrender'),
        dependency('xext'),
        dependency('x11'),
        dependency('xproto', version: '>= 7.0.17'),
    ],
    install: true,
)

man_config = configuration_data()
man_config.set('version', meson.project_version())
rendercheck_man = configure_file(
    input: 'man/rendercheck.man',
    output: 'rendercheck.1',
    configuration: man_config,
    install: true,
    install_dir: join_paths(get_option('mandir'), 'man1'),
)
