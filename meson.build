project('mcuboot', 'c', subproject_dir: 'ext') 

mcuboot_dir = 'boot/bootutil'
mcuboot_src_dir = mcuboot_dir / 'src'
mcuboot_inc_dir = mcuboot_dir / 'include'

mcuboot_sources = []

mcuboot_sources += files(
  mcuboot_src_dir / 'boot_record.c',
  mcuboot_src_dir / 'bootutil_misc.c',
  mcuboot_src_dir / 'bootutil_public.c',
  mcuboot_src_dir / 'caps.c',
  mcuboot_src_dir / 'encrypted.c',
  mcuboot_src_dir / 'fault_injection_hardening.c',
  mcuboot_src_dir / 'fault_injection_hardening_delay_rng_mbedtls.c',  # this probably isn't applicable
  mcuboot_src_dir / 'image_ecdsa.c',
  mcuboot_src_dir / 'image_ed25519.c',
  mcuboot_src_dir / 'image_rsa.c',
  mcuboot_src_dir / 'image_validate.c',
  mcuboot_src_dir / 'loader.c',
  mcuboot_src_dir / 'swap_misc.c',
  mcuboot_src_dir / 'swap_move.c',
  mcuboot_src_dir / 'swap_scratch.c',
  mcuboot_src_dir / 'tlv.c',
  )


cmake = import('cmake')

mbedtls_options = cmake.subproject_options()
mbedtls_options.add_cmake_defines({'ENABLE_PROGRAMS': false})
mbedtls_options.add_cmake_defines({'ENABLE_TESTING': false})

mbedtls_subproject = cmake.subproject('mbedtls', options: mbedtls_options)
mbedtls = mbedtls_subproject.dependency('mbedtls')
mbedx509 = mbedtls_subproject.dependency('mbedx509')
mbedcrypto = mbedtls_subproject.dependency('mbedcrypto')

mcuboot_dep = declare_dependency(
  sources: [mcuboot_sources], 
  include_directories: [mcuboot_inc_dir, mcuboot_src_dir], 
  dependencies: [mbedtls, mbedx509, mbedcrypto])
