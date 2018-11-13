macos_preprocessor_flags = [
  '-DSFML_OS_MACOSX=1', 
  '-DSFML_BUILD_FRAMEWORKS=1', 
]

unix_srcs = glob([
  'src/SFML/**/Unix/**/*.cpp',
])

linux_srcs = glob([
  'src/SFML/**/Unix/**/*.cpp',
  'src/SFML/**/Egl*.cpp',
  'src/SFML/**/EGL*.cpp',
])

macos_srcs = glob([
  'src/SFML/System/Unix/**/*.cpp',
  'src/SFML/**/OSX/**/*.cpp',
  'src/SFML/**/OSX/**/*.mm',
  'src/SFML/**/OSX/**/*.m',
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

platform_srcs = unix_srcs + linux_srcs + macos_srcs + windows_srcs + freebsd_srcs + android_srcs

linux_exported_linker_flags = [
  '-lX11',
  '-lGL',
  '-lpthread',
]

macos_deps = [
  'buckaroo.github.buckaroo-pm.host-application-services//:application-services', 
  'buckaroo.github.buckaroo-pm.host-core-foundation//:core-foundation', 
  'buckaroo.github.buckaroo-pm.host-core-services//:core-services', 
  'buckaroo.github.buckaroo-pm.host-core-graphics//:core-graphics', 
  'buckaroo.github.buckaroo-pm.host-io-kit//:io-kit', 
  'buckaroo.github.buckaroo-pm.host-app-kit//:app-kit', 
  'buckaroo.github.buckaroo-pm.host-carbon//:carbon', 
  'buckaroo.github.buckaroo-pm.host-opengl//:opengl', 
  'buckaroo.github.buckaroo-pm.host-cocoa//:cocoa', 
  '//extlibs/libs-osx/Frameworks:openal', 
]

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
  exported_platform_linker_flags = [
    ('default', linux_exported_linker_flags),
    ('linux.*', linux_exported_linker_flags),
  ],
  deps = [
    'buckaroo.github.buckaroo-pm.xiph-ogg//:ogg', 
    'buckaroo.github.buckaroo-pm.xiph-flac//:flac', 
    'buckaroo.github.buckaroo-pm.xiph-vorbis//:vorbis', 
    'buckaroo.github.buckaroo-pm.luadist-freetype//:freetype', 
    '//extlibs/headers/AL:al', 
    '//extlibs/headers/stb_image:stb_image', 
  ], 
  platform_deps = [
    ('macos.*', macos_deps), 
  ], 
  visibility = [
    'PUBLIC',
  ],
)
