# Copyright (c) 2026 The Zephyr Contributors
# SPDX-License-Identifier: Apache-2.0

if(CONFIG_LIBCSUIT)
  set(LIBCSUIT_SRC ${CMAKE_CURRENT_SOURCE_DIR}/..)

  zephyr_library_named(modules_csuit)

  # Add include directories
  zephyr_library_include_directories(
    ${LIBCSUIT_SRC}/inc
    ${LIBCSUIT_SRC}/3rdparty/QCBOR/inc
    ${LIBCSUIT_SRC}/3rdparty/t_cose/inc
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src
    ${LIBCSUIT_SRC}/3rdparty/mbedtls/include
  )

  # Add QCBOR sources with float support disabled
  zephyr_library_sources(
    ${LIBCSUIT_SRC}/3rdparty/QCBOR/src/qcbor_encode.c
    ${LIBCSUIT_SRC}/3rdparty/QCBOR/src/qcbor_decode.c
    ${LIBCSUIT_SRC}/3rdparty/QCBOR/src/qcbor_err_to_str.c
    ${LIBCSUIT_SRC}/3rdparty/QCBOR/src/UsefulBuf.c
  )

  # Add t_cose sources
  zephyr_library_sources(
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_sign1_sign.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_parameters.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_sign1_verify.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_util.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_key.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_sign_sign.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_mac_compute.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_signature_sign_main.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_signature_sign_restart.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_signature_sign_eddsa.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_sign_verify.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_mac_validate.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_signature_verify_main.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_signature_verify_eddsa.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_encrypt_enc.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_encrypt_dec.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_qcbor_gap.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_recipient_enc_esdh.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_recipient_enc_keywrap.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_recipient_dec_esdh.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/src/t_cose_recipient_dec_keywrap.c
    ${LIBCSUIT_SRC}/3rdparty/t_cose/crypto_adapters/t_cose_psa_crypto.c
  )

  # Add libcsuit sources
  zephyr_library_sources(
    ${LIBCSUIT_SRC}/src/suit_common.c
    ${LIBCSUIT_SRC}/src/suit_digest.c
    ${LIBCSUIT_SRC}/src/suit_cose.c
    ${LIBCSUIT_SRC}/src/suit_manifest_print.c
    ${LIBCSUIT_SRC}/src/suit_manifest_encode.c
    ${LIBCSUIT_SRC}/src/suit_manifest_decode.c
    ${LIBCSUIT_SRC}/src/suit_manifest_process.c
    ${LIBCSUIT_SRC}/src/suit_manifest_callbacks.c
    ${LIBCSUIT_SRC}/src/suit_reporting_engine.c
    ${LIBCSUIT_SRC}/src/suit_report_print.c
  )

  zephyr_library_compile_definitions(
    LIBCSUIT_PSA_CRYPTO_C=1
    T_COSE_USE_PSA_CRYPTO=1
    USEFULBUF_DISABLE_ALL_FLOAT
    MBEDTLS_ALLOW_PRIVATE_ACCESS
  )
endif()
