enable_testing()

foreach(test IN ITEMS
    test_base64
    test_crypto
    test_group_session
    test_list
    test_megolm
    test_message
    test_olm
    test_olm_decrypt
    test_olm_sha256
    test_olm_signature
    test_olm_using_malloc
    test_ratchet
    test_session
    test_pk
    )
add_executable(${test} ${test}.cpp)
target_include_directories(${test} PRIVATE include)
target_link_libraries(${test} Olm::Olm)
endforeach(test)

add_test(Base64 test_base64)
add_test(Crypto test_crypto)
add_test(GroupSession test_group_session)
add_test(List test_list)
add_test(Megolm test_megolm)
add_test(Message test_message)
add_test(Olm test_olm)
add_test(OlmDecrypt test_olm_decrypt)
add_test(OlmSha256 test_olm_sha256)
add_test(OlmSignature test_olm_signature)
add_test(OlmUsingMalloc test_olm_using_malloc)
add_test(Ratchet test_ratchet)
add_test(Session test_session)
add_test(PublicKey test_session)
