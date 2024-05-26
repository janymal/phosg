project(
    'phosg',
    'cpp',
    default_options: [
        'default_library=static',
        'cpp_std=c++20',
        'werror=true',
    ],
)

cpp = meson.get_compiler('cpp')
openal_dep = dependency('OpenAL')

if cpp.get_argument_syntax() == 'gcc'
    add_project_arguments(
        cpp.get_supported_arguments(
            [
                '-Wno-strict-aliasing',
                '-Wno-unused-result',
                '-Wno-overflow',
            ],
        ),
        language: 'cpp',
    )
elif cpp.get_argument_syntax() == 'msvc'
    add_project_arguments(
        cpp.get_supported_arguments(
            ['/wd4458'],
        ),
        language: 'cpp',
    )
endif

root_inc = include_directories('.')
# phosg_audio_inc = include_directories('phosg-audio')

subdir('phosg')
subdir('phosg-audio')
