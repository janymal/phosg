phosg_audio_lib = library(
    'phosg-audio',
    'Constants.cc',
    'File.cc',
    'Convert.cc',
    'Capture.cc',
    'Sound.cc',
    'Stream.cc',
    'FourierTransform.cc',
    dependencies: [openal_dep, phosg_dep],
    install: true,
)

install_headers(
    'Capture.hh',
    'Constants.hh',
    'Convert.hh',
    'File.hh',
    'FourierTransform.hh',
    'Sound.hh',
    'Stream.hh',
    subdir: 'phosg-audio',
)


phosg_audio_dep = declare_dependency(
    dependencies: [openal_dep, phosg_dep],
    include_directories: root_inc,
    link_with: [phosg_audio_lib],
)

audiocat_exe = executable(
    'audiocat',
    'Audiocat.cc',
    dependencies: [phosg_audio_dep],
    install: true,
)
