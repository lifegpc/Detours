cc = meson.get_compiler('cpp')
deps = [
    get_variable('detours_dep'),
    cc.find_library('kernel32'),
    cc.find_library('rpcrt4')
]
FLAGS = []
MSVC = cc.get_id() == 'msvc'
if MSVC
    FLAGS += ['/EHsc', '-DCATCH_CONFIG_NO_WINDOWS_SEH']
endif

sources = files([
    'main.cpp',
    'test_module_api.cpp',
    'test_image_api.cpp',
    'corruptor.cpp',
    'process_helpers.cpp',
    'payload.cpp'
])
unittests = executable('unittests', sources, cpp_args: FLAGS, dependencies: deps, install: false)
test('unittests', unittests)
