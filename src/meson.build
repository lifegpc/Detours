cc = meson.get_compiler('cpp')
MSVC = cc.get_id() == 'msvc'
FLAGS = []
if MSVC
    FLAGS += ['/WX', '/we4777', '/we4800', '/Gy']
endif

if get_option('detours_source_browsing')
    if MSVC
        FLAGS += ['/FR']
    endif
else
    FLAGS += ['-DWIN32_LEAN_AND_MEAN', '-D_WIN32_WINNT=0x501']
endif

arch = host_machine.cpu_family()
if MSVC
    if arch == 'ia64'
        FLAGS += ['/wd4163']
    endif
    if get_option('detours_win_7')
        FLAGS += ['-D_USING_V110_SDK71_']
    endif
endif

sources = files([
    'detours.cpp',
    'modules.cpp',
    'disasm.cpp',
    'image.cpp',
    'creatwth.cpp',
    'disolx86.cpp',
    'disolx64.cpp',
    'disolia64.cpp',
    'disolarm.cpp',
    'disolarm64.cpp',
])

detours = static_library('detours', sources, cpp_args: FLAGS, pic: true, install: not meson.is_subproject())
detours_dep = declare_dependency(include_directories: include_directories('.'), link_with: detours)

if not meson.is_subproject()
    install_headers('detours.h', 'detver.h')
endif