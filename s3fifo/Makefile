FILES=checkpoint.cc commit_buffer.cc console.cc console_client.cc
FILES+=contention_manager.cc entity.cc epoch.cc felis_probes.cc
FILES+=gc.cc hashtable_index_impl.cc iface.cc
FILES+=index.cc index_common.cc locality_manager.cc log.cc
FILES+=main.cc masstree_index_impl.cc mem.cc module.cc
FILES+=node_config.cc piece.cc pwv_graph.cc #receiver.cc
FILES+=routine_sched.cc shipping.cc slice.cc tcp_node.cc txn.cc vhandle.cc vhandle_sync.cc
FILES+=util/locks.cc util/os_linux.cc

CXXFLAGS=-Wstrict-aliasing -DCACHE_LINE_SIZE=64 -DSPDLOG_COMPILED_LIB
CXXFLAGS+=-fno-omit-frame-pointer -mno-omit-leaf-frame-pointer
CXXFLAGS+=-Ofast -march=native -flto=thin
CXXFLAGS+=-std=c++17
#CXXFLAGS+=-stdlib=libc++
CXXFLAGS+=-fwhole-program-vtables -fvisibility=hidden -fvisibility-inlines-hidden -fforce-emit-vtables -fstrict-vtable-pointers -DNDEBUG
CXXFLAGS+=-Ispdlog/include

LDFLAGS=-lc++ -lc++abi -Lspdlog/build -lspdlog -Ljson11/build -ljson11 -lpthread -Lgopp/build -lgopp

all:
	clang++-8 $(CXXFLAGS) $(FILES) $(LDFLAGS)

