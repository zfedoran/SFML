load('//:subdir_glob.bzl', 'subdir_glob')
load('//:buckaroo_macros.bzl', 'buckaroo_deps', 'buckaroo_deps_from_package')

macos_preprocessor_flags = [
  '-DSFML_OS_MACOSX=1',
  '-DSFML_BUILD_FRAMEWORKS=1',
]

linux_preprocessor_flags = [
  '-DSFML_OS_LINUX=1',
]

unix_srcs = glob([
  'src/SFML/**/Unix/**/*.cpp',
])

egl_srcs = glob([
  'src/SFML/**/Egl*.cpp',
  'src/SFML/**/Egl*.cpp',
  'src/SFML/**/EGL*.cpp',
])

linux_srcs = glob([
  'src/SFML/**/Unix/**/*.cpp',
])

macos_srcs = glob([
  'src/SFML/System/Unix/**/*.cpp',
  'src/SFML/**/OSX/**/*.cpp',
  'src/SFML/**/OSX/**/*.mm',
  'src/SFML/**/OSX/**/*.m',
])

openbsd_srcs = glob([
  'src/SFML/**/OpenBSD/**/*.cpp',
])

freebsd_srcs = glob([
  'src/SFML/**/FreeBSD/**/*.cpp',
])

windows_srcs = glob([
  'src/SFML/Main/MainWin32.cpp',
  'src/SFML/**/Win32/**/*.cpp',
])

android_srcs = glob([
  'src/SFML/Main/MainAndroid.cpp',
  'src/SFML/Main/SFMLActivity.cpp',
  'src/SFML/**/Android/**/*.cpp',
])

platform_srcs = unix_srcs + linux_srcs + macos_srcs + \
  windows_srcs + freebsd_srcs + android_srcs + \
  openbsd_srcs + egl_srcs

macos_deps = \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-core-foundation') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-core-services') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-core-graphics') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-io-kit') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-app-kit') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-carbon') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-cocoa') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-opengl') + \
  [ '//extlibs/libs-osx/Frameworks:openal' ]

linux_deps = \
  buckaroo_deps_from_package('github.com/buckaroo-pm/host-pthread') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/pkg-config-x11') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/pkg-config-xrandr') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/pkg-config-udev') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/pkg-config-gl') + \
  buckaroo_deps_from_package('github.com/buckaroo-pm/pkg-config-openal')

cxx_library(
  name = 'sfml',
  header_namespace = 'SFML',
  exported_headers = subdir_glob([
    ('include/SFML', '**/*.hpp'),
    ('include/SFML', '**/*.h'),
    ('include/SFML', '**/*.inl'),
  ]),
  headers = subdir_glob([
    ('src/SFML', '**/*.hpp'),
    ('src/SFML', '**/*.h'),
  ]),
  platform_preprocessor_flags = [
    ('macos.*', macos_preprocessor_flags),
    ('linux.*', linux_preprocessor_flags),
  ],
  srcs = glob([
    'src/SFML/**/*.cpp',
  ], exclude = platform_srcs),
  platform_srcs = [
    ('default', unix_srcs),
    ('linux.*', linux_srcs),
    ('macos.*', macos_srcs),
    ('windows.*', windows_srcs),
    ('android.*', android_srcs),
  ],
  exported_preprocessor_flags = [
    '-DHAVE_PROTOTYPES=1',
  ],
  deps =
    buckaroo_deps_from_package('github.com/buckaroo-pm/xiph-ogg') +
    buckaroo_deps_from_package('github.com/buckaroo-pm/xiph-flac') +
    buckaroo_deps_from_package('github.com/buckaroo-pm/xiph-vorbis') +
    buckaroo_deps_from_package('github.com/buckaroo-pm/freetype2') + [
    '//extlibs/headers/stb_image:stb_image',
  ],
  platform_deps = [
    ('macos.*', macos_deps),
    ('linux.*', linux_deps),
  ],
  licenses = [
    'license.md',
  ],
  visibility = [
    'PUBLIC',
  ],
)
