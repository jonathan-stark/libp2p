cmake_minimum_required(VERSION 2.6)

if( NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/c-ipfs/.git" )
    message( SEND_ERROR "The git submodules are not available. Please run
    git submodule update --init --recursive"
    )
endif()

add_library(lmdb
    lmdb/libraries/liblmdb/mdb.c
    lmdb/libraries/liblmdb/mdb_copy.c
    lmdb/libraries/liblmdb/mdb_dump.c
    lmdb/libraries/liblmdb/mdb_load.c
    lmdb/libraries/liblmdb/mdb_stat.c
    lmdb/libraries/liblmdb/midl.c
#lmdb/libraries/liblmdb/mtest.c
#lmdb/libraries/liblmdb/mtest2.c
#lmdb/libraries/liblmdb/mtest3.c
#lmdb/libraries/liblmdb/mtest4.c
#lmdb/libraries/liblmdb/mtest5.c
#lmdb/libraries/liblmdb/mtest6.c
)

add_library(c-protobuf
#    c-protobuf/main.c
    c-protobuf/protobuf.c
    c-protobuf/protobuf.h
    c-protobuf/varint.c
    c-protobuf/varint.h
)

add_library(c-multihash
    c-multihash/include/mh/errors.h
    c-multihash/include/mh/generic.h
    c-multihash/include/mh/hashes.h
    c-multihash/include/mh/multihash.h
    c-multihash/src/errors.c
    c-multihash/src/hashes.c
    c-multihash/src/multihash.c
)

add_library(c-multiaddr
    c-multiaddr/base58.c
    c-multiaddr/multiaddr.c
    c-multiaddr/protocols.c
    c-multiaddr/protoutils.c
    c-multiaddr/test_multiaddr.h
    c-multiaddr/testing.c
    c-multiaddr/varhexutils.c
    c-multiaddr/varint.c
)

target_link_libraries(c-protobuf
    c-multihash
)

target_include_directories(c-multihash PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/c-multihash/include/
)

target_include_directories(c-multiaddr PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/c-multiaddr/include/
)


add_library(c-libp2p
    c-libp2p/conn/connection.c		
    c-libp2p/conn/session.c			
    c-libp2p/conn/transport_dialer.c
    c-libp2p/conn/dialer.c			
    c-libp2p/conn/tcp_transport_dialer.c

    c-libp2p/crypto/aes.c
    c-libp2p/crypto/ephemeral.c
    c-libp2p/crypto/key.c
    c-libp2p/crypto/peerutils.c
    c-libp2p/crypto/rsa.c
    c-libp2p/crypto/sha1.c
    c-libp2p/crypto/sha256.c
    c-libp2p/crypto/sha512.c

    c-libp2p/crypto/encoding/base16.c
    c-libp2p/crypto/encoding/base32.c
    c-libp2p/crypto/encoding/base58.c
    c-libp2p/crypto/encoding/base64.c
    c-libp2p/crypto/encoding/x509.c

    c-libp2p/db/datastore.c
    c-libp2p/db/filestore.c

    c-libp2p/thirdparty/mbedtls/aes.c
    c-libp2p/thirdparty/mbedtls/aesni.c
    c-libp2p/thirdparty/mbedtls/arc4.c
    c-libp2p/thirdparty/mbedtls/asn1parse.c
    c-libp2p/thirdparty/mbedtls/asn1write.c
    c-libp2p/thirdparty/mbedtls/base64.c
    c-libp2p/thirdparty/mbedtls/bignum.c
    c-libp2p/thirdparty/mbedtls/blowfish.c
    c-libp2p/thirdparty/mbedtls/camellia.c
    c-libp2p/thirdparty/mbedtls/ccm.c
    c-libp2p/thirdparty/mbedtls/certs.c
    c-libp2p/thirdparty/mbedtls/cipher.c
    c-libp2p/thirdparty/mbedtls/cipher_wrap.c
    c-libp2p/thirdparty/mbedtls/cmac.c
    c-libp2p/thirdparty/mbedtls/ctr_drbg.c
    c-libp2p/thirdparty/mbedtls/debug.c
    c-libp2p/thirdparty/mbedtls/des.c
    c-libp2p/thirdparty/mbedtls/dhm.c
    c-libp2p/thirdparty/mbedtls/ecdh.c
    c-libp2p/thirdparty/mbedtls/ecdsa.c
    c-libp2p/thirdparty/mbedtls/ecjpake.c
    c-libp2p/thirdparty/mbedtls/ecp.c
    c-libp2p/thirdparty/mbedtls/ecp_curves.c
    c-libp2p/thirdparty/mbedtls/entropy.c
    c-libp2p/thirdparty/mbedtls/entropy_poll.c
    c-libp2p/thirdparty/mbedtls/error.c
    c-libp2p/thirdparty/mbedtls/gcm.c
    c-libp2p/thirdparty/mbedtls/havege.c
    c-libp2p/thirdparty/mbedtls/hmac_drbg.c
    c-libp2p/thirdparty/mbedtls/md.c
    c-libp2p/thirdparty/mbedtls/md2.c
    c-libp2p/thirdparty/mbedtls/md4.c
    c-libp2p/thirdparty/mbedtls/md5.c
    c-libp2p/thirdparty/mbedtls/md_wrap.c
    c-libp2p/thirdparty/mbedtls/memory_buffer_alloc.c
    c-libp2p/thirdparty/mbedtls/net_sockets.c
    c-libp2p/thirdparty/mbedtls/oid.c
    c-libp2p/thirdparty/mbedtls/padlock.c
    c-libp2p/thirdparty/mbedtls/pem.c
    c-libp2p/thirdparty/mbedtls/pk.c
    c-libp2p/thirdparty/mbedtls/pk_wrap.c
    c-libp2p/thirdparty/mbedtls/pkcs11.c
    c-libp2p/thirdparty/mbedtls/pkcs12.c
    c-libp2p/thirdparty/mbedtls/pkcs5.c
    c-libp2p/thirdparty/mbedtls/pkparse.c
    c-libp2p/thirdparty/mbedtls/pkwrite.c
    c-libp2p/thirdparty/mbedtls/platform.c
    c-libp2p/thirdparty/mbedtls/ripemd160.c
    c-libp2p/thirdparty/mbedtls/rsa.c
    c-libp2p/thirdparty/mbedtls/sha1.c
    c-libp2p/thirdparty/mbedtls/sha256.c
    c-libp2p/thirdparty/mbedtls/sha512.c
    c-libp2p/thirdparty/mbedtls/ssl_cache.c
    c-libp2p/thirdparty/mbedtls/ssl_ciphersuites.c
    c-libp2p/thirdparty/mbedtls/ssl_cli.c
    c-libp2p/thirdparty/mbedtls/ssl_cookie.c
    c-libp2p/thirdparty/mbedtls/ssl_srv.c
    c-libp2p/thirdparty/mbedtls/ssl_ticket.c
    c-libp2p/thirdparty/mbedtls/ssl_tls.c
    c-libp2p/thirdparty/mbedtls/threading.c
    c-libp2p/thirdparty/mbedtls/timing.c
    c-libp2p/thirdparty/mbedtls/version.c
    c-libp2p/thirdparty/mbedtls/version_features.c
    c-libp2p/thirdparty/mbedtls/x509.c
    c-libp2p/thirdparty/mbedtls/x509_create.c
    c-libp2p/thirdparty/mbedtls/x509_crl.c
    c-libp2p/thirdparty/mbedtls/x509_crt.c
    c-libp2p/thirdparty/mbedtls/x509_csr.c
    c-libp2p/thirdparty/mbedtls/x509write_crt.c
    c-libp2p/thirdparty/mbedtls/x509write_csr.c
    c-libp2p/thirdparty/mbedtls/xtea.c

    c-libp2p/hashmap/hashmap.c

    c-libp2p/net/multistream.c
    c-libp2p/net/protocol.c
    c-libp2p/net/sctp.c
    c-libp2p/net/socket.c
    c-libp2p/net/tcp.c
    c-libp2p/net/udp.c

    c-libp2p/os/utils.c

    c-libp2p/peer/peer.c
    c-libp2p/peer/peerstore.c
    c-libp2p/peer/providerstore.c

    c-libp2p/record/message.c
    c-libp2p/record/message_handler.c
    c-libp2p/record/record.c

    c-libp2p/routing/dht.c
    c-libp2p/routing/dht_protocol.c
    c-libp2p/routing/kademlia.c

#    c-libp2p/secio/char_vector.c
    c-libp2p/secio/exchange.c
    c-libp2p/secio/propose.c
    c-libp2p/secio/secio.c

    c-libp2p/utils/linked_list.c
    c-libp2p/utils/logger.c
    c-libp2p/utils/string_list.c
    c-libp2p/utils/vector.c
)



target_include_directories(c-libp2p PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/c-libp2p/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-multiaddr/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-multihash/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-protobuf/
)

add_library(c-ipfs
    c-ipfs/blocks/block.c
    c-ipfs/blocks/blockstore.c
    c-ipfs/cid/cid.c
    c-ipfs/cid/set.c
    c-ipfs/commands/argument.c
    c-ipfs/commands/command.c
    c-ipfs/commands/command_option.c

    c-ipfs/cmd/ipfs/init.c
#    c-ipfs/cmd/ipfs/main.c

    c-ipfs/core/api.c
    c-ipfs/core/bootstrap.c
    c-ipfs/core/builder.c
    c-ipfs/core/daemon.c
    c-ipfs/core/ipfs_node.c
#    c-ipfs/core/net.c
    c-ipfs/core/null.c
    c-ipfs/core/ping.c
    c-ipfs/datastore/ds_helper.c
    c-ipfs/datastore/key.c
    c-ipfs/dnslink/dnslink.c
    c-ipfs/flatfs/flatfs.c
    c-ipfs/importer/exporter.c
    c-ipfs/importer/importer.c
    c-ipfs/importer/resolver.c
    c-ipfs/merkledag/merkledag.c
    c-ipfs/merkledag/node.c
    c-ipfs/multibase/multibase.c
    c-ipfs/namesys/base.c
    c-ipfs/namesys/dns.c
    c-ipfs/namesys/is_domain_test.c
    c-ipfs/namesys/isdomain.c
    c-ipfs/namesys/namesys.c
    c-ipfs/namesys/pb.c
    c-ipfs/namesys/proquint.c
    c-ipfs/namesys/proquint_test.c
#    c-ipfs/namesys/publisher.c
#    c-ipfs/namesys/routing.c
    c-ipfs/path/path.c
#    c-ipfs/path/resolver.c
    c-ipfs/pin/pin.c

    c-ipfs/repo/init.c
    c-ipfs/repo/config/addresses.c
    c-ipfs/repo/config/bootstrap_peers.c
    c-ipfs/repo/config/config.c
    c-ipfs/repo/config/gateway.c
    c-ipfs/repo/config/identity.c
    c-ipfs/repo/config/peer.c
    c-ipfs/repo/config/replication.c
    c-ipfs/repo/config/swarm.c
    c-ipfs/repo/fsrepo/fs_repo.c
    c-ipfs/repo/fsrepo/jsmn.c
    c-ipfs/repo/fsrepo/lmdb_datastore.c


    c-ipfs/routing/k_routing.c
    c-ipfs/routing/offline.c
    c-ipfs/routing/online.c
    c-ipfs/routing/supernode.c
    c-ipfs/unixfs/unixfs.c
    c-ipfs/util/errs.c
    c-ipfs/util/thread_pool.c
    c-ipfs/util/time.c

    c-ipfs/exchange/bitswap/bitswap.c
    c-ipfs/exchange/bitswap/engine.c
    c-ipfs/exchange/bitswap/message.c
    c-ipfs/exchange/bitswap/network.c
    c-ipfs/exchange/bitswap/peer_request_queue.c
    c-ipfs/exchange/bitswap/want_manager.c
    c-ipfs/exchange/bitswap/wantlist_queue.c
)

target_include_directories(c-ipfs PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/c-libp2p/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-ipfs/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-protobuf/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-multiaddr/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-multihash/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/lmdb/libraries/liblmdb/
)

add_executable(ipfs 
    c-ipfs/main/main.c
)

target_link_libraries(ipfs
    c-multihash
    c-ipfs
    c-multiaddr
    c-protobuf
    c-libp2p
    lmdb
    -lresolv
)

add_executable(test_ipfs
    c-ipfs/test/test_helper.c
    c-ipfs/test/testit.c
)

target_include_directories(test_ipfs PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/c-protobuf/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-ipfs/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-libp2p/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/c-multiaddr/include/
)

target_link_libraries(test_ipfs
    c-multihash
    c-ipfs
    c-multiaddr
    c-protobuf
    c-libp2p
    lmdb
)


IF(APPLE)
   INCLUDE_DIRECTORIES ( /System/Library/Frameworks )
   FIND_LIBRARY(COCOA_LIBRARY Cocoa)
ENDIF(APPLE)

