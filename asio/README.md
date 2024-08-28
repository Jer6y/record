# 软件包 : Boost.Asio

# 测试环境 

### OS : openEuler 2309 

### Arch : RISC-V

### Machine : Qemu-Virt

# 测试流程

1. 拉取  Boost 源码 并解压

   ```shell
   wget https://github.com/boostorg/boost/releases/download/boost-1.86.0/boost-1.86.0-b2-nodocs.tar.gz
   tar -xvf boost-1.86.0-b2-nodocs.tar.gz
   ```

2. 安装依赖

   ```shell
   sudo yum install gcc g++ cmake make 
   ```

3. 在 riscv 机器上编译安装

   ```shell
   ./b2 install --prefix=/usr
   ```

4. 拉取 Asio 测试相关源码

   ```shell
   git clone https://github.com/boostorg/asio.git -b master
   ```

5. 在 test 目录中添加下面两个文件

   ```
   touch Makefile 
   touch test.sh
   ```

6. Makefile 中的内容为

   ```makefile
   SRC:= $(shell find . -name "*.cpp")
   
   TARGETS:=$(patsubst %.cpp,%.out,${SRC})
   
   compile:$(TARGETS)
   
   
   test:$(TARGETS)
           bash ./test.sh $(TARGETS)
   
   %.out:%.cpp
           g++ -lcrypto -lssl $< -o $@
   
   debug:
           @echo ${TARGETS}
   
   .PHONY: debug compile test
   ```

7. test.sh 中的内容为

   ```shell
   #!/bin/bash
   TEST=$@
   for it in ${TEST}
   do
           ./${it}
   done
   ```

8. 将测试用例中的 experimental目录的用例去除（此处与 c++ 版本有关，编译失败）

   ```shell
   rm -rf experimental
   ```

9. 执行测试

   ```shell
   make test
   ```

   

# 测试结果

### 编译 : 通过

### 测试 : 通过

```shell
basic_signal_set test suite begins
null_test passed
basic_signal_set test suite ends

*** No errors detected.
uses_executor test suite begins
null_test passed
uses_executor test suite ends

*** No errors detected.
associated_allocator test suite begins
null_test passed
associated_allocator test suite ends

*** No errors detected.
file_base test suite begins
null_test passed
file_base test suite ends

*** No errors detected.
read_until test suite begins
test_dynamic_string_read_until_char passed
test_streambuf_read_until_char passed
test_dynamic_string_read_until_string passed
test_streambuf_read_until_string passed
test_dynamic_string_read_until_match_condition passed
test_streambuf_read_until_match_condition passed
test_dynamic_string_async_read_until_char passed
test_streambuf_async_read_until_char passed
test_dynamic_string_async_read_until_string passed
test_streambuf_async_read_until_string passed
test_dynamic_string_async_read_until_match_condition passed
test_streambuf_async_read_until_match_condition passed
read_until test suite ends

*** No errors detected.
basic_streambuf test suite begins
null_test passed
basic_streambuf test suite ends

*** No errors detected.
readable_pipe test suite begins
readable_pipe_compile::test passed
readable_pipe test suite ends

*** No errors detected.
high_resolution_timer test suite begins
null_test passed
high_resolution_timer test suite ends

*** No errors detected.
async_result test suite begins
null_test passed
async_result test suite ends

*** No errors detected.
strand test suite begins
strand_test passed
strand_conversion_test passed
strand_query_test passed
strand_execute_test passed
strand test suite ends

*** No errors detected.
basic_raw_socket test suite begins
null_test passed
basic_raw_socket test suite ends

*** No errors detected.
any_completion_executor test suite begins
any_completion_executor_construction_test passed
any_completion_executor_nothrow_construction_test passed
any_completion_executor_assignment_test passed
any_completion_executor_swap_test passed
any_completion_executor_query_test passed
any_completion_executor_execute_test passed
any_completion_executor test suite ends

*** No errors detected.
recycling_allocator test suite begins
recycling_allocator_test passed
recycling_allocator test suite ends

*** No errors detected.
use_awaitable test suite begins
null_test passed
use_awaitable test suite ends

*** No errors detected.
cancellation_signal test suite begins
null_test passed
cancellation_signal test suite ends

*** No errors detected.
basic_file test suite begins
null_test passed
basic_file test suite ends

*** No errors detected.
associated_immediate_executor test suite begins
null_test passed
associated_immediate_executor test suite ends

*** No errors detected.
immediate test suite begins
null_test passed
immediate test suite ends

*** No errors detected.
placeholders test suite begins
null_test passed
placeholders test suite ends

*** No errors detected.
redirect_error test suite begins
redirect_error_test passed
partial_redirect_error_test passed
redirect_error test suite ends

*** No errors detected.
cancellation_state test suite begins
null_test passed
cancellation_state test suite ends

*** No errors detected.
basic_waitable_timer test suite begins
null_test passed
basic_waitable_timer test suite ends

*** No errors detected.
completion_condition test suite begins
null_test passed
completion_condition test suite ends

*** No errors detected.
buffered_stream test suite begins
test_compile passed
test_sync_operations passed
test_async_operations passed
buffered_stream test suite ends

*** No errors detected.
append test suite begins
append_test passed
append test suite ends

*** No errors detected.
ip/unicast test suite begins
ip_unicast_compile::test passed
ip_unicast_runtime::test passed
ip/unicast test suite ends

*** No errors detected.
ip/basic_resolver_entry test suite begins
null_test passed
ip/basic_resolver_entry test suite ends

*** No errors detected.
ip/address_v6 test suite begins
ip_address_v6_compile::test passed
ip_address_v6_runtime::test passed
ip/address_v6 test suite ends

*** No errors detected.
ip/address_v4_range test suite begins
null_test passed
ip/address_v4_range test suite ends

*** No errors detected.
ip/basic_resolver test suite begins
null_test passed
ip/basic_resolver test suite ends

*** No errors detected.
ip/address_v4_iterator test suite begins
null_test passed
ip/address_v4_iterator test suite ends

*** No errors detected.
ip/address_v6_range test suite begins
null_test passed
ip/address_v6_range test suite ends

*** No errors detected.
ip/icmp test suite begins
ip_icmp_socket_compile::test passed
ip_icmp_resolver_compile::test passed
ip/icmp test suite ends

*** No errors detected.
ip/basic_endpoint test suite begins
null_test passed
ip/basic_endpoint test suite ends

*** No errors detected.
ip/basic_resolver_iterator test suite begins
null_test passed
ip/basic_resolver_iterator test suite ends

*** No errors detected.
ip/host_name test suite begins
ip_host_name_compile::test passed
ip/host_name test suite ends

*** No errors detected.
ip/network_v4 test suite begins
ip_network_v4_compile::test passed
ip_network_v4_runtime::test passed
ip/network_v4 test suite ends

*** No errors detected.
ip/address test suite begins
ip_address_compile::test passed
ip/address test suite ends

*** No errors detected.
ip/multicast test suite begins
ip_multicast_compile::test passed
ip_multicast_runtime::test passed
ip/multicast test suite ends

*** No errors detected.
ip/resolver_query_base test suite begins
null_test passed
ip/resolver_query_base test suite ends

*** No errors detected.
ip/basic_resolver_query test suite begins
null_test passed
ip/basic_resolver_query test suite ends

*** No errors detected.
ip/udp test suite begins
ip_udp_socket_compile::test passed
ip_udp_socket_runtime::test passed
ip_udp_resolver_compile::test passed
ip/udp test suite ends

*** No errors detected.
ip/network_v6 test suite begins
ip_network_v6_compile::test passed
ip_network_v6_runtime::test passed
ip/network_v6 test suite ends

*** No errors detected.
ip/tcp test suite begins
ip_tcp_compile::test passed
ip_tcp_runtime::test passed
ip_tcp_socket_compile::test passed
ip_tcp_socket_runtime::test passed
ip_tcp_acceptor_compile::test passed
ip_tcp_acceptor_runtime::test passed
ip_tcp_resolver_compile::test passed
ip_tcp_resolver_entry_compile::test passed
ip_tcp_resolver_entry_compile::test passed
ip_tcp_iostream_compile::test passed
ip/tcp test suite ends

*** No errors detected.
ip/address_v6_iterator test suite begins
null_test passed
ip/address_v6_iterator test suite ends

*** No errors detected.
ip/address_v4 test suite begins
ip_address_v4_compile::test passed
ip_address_v4_runtime::test passed
ip/address_v4 test suite ends

*** No errors detected.
ip/v6_only test suite begins
ip_v6_only_compile::test passed
ip_v6_only_runtime::test passed
ip/v6_only test suite ends

*** No errors detected.
local/basic_endpoint test suite begins
null_test passed
local/basic_endpoint test suite ends

*** No errors detected.
local/connect_pair test suite begins
local_connect_pair_compile::test passed
local/connect_pair test suite ends

*** No errors detected.
local/seq_packet_protocol test suite begins
local_seq_packet_protocol_socket_compile::test passed
local/seq_packet_protocol test suite ends

*** No errors detected.
local/stream_protocol test suite begins
local_stream_protocol_socket_compile::test passed
local/stream_protocol test suite ends

*** No errors detected.
local/datagram_protocol test suite begins
local_datagram_protocol_socket_compile::test passed
local/datagram_protocol test suite ends

*** No errors detected.
executor test suite begins
null_test passed
executor test suite ends

*** No errors detected.
signal_set test suite begins
signal_set_compile::test passed
signal_set test suite ends

*** No errors detected.
basic_writable_pipe test suite begins
null_test passed
basic_writable_pipe test suite ends

*** No errors detected.
buffers_iterator test suite begins
buffers_iterator_compile::test passed
buffers_iterator test suite ends

*** No errors detected.
execution_context test suite begins
null_test passed
execution_context test suite ends

*** No errors detected.
basic_serial_port test suite begins
null_test passed
basic_serial_port test suite ends

*** No errors detected.
wait_traits test suite begins
null_test passed
wait_traits test suite ends

*** No errors detected.
basic_readable_pipe test suite begins
null_test passed
basic_readable_pipe test suite ends

*** No errors detected.
deadline_timer test suite begins
deadline_timer_test passed
deadline_timer_cancel_test passed
deadline_timer_custom_allocation_test passed
deadline_timer_thread_test passed
deadline_timer_async_result_test passed
deadline_timer_move_test passed
deadline_timer test suite ends

*** No errors detected.
time_traits test suite begins
null_test passed
time_traits test suite ends

*** No errors detected.
basic_socket_acceptor test suite begins
null_test passed
basic_socket_acceptor test suite ends

*** No errors detected.
system_context test suite begins
null_test passed
system_context test suite ends

*** No errors detected.
use_future test suite begins
use_future_0_test passed
use_future_1_test passed
use_future_2_test passed
use_future_3_test passed
use_future_package_0_test passed
use_future_package_1_test passed
use_future_package_2_test passed
use_future_package_3_test passed
use_future test suite ends

*** No errors detected.
bind_executor test suite begins
bind_executor_to_function_object_test passed
bind_executor_to_completion_token_v1_test passed
bind_executor_to_completion_token_v2_test passed
partial_bind_executor_test passed
bind_executor test suite ends

*** No errors detected.
connect_pipe test suite begins
connect_pipe_compile::test passed
connect_pipe_runtime::test passed
connect_pipe test suite ends

*** No errors detected.
prepend test suite begins
prepend_test passed
prepend test suite ends

*** No errors detected.
bind_immediate_executor test suite begins
bind_immediate_executor_to_function_object_test passed
bind_immediate_executor_to_completion_token_v1_test passed
bind_immediate_executor_to_completion_token_v2_test passed
partial_bind_immediate_executor_test passed
bind_immediate_executor test suite ends

*** No errors detected.
buffered_read_stream test suite begins
test_compile passed
test_sync_operations passed
test_async_operations passed
buffered_read_stream test suite ends

*** No errors detected.
packaged_task test suite begins
null_test passed
packaged_task test suite ends

*** No errors detected.
strand test suite begins
strand_test passed
strand_wrap_test passed
strand test suite ends

*** No errors detected.
ts/socket test suite begins
null_test passed
ts/socket test suite ends

*** No errors detected.
ts/executor test suite begins
null_test passed
ts/executor test suite ends

*** No errors detected.
ts/net test suite begins
null_test passed
ts/net test suite ends

*** No errors detected.
ts/timer test suite begins
null_test passed
ts/timer test suite ends

*** No errors detected.
ts/netfwd test suite begins
null_test passed
ts/netfwd test suite ends

*** No errors detected.
ts/internet test suite begins
null_test passed
ts/internet test suite ends

*** No errors detected.
ts/buffer test suite begins
null_test passed
ts/buffer test suite ends

*** No errors detected.
ts/io_context test suite begins
null_test passed
ts/io_context test suite ends

*** No errors detected.
serial_port_base test suite begins
serial_port_base_compile::test passed
serial_port_base test suite ends

*** No errors detected.
basic_socket test suite begins
null_test passed
basic_socket test suite ends

*** No errors detected.
system_timer test suite begins
system_timer_test passed
system_timer_cancel_test passed
system_timer_custom_allocation_test passed
system_timer_thread_test passed
system_timer_move_test passed
system_timer_op_cancel_test passed
system_timer test suite ends

*** No errors detected.
bind_allocator test suite begins
bind_allocator_to_function_object_test passed
bind_allocator_to_completion_token_v1_test passed
bind_allocator_to_completion_token_v2_test passed
bind_allocator test suite ends

*** No errors detected.
thread_pool test suite begins
thread_pool_test passed
thread_pool_service_test passed
thread_pool_executor_query_test passed
thread_pool_executor_execute_test passed
thread_pool test suite ends

*** No errors detected.
associated_cancellation_slot test suite begins
null_test passed
associated_cancellation_slot test suite ends

*** No errors detected.
cancel_at test suite begins
cancel_at_function_object_test passed
cancel_at_timer_function_object_test passed
cancel_at_completion_token_v1_test passed
cancel_at_timer_completion_token_v1_test passed
cancel_at_completion_token_v2_test passed
cancel_at_timer_completion_token_v2_test passed
partial_cancel_at_test passed
partial_cancel_at_timer_test passed
cancel_at test suite ends

*** No errors detected.
write test suite begins
test_2_arg_zero_buffers_write passed
test_2_arg_const_buffer_write passed
test_2_arg_mutable_buffer_write passed
test_2_arg_vector_buffers_write passed
test_2_arg_dynamic_string_write passed
test_3_arg_nothrow_zero_buffers_write passed
test_3_arg_nothrow_const_buffer_write passed
test_3_arg_nothrow_mutable_buffer_write passed
test_3_arg_nothrow_vector_buffers_write passed
test_3_arg_nothrow_dynamic_string_write passed
test_3_arg_const_buffer_write passed
test_3_arg_mutable_buffer_write passed
test_3_arg_vector_buffers_write passed
test_3_arg_dynamic_string_write passed
test_4_arg_const_buffer_write passed
test_4_arg_mutable_buffer_write passed
test_4_arg_vector_buffers_write passed
test_4_arg_dynamic_string_write passed
test_3_arg_const_buffer_async_write passed
test_3_arg_mutable_buffer_async_write passed
test_3_arg_boost_array_buffers_async_write passed
test_3_arg_std_array_buffers_async_write passed
test_3_arg_vector_buffers_async_write passed
test_3_arg_dynamic_string_async_write passed
test_3_arg_streambuf_async_write passed
test_4_arg_const_buffer_async_write passed
test_4_arg_mutable_buffer_async_write passed
test_4_arg_boost_array_buffers_async_write passed
test_4_arg_std_array_buffers_async_write passed
test_4_arg_vector_buffers_async_write passed
test_4_arg_dynamic_string_async_write passed
test_4_arg_streambuf_async_write passed
write test suite ends

*** No errors detected.
invocable_archetype test suite begins
null_test passed
invocable_archetype test suite ends

*** No errors detected.
executor test suite begins
is_executor_test passed
executor test suite ends

*** No errors detected.
context_as test suite begins
context_as_executor_query_test passed
context_as test suite ends

*** No errors detected.
any_executor test suite begins
any_executor_construction_test passed
any_executor_nothrow_construction_test passed
any_executor_assignment_test passed
any_executor_swap_test passed
any_executor_query_test passed
any_executor_execute_test passed
any_executor test suite ends

*** No errors detected.
blocking test suite begins
test_can_query<ex_nq_nr,s,true> passed
test_can_query<ex_nq_nr,n1,true> passed
test_can_query<ex_nq_nr,n2,false> passed
test_can_query<ex_nq_nr,n3,false> passed
test_query<ex_nq_nr,s,n1> passed
test_query<ex_nq_nr,n1,n1> passed
test_constexpr_query<ex_nq_nr,s,n1> passed
test_constexpr_query<ex_nq_nr,n1,n1> passed
test_can_require<ex_nq_nr,s,false> passed
test_can_require<ex_nq_nr,n1,true> passed
test_can_require<ex_nq_nr,n2,false> passed
test_can_require<ex_nq_nr,n3,false> passed
test_require<ex_nq_nr,n1,n1> passed
test_can_prefer<ex_nq_nr,s,false> passed
test_can_prefer<ex_nq_nr,n1,true> passed
test_can_prefer<ex_nq_nr,n2,false> passed
test_can_prefer<ex_nq_nr,n3,true> passed
test_prefer<ex_nq_nr,n1,n1> passed
test_prefer<ex_nq_nr,n3,n1> passed
test_can_query<ex_cq_nr<s,s,n1>,s,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n3,true> passed
test_can_query<ex_cq_nr<s,s,n2>,s,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n3,true> passed
test_can_query<ex_cq_nr<s,s,n3>,s,true> passed
test_can_query<ex_cq_nr<s,s,n3>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n3>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n3>,n3,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n1>,n3,false> passed
test_can_query<ex_cq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n2>,n3,false> passed
test_can_query<ex_cq_nr<s,n1,n3>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n3>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n3>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n3>,n3,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n1>,n3,false> passed
test_can_query<ex_cq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,n3,false> passed
test_can_query<ex_cq_nr<s,n2,n3>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n3>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n3>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n3>,n3,false> passed
test_can_query<ex_cq_nr<s,n3,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n3,n1>,n1,false> passed
test_can_query<ex_cq_nr<s,n3,n1>,n2,false> passed
test_can_query<ex_cq_nr<s,n3,n1>,n3,true> passed
test_can_query<ex_cq_nr<s,n3,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n3,n2>,n1,false> passed
test_can_query<ex_cq_nr<s,n3,n2>,n2,false> passed
test_can_query<ex_cq_nr<s,n3,n2>,n3,true> passed
test_can_query<ex_cq_nr<s,n3,n3>,s,true> passed
test_can_query<ex_cq_nr<s,n3,n3>,n1,false> passed
test_can_query<ex_cq_nr<s,n3,n3>,n2,false> passed
test_can_query<ex_cq_nr<s,n3,n3>,n3,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n3,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n2,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n3,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,s,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,n1,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,n2,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,n3,true> passed
test_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_query<ex_cq_nr<s,s,n1>,n3,n1> passed
test_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_query<ex_cq_nr<s,s,n2>,n3,n2> passed
test_query<ex_cq_nr<s,s,n3>,s,n3> passed
test_query<ex_cq_nr<s,s,n3>,n1,n3> passed
test_query<ex_cq_nr<s,s,n3>,n2,n3> passed
test_query<ex_cq_nr<s,s,n3>,n3,n3> passed
test_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_cq_nr<s,n1,n3>,s,n3> passed
test_query<ex_cq_nr<s,n1,n3>,n1,n3> passed
test_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_cq_nr<s,n2,n3>,s,n3> passed
test_query<ex_cq_nr<s,n2,n3>,n2,n3> passed
test_query<ex_cq_nr<s,n3,n1>,s,n1> passed
test_query<ex_cq_nr<s,n3,n1>,n3,n1> passed
test_query<ex_cq_nr<s,n3,n2>,s,n2> passed
test_query<ex_cq_nr<s,n3,n2>,n3,n2> passed
test_query<ex_cq_nr<s,n3,n3>,s,n3> passed
test_query<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n3,n1> passed
test_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n3,n2> passed
test_query<ex_cq_nr<n3,s,n3>,s,n3> passed
test_query<ex_cq_nr<n3,s,n3>,n1,n3> passed
test_query<ex_cq_nr<n3,s,n3>,n2,n3> passed
test_query<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n3,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n3,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,n1,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,n2,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,n3,n3> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,n1,n3>,n1,n3> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,n2,n3>,n2,n3> passed
test_constexpr_query<ex_cq_nr<s,n3,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n3,n1>,n3,n1> passed
test_constexpr_query<ex_cq_nr<s,n3,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n3,n2>,n3,n2> passed
test_constexpr_query<ex_cq_nr<s,n3,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n3,n1> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n3,n2> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,n1,n3> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,n2,n3> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_can_require<ex_cq_nr<s,s,n1>,s,false> passed
test_can_require<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,s,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,s,n2>,s,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,s,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,s,n3>,s,false> passed
test_can_require<ex_cq_nr<s,s,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,s,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,s,n3>,n3,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,n3,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,n2,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,n3,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,n1,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,n2,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,s,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,n3,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<n1,s,n1>,n3,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n2,true> passed
test_can_require<ex_cq_nr<n2,s,n2>,n3,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,s,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,n1,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,n2,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,n3,true> passed
test_require<ex_cq_nr<s,s,n1>,n1,n1> passed
test_require<ex_cq_nr<s,s,n2>,n2,n2> passed
test_require<ex_cq_nr<s,s,n3>,n3,n3> passed
test_require<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_require<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_require<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_require<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_require<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_require<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_can_prefer<ex_cq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,s,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n3>,n2,false> passed
test_can_prefer<ex_cq_nr<s,s,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,s,false> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,n2,false> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,n3,true> passed
test_prefer<ex_cq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,s,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,s,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,s,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,s,n3>,n3,n3> passed
test_prefer<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n1,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n1,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,n1,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,n1,n3>,n3,n3> passed
test_prefer<ex_cq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n2,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n2,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,n2,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,n2,n3>,n3,n3> passed
test_prefer<ex_cq_nr<s,n3,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n3,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,n3,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n3,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,n3,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_prefer<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<n1,s,n1>,n3,n1> passed
test_prefer<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<n2,s,n2>,n3,n2> passed
test_prefer<ex_cq_nr<n3,s,n3>,n1,n3> passed
test_prefer<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_can_query<ex_mq_nr<s,s,n1>,s,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n3,true> passed
test_can_query<ex_mq_nr<s,s,n2>,s,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n3,true> passed
test_can_query<ex_mq_nr<s,s,n3>,s,true> passed
test_can_query<ex_mq_nr<s,s,n3>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n3>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n3>,n3,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n1>,n3,false> passed
test_can_query<ex_mq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n2>,n3,false> passed
test_can_query<ex_mq_nr<s,n1,n3>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n3>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n3>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n3>,n3,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n1>,n3,false> passed
test_can_query<ex_mq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,n3,false> passed
test_can_query<ex_mq_nr<s,n2,n3>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n3>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n3>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n3>,n3,false> passed
test_can_query<ex_mq_nr<s,n3,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n3,n1>,n1,false> passed
test_can_query<ex_mq_nr<s,n3,n1>,n2,false> passed
test_can_query<ex_mq_nr<s,n3,n1>,n3,true> passed
test_can_query<ex_mq_nr<s,n3,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n3,n2>,n1,false> passed
test_can_query<ex_mq_nr<s,n3,n2>,n2,false> passed
test_can_query<ex_mq_nr<s,n3,n2>,n3,true> passed
test_can_query<ex_mq_nr<s,n3,n3>,s,true> passed
test_can_query<ex_mq_nr<s,n3,n3>,n1,false> passed
test_can_query<ex_mq_nr<s,n3,n3>,n2,false> passed
test_can_query<ex_mq_nr<s,n3,n3>,n3,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n3,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n2,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n3,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,s,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,n1,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,n2,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,n3,true> passed
test_query<ex_mq_nr<s,s,n1>,s,n1> passed
test_query<ex_mq_nr<s,s,n1>,n1,n1> passed
test_query<ex_mq_nr<s,s,n1>,n2,n1> passed
test_query<ex_mq_nr<s,s,n1>,n3,n1> passed
test_query<ex_mq_nr<s,s,n2>,s,n2> passed
test_query<ex_mq_nr<s,s,n2>,n1,n2> passed
test_query<ex_mq_nr<s,s,n2>,n2,n2> passed
test_query<ex_mq_nr<s,s,n2>,n3,n2> passed
test_query<ex_mq_nr<s,s,n3>,s,n3> passed
test_query<ex_mq_nr<s,s,n3>,n1,n3> passed
test_query<ex_mq_nr<s,s,n3>,n2,n3> passed
test_query<ex_mq_nr<s,s,n3>,n3,n3> passed
test_query<ex_mq_nr<s,n1,n1>,s,n1> passed
test_query<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_mq_nr<s,n1,n2>,s,n2> passed
test_query<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_mq_nr<s,n1,n3>,s,n3> passed
test_query<ex_mq_nr<s,n1,n3>,n1,n3> passed
test_query<ex_mq_nr<s,n2,n1>,s,n1> passed
test_query<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_mq_nr<s,n2,n2>,s,n2> passed
test_query<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_mq_nr<s,n2,n3>,s,n3> passed
test_query<ex_mq_nr<s,n2,n3>,n2,n3> passed
test_query<ex_mq_nr<s,n3,n1>,s,n1> passed
test_query<ex_mq_nr<s,n3,n1>,n3,n1> passed
test_query<ex_mq_nr<s,n3,n2>,s,n2> passed
test_query<ex_mq_nr<s,n3,n2>,n3,n2> passed
test_query<ex_mq_nr<s,n3,n3>,s,n3> passed
test_query<ex_mq_nr<s,n3,n3>,n3,n3> passed
test_query<ex_mq_nr<n1,s,n1>,s,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n3,n1> passed
test_query<ex_mq_nr<n2,s,n2>,s,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n3,n2> passed
test_query<ex_mq_nr<n3,s,n3>,s,n3> passed
test_query<ex_mq_nr<n3,s,n3>,n1,n3> passed
test_query<ex_mq_nr<n3,s,n3>,n2,n3> passed
test_query<ex_mq_nr<n3,s,n3>,n3,n3> passed
test_can_require<ex_mq_nr<s,s,n1>,s,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,s,n2>,s,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,s,n3>,s,false> passed
test_can_require<ex_mq_nr<s,s,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n3>,n3,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,n3,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,n3,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,s,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,n3,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n3,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n2,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n3,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,s,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,n1,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,n2,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,n3,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,s,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n3>,n2,false> passed
test_can_prefer<ex_mq_nr<s,s,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,s,false> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,n2,false> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,n3,true> passed
test_prefer<ex_mq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,s,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,s,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,s,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,s,n3>,n3,n3> passed
test_prefer<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n1,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n1,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,n1,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,n1,n3>,n3,n3> passed
test_prefer<ex_mq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n2,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n2,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,n2,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,n2,n3>,n3,n3> passed
test_prefer<ex_mq_nr<s,n3,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n3,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,n3,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n3,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,n3,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,n3,n3>,n3,n3> passed
test_prefer<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<n1,s,n1>,n3,n1> passed
test_prefer<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<n2,s,n2>,n3,n2> passed
test_prefer<ex_mq_nr<n3,s,n3>,n1,n3> passed
test_prefer<ex_mq_nr<n3,s,n3>,n3,n3> passed
test_can_query<ex_fq_nr<s,s,n1>,s,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n3,true> passed
test_can_query<ex_fq_nr<s,s,n2>,s,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n3,true> passed
test_can_query<ex_fq_nr<s,s,n3>,s,true> passed
test_can_query<ex_fq_nr<s,s,n3>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n3>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n3>,n3,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n1>,n3,false> passed
test_can_query<ex_fq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n2>,n3,false> passed
test_can_query<ex_fq_nr<s,n1,n3>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n3>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n3>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n3>,n3,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n1>,n3,false> passed
test_can_query<ex_fq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,n3,false> passed
test_can_query<ex_fq_nr<s,n2,n3>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n3>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n3>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n3>,n3,false> passed
test_can_query<ex_fq_nr<s,n3,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n3,n1>,n1,false> passed
test_can_query<ex_fq_nr<s,n3,n1>,n2,false> passed
test_can_query<ex_fq_nr<s,n3,n1>,n3,true> passed
test_can_query<ex_fq_nr<s,n3,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n3,n2>,n1,false> passed
test_can_query<ex_fq_nr<s,n3,n2>,n2,false> passed
test_can_query<ex_fq_nr<s,n3,n2>,n3,true> passed
test_can_query<ex_fq_nr<s,n3,n3>,s,true> passed
test_can_query<ex_fq_nr<s,n3,n3>,n1,false> passed
test_can_query<ex_fq_nr<s,n3,n3>,n2,false> passed
test_can_query<ex_fq_nr<s,n3,n3>,n3,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n3,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n2,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n3,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,s,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,n1,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,n2,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,n3,true> passed
test_query<ex_fq_nr<s,s,n1>,s,n1> passed
test_query<ex_fq_nr<s,s,n1>,n1,n1> passed
test_query<ex_fq_nr<s,s,n1>,n2,n1> passed
test_query<ex_fq_nr<s,s,n1>,n3,n1> passed
test_query<ex_fq_nr<s,s,n2>,s,n2> passed
test_query<ex_fq_nr<s,s,n2>,n1,n2> passed
test_query<ex_fq_nr<s,s,n2>,n2,n2> passed
test_query<ex_fq_nr<s,s,n2>,n3,n2> passed
test_query<ex_fq_nr<s,s,n3>,s,n3> passed
test_query<ex_fq_nr<s,s,n3>,n1,n3> passed
test_query<ex_fq_nr<s,s,n3>,n2,n3> passed
test_query<ex_fq_nr<s,s,n3>,n3,n3> passed
test_query<ex_fq_nr<s,n1,n1>,s,n1> passed
test_query<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_fq_nr<s,n1,n2>,s,n2> passed
test_query<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_fq_nr<s,n1,n3>,s,n3> passed
test_query<ex_fq_nr<s,n1,n3>,n1,n3> passed
test_query<ex_fq_nr<s,n2,n1>,s,n1> passed
test_query<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_fq_nr<s,n2,n2>,s,n2> passed
test_query<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_fq_nr<s,n2,n3>,s,n3> passed
test_query<ex_fq_nr<s,n2,n3>,n2,n3> passed
test_query<ex_fq_nr<s,n3,n1>,s,n1> passed
test_query<ex_fq_nr<s,n3,n1>,n3,n1> passed
test_query<ex_fq_nr<s,n3,n2>,s,n2> passed
test_query<ex_fq_nr<s,n3,n2>,n3,n2> passed
test_query<ex_fq_nr<s,n3,n3>,s,n3> passed
test_query<ex_fq_nr<s,n3,n3>,n3,n3> passed
test_query<ex_fq_nr<n1,s,n1>,s,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n3,n1> passed
test_query<ex_fq_nr<n2,s,n2>,s,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n3,n2> passed
test_query<ex_fq_nr<n3,s,n3>,s,n3> passed
test_query<ex_fq_nr<n3,s,n3>,n1,n3> passed
test_query<ex_fq_nr<n3,s,n3>,n2,n3> passed
test_query<ex_fq_nr<n3,s,n3>,n3,n3> passed
test_can_require<ex_fq_nr<s,s,n1>,s,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,s,n2>,s,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,s,n3>,s,false> passed
test_can_require<ex_fq_nr<s,s,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n3>,n3,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,n3,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,n3,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,s,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,n3,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n3,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n2,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n3,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,s,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,n1,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,n2,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,n3,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,s,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n3>,n2,false> passed
test_can_prefer<ex_fq_nr<s,s,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,s,false> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,n2,false> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,n3,true> passed
test_prefer<ex_fq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,s,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,s,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,s,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,s,n3>,n3,n3> passed
test_prefer<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n1,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n1,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,n1,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,n1,n3>,n3,n3> passed
test_prefer<ex_fq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n2,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n2,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,n2,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,n2,n3>,n3,n3> passed
test_prefer<ex_fq_nr<s,n3,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n3,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,n3,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n3,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,n3,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,n3,n3>,n3,n3> passed
test_prefer<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<n1,s,n1>,n3,n1> passed
test_prefer<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<n2,s,n2>,n3,n2> passed
test_prefer<ex_fq_nr<n3,s,n3>,n1,n3> passed
test_prefer<ex_fq_nr<n3,s,n3>,n3,n3> passed
test_can_query<ex_mq_mr<n1,n1>,s,true> passed
test_can_query<ex_mq_mr<n1,n1>,n1,true> passed
test_can_query<ex_mq_mr<n1,n1>,n2,false> passed
test_can_query<ex_mq_mr<n1,n1>,n3,false> passed
test_can_query<ex_mq_mr<n1,n2>,s,true> passed
test_can_query<ex_mq_mr<n1,n2>,n1,true> passed
test_can_query<ex_mq_mr<n1,n2>,n2,true> passed
test_can_query<ex_mq_mr<n1,n2>,n3,false> passed
test_can_query<ex_mq_mr<n1,n3>,s,true> passed
test_can_query<ex_mq_mr<n1,n3>,n1,true> passed
test_can_query<ex_mq_mr<n1,n3>,n2,false> passed
test_can_query<ex_mq_mr<n1,n3>,n3,true> passed
test_can_query<ex_mq_mr<n2,n1>,s,true> passed
test_can_query<ex_mq_mr<n2,n1>,n1,true> passed
test_can_query<ex_mq_mr<n2,n1>,n2,true> passed
test_can_query<ex_mq_mr<n2,n1>,n3,false> passed
test_can_query<ex_mq_mr<n2,n2>,s,true> passed
test_can_query<ex_mq_mr<n2,n2>,n1,false> passed
test_can_query<ex_mq_mr<n2,n2>,n2,true> passed
test_can_query<ex_mq_mr<n2,n2>,n3,false> passed
test_can_query<ex_mq_mr<n2,n3>,s,true> passed
test_can_query<ex_mq_mr<n2,n3>,n1,false> passed
test_can_query<ex_mq_mr<n2,n3>,n2,true> passed
test_can_query<ex_mq_mr<n2,n3>,n3,true> passed
test_can_query<ex_mq_mr<n3,n1>,s,true> passed
test_can_query<ex_mq_mr<n3,n1>,n1,true> passed
test_can_query<ex_mq_mr<n3,n1>,n2,false> passed
test_can_query<ex_mq_mr<n3,n1>,n3,true> passed
test_can_query<ex_mq_mr<n3,n2>,s,true> passed
test_can_query<ex_mq_mr<n3,n2>,n1,false> passed
test_can_query<ex_mq_mr<n3,n2>,n2,true> passed
test_can_query<ex_mq_mr<n3,n2>,n3,true> passed
test_can_query<ex_mq_mr<n3,n3>,s,true> passed
test_can_query<ex_mq_mr<n3,n3>,n1,false> passed
test_can_query<ex_mq_mr<n3,n3>,n2,false> passed
test_can_query<ex_mq_mr<n3,n3>,n3,true> passed
test_query<ex_mq_mr<n1,n1>,s,n1> passed
test_query<ex_mq_mr<n1,n1>,n1,n1> passed
test_query<ex_mq_mr<n1,n2>,s,n1> passed
test_query<ex_mq_mr<n1,n2>,n1,n1> passed
test_query<ex_mq_mr<n1,n3>,s,n1> passed
test_query<ex_mq_mr<n1,n3>,n1,n1> passed
test_query<ex_mq_mr<n2,n1>,s,n2> passed
test_query<ex_mq_mr<n2,n1>,n2,n2> passed
test_query<ex_mq_mr<n2,n2>,s,n2> passed
test_query<ex_mq_mr<n2,n2>,n2,n2> passed
test_query<ex_mq_mr<n2,n3>,s,n2> passed
test_query<ex_mq_mr<n2,n3>,n2,n2> passed
test_query<ex_mq_mr<n3,n1>,s,n3> passed
test_query<ex_mq_mr<n3,n1>,n3,n3> passed
test_query<ex_mq_mr<n3,n2>,s,n3> passed
test_query<ex_mq_mr<n3,n2>,n3,n3> passed
test_query<ex_mq_mr<n3,n3>,s,n3> passed
test_query<ex_mq_mr<n3,n3>,n3,n3> passed
test_can_require<ex_mq_mr<n1,n1>,s,false> passed
test_can_require<ex_mq_mr<n1,n1>,n1,true> passed
test_can_require<ex_mq_mr<n1,n1>,n2,false> passed
test_can_require<ex_mq_mr<n1,n1>,n3,false> passed
test_can_require<ex_mq_mr<n1,n2>,s,false> passed
test_can_require<ex_mq_mr<n1,n2>,n1,true> passed
test_can_require<ex_mq_mr<n1,n2>,n2,true> passed
test_can_require<ex_mq_mr<n1,n2>,n3,false> passed
test_can_require<ex_mq_mr<n1,n3>,s,false> passed
test_can_require<ex_mq_mr<n1,n3>,n1,true> passed
test_can_require<ex_mq_mr<n1,n3>,n2,false> passed
test_can_require<ex_mq_mr<n1,n3>,n3,true> passed
test_can_require<ex_mq_mr<n2,n1>,s,false> passed
test_can_require<ex_mq_mr<n2,n1>,n1,true> passed
test_can_require<ex_mq_mr<n2,n1>,n2,true> passed
test_can_require<ex_mq_mr<n2,n1>,n3,false> passed
test_can_require<ex_mq_mr<n2,n2>,s,false> passed
test_can_require<ex_mq_mr<n2,n2>,n1,false> passed
test_can_require<ex_mq_mr<n2,n2>,n2,true> passed
test_can_require<ex_mq_mr<n2,n2>,n3,false> passed
test_can_require<ex_mq_mr<n2,n3>,s,false> passed
test_can_require<ex_mq_mr<n2,n3>,n1,false> passed
test_can_require<ex_mq_mr<n2,n3>,n2,true> passed
test_can_require<ex_mq_mr<n2,n3>,n3,true> passed
test_can_require<ex_mq_mr<n3,n1>,s,false> passed
test_can_require<ex_mq_mr<n3,n1>,n1,true> passed
test_can_require<ex_mq_mr<n3,n1>,n2,false> passed
test_can_require<ex_mq_mr<n3,n1>,n3,true> passed
test_can_require<ex_mq_mr<n3,n2>,s,false> passed
test_can_require<ex_mq_mr<n3,n2>,n1,false> passed
test_can_require<ex_mq_mr<n3,n2>,n2,true> passed
test_can_require<ex_mq_mr<n3,n2>,n3,true> passed
test_can_require<ex_mq_mr<n3,n3>,s,false> passed
test_can_require<ex_mq_mr<n3,n3>,n1,false> passed
test_can_require<ex_mq_mr<n3,n3>,n2,false> passed
test_can_require<ex_mq_mr<n3,n3>,n3,true> passed
test_require<ex_mq_mr<n1,n1>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n2,n2> passed
test_require<ex_mq_mr<n1,n3>,n1,n1> passed
test_require<ex_mq_mr<n1,n3>,n3,n3> passed
test_require<ex_mq_mr<n2,n1>,n1,n1> passed
test_require<ex_mq_mr<n2,n1>,n2,n2> passed
test_require<ex_mq_mr<n2,n2>,n2,n2> passed
test_require<ex_mq_mr<n2,n3>,n2,n2> passed
test_require<ex_mq_mr<n2,n3>,n3,n3> passed
test_require<ex_mq_mr<n3,n1>,n1,n1> passed
test_require<ex_mq_mr<n3,n1>,n3,n3> passed
test_require<ex_mq_mr<n3,n2>,n2,n2> passed
test_require<ex_mq_mr<n3,n2>,n3,n3> passed
test_require<ex_mq_mr<n3,n3>,n3,n3> passed
test_can_prefer<ex_mq_mr<n1,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n1>,n2,false> passed
test_can_prefer<ex_mq_mr<n1,n1>,n3,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,n2,false> passed
test_can_prefer<ex_mq_mr<n1,n2>,n3,true> passed
test_can_prefer<ex_mq_mr<n1,n3>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n3>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n3>,n2,false> passed
test_can_prefer<ex_mq_mr<n1,n3>,n3,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,n2,false> passed
test_can_prefer<ex_mq_mr<n2,n1>,n3,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,n2,false> passed
test_can_prefer<ex_mq_mr<n2,n2>,n3,true> passed
test_can_prefer<ex_mq_mr<n2,n3>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n3>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n3>,n2,false> passed
test_can_prefer<ex_mq_mr<n2,n3>,n3,true> passed
test_can_prefer<ex_mq_mr<n3,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n3,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n3,n1>,n2,false> passed
test_can_prefer<ex_mq_mr<n3,n1>,n3,true> passed
test_can_prefer<ex_mq_mr<n3,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n3,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n3,n2>,n2,false> passed
test_can_prefer<ex_mq_mr<n3,n2>,n3,true> passed
test_can_prefer<ex_mq_mr<n3,n3>,s,false> passed
test_can_prefer<ex_mq_mr<n3,n3>,n1,true> passed
test_can_prefer<ex_mq_mr<n3,n3>,n2,false> passed
test_can_prefer<ex_mq_mr<n3,n3>,n3,true> passed
test_prefer<ex_mq_mr<n1,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n1>,n3,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n3,n1> passed
test_prefer<ex_mq_mr<n1,n3>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n3>,n3,n3> passed
test_prefer<ex_mq_mr<n2,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n2,n1>,n3,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n1,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n3,n2> passed
test_prefer<ex_mq_mr<n2,n3>,n1,n2> passed
test_prefer<ex_mq_mr<n2,n3>,n3,n3> passed
test_prefer<ex_mq_mr<n3,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n3,n1>,n3,n3> passed
test_prefer<ex_mq_mr<n3,n2>,n1,n3> passed
test_prefer<ex_mq_mr<n3,n2>,n3,n3> passed
test_prefer<ex_mq_mr<n3,n3>,n1,n3> passed
test_prefer<ex_mq_mr<n3,n3>,n3,n3> passed
test_can_query<ex_fq_fr<n1,n1>,s,true> passed
test_can_query<ex_fq_fr<n1,n1>,n1,true> passed
test_can_query<ex_fq_fr<n1,n1>,n2,false> passed
test_can_query<ex_fq_fr<n1,n1>,n3,false> passed
test_can_query<ex_fq_fr<n1,n2>,s,true> passed
test_can_query<ex_fq_fr<n1,n2>,n1,true> passed
test_can_query<ex_fq_fr<n1,n2>,n2,true> passed
test_can_query<ex_fq_fr<n1,n2>,n3,false> passed
test_can_query<ex_fq_fr<n1,n3>,s,true> passed
test_can_query<ex_fq_fr<n1,n3>,n1,true> passed
test_can_query<ex_fq_fr<n1,n3>,n2,false> passed
test_can_query<ex_fq_fr<n1,n3>,n3,true> passed
test_can_query<ex_fq_fr<n2,n1>,s,true> passed
test_can_query<ex_fq_fr<n2,n1>,n1,true> passed
test_can_query<ex_fq_fr<n2,n1>,n2,true> passed
test_can_query<ex_fq_fr<n2,n1>,n3,false> passed
test_can_query<ex_fq_fr<n2,n2>,s,true> passed
test_can_query<ex_fq_fr<n2,n2>,n1,false> passed
test_can_query<ex_fq_fr<n2,n2>,n2,true> passed
test_can_query<ex_fq_fr<n2,n2>,n3,false> passed
test_can_query<ex_fq_fr<n2,n3>,s,true> passed
test_can_query<ex_fq_fr<n2,n3>,n1,false> passed
test_can_query<ex_fq_fr<n2,n3>,n2,true> passed
test_can_query<ex_fq_fr<n2,n3>,n3,true> passed
test_can_query<ex_fq_fr<n3,n1>,s,true> passed
test_can_query<ex_fq_fr<n3,n1>,n1,true> passed
test_can_query<ex_fq_fr<n3,n1>,n2,false> passed
test_can_query<ex_fq_fr<n3,n1>,n3,true> passed
test_can_query<ex_fq_fr<n3,n2>,s,true> passed
test_can_query<ex_fq_fr<n3,n2>,n1,false> passed
test_can_query<ex_fq_fr<n3,n2>,n2,true> passed
test_can_query<ex_fq_fr<n3,n2>,n3,true> passed
test_can_query<ex_fq_fr<n3,n3>,s,true> passed
test_can_query<ex_fq_fr<n3,n3>,n1,false> passed
test_can_query<ex_fq_fr<n3,n3>,n2,false> passed
test_can_query<ex_fq_fr<n3,n3>,n3,true> passed
test_query<ex_fq_fr<n1,n1>,s,n1> passed
test_query<ex_fq_fr<n1,n1>,n1,n1> passed
test_query<ex_fq_fr<n1,n2>,s,n1> passed
test_query<ex_fq_fr<n1,n2>,n1,n1> passed
test_query<ex_fq_fr<n1,n3>,s,n1> passed
test_query<ex_fq_fr<n1,n3>,n1,n1> passed
test_query<ex_fq_fr<n2,n1>,s,n2> passed
test_query<ex_fq_fr<n2,n1>,n2,n2> passed
test_query<ex_fq_fr<n2,n2>,s,n2> passed
test_query<ex_fq_fr<n2,n2>,n2,n2> passed
test_query<ex_fq_fr<n2,n3>,s,n2> passed
test_query<ex_fq_fr<n2,n3>,n2,n2> passed
test_query<ex_fq_fr<n3,n1>,s,n3> passed
test_query<ex_fq_fr<n3,n1>,n3,n3> passed
test_query<ex_fq_fr<n3,n2>,s,n3> passed
test_query<ex_fq_fr<n3,n2>,n3,n3> passed
test_query<ex_fq_fr<n3,n3>,s,n3> passed
test_query<ex_fq_fr<n3,n3>,n3,n3> passed
test_can_require<ex_fq_fr<n1,n1>,s,false> passed
test_can_require<ex_fq_fr<n1,n1>,n1,true> passed
test_can_require<ex_fq_fr<n1,n1>,n2,false> passed
test_can_require<ex_fq_fr<n1,n1>,n3,false> passed
test_can_require<ex_fq_fr<n1,n2>,s,false> passed
test_can_require<ex_fq_fr<n1,n2>,n1,true> passed
test_can_require<ex_fq_fr<n1,n2>,n2,true> passed
test_can_require<ex_fq_fr<n1,n2>,n3,false> passed
test_can_require<ex_fq_fr<n1,n3>,s,false> passed
test_can_require<ex_fq_fr<n1,n3>,n1,true> passed
test_can_require<ex_fq_fr<n1,n3>,n2,false> passed
test_can_require<ex_fq_fr<n1,n3>,n3,true> passed
test_can_require<ex_fq_fr<n2,n1>,s,false> passed
test_can_require<ex_fq_fr<n2,n1>,n1,true> passed
test_can_require<ex_fq_fr<n2,n1>,n2,true> passed
test_can_require<ex_fq_fr<n2,n1>,n3,false> passed
test_can_require<ex_fq_fr<n2,n2>,s,false> passed
test_can_require<ex_fq_fr<n2,n2>,n1,false> passed
test_can_require<ex_fq_fr<n2,n2>,n2,true> passed
test_can_require<ex_fq_fr<n2,n2>,n3,false> passed
test_can_require<ex_fq_fr<n2,n3>,s,false> passed
test_can_require<ex_fq_fr<n2,n3>,n1,false> passed
test_can_require<ex_fq_fr<n2,n3>,n2,true> passed
test_can_require<ex_fq_fr<n2,n3>,n3,true> passed
test_can_require<ex_fq_fr<n3,n1>,s,false> passed
test_can_require<ex_fq_fr<n3,n1>,n1,true> passed
test_can_require<ex_fq_fr<n3,n1>,n2,false> passed
test_can_require<ex_fq_fr<n3,n1>,n3,true> passed
test_can_require<ex_fq_fr<n3,n2>,s,false> passed
test_can_require<ex_fq_fr<n3,n2>,n1,false> passed
test_can_require<ex_fq_fr<n3,n2>,n2,true> passed
test_can_require<ex_fq_fr<n3,n2>,n3,true> passed
test_can_require<ex_fq_fr<n3,n3>,s,false> passed
test_can_require<ex_fq_fr<n3,n3>,n1,false> passed
test_can_require<ex_fq_fr<n3,n3>,n2,false> passed
test_can_require<ex_fq_fr<n3,n3>,n3,true> passed
test_require<ex_fq_fr<n1,n1>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n2,n2> passed
test_require<ex_fq_fr<n1,n3>,n1,n1> passed
test_require<ex_fq_fr<n1,n3>,n3,n3> passed
test_require<ex_fq_fr<n2,n1>,n1,n1> passed
test_require<ex_fq_fr<n2,n1>,n2,n2> passed
test_require<ex_fq_fr<n2,n2>,n2,n2> passed
test_require<ex_fq_fr<n2,n3>,n2,n2> passed
test_require<ex_fq_fr<n2,n3>,n3,n3> passed
test_require<ex_fq_fr<n3,n1>,n1,n1> passed
test_require<ex_fq_fr<n3,n1>,n3,n3> passed
test_require<ex_fq_fr<n3,n2>,n2,n2> passed
test_require<ex_fq_fr<n3,n2>,n3,n3> passed
test_require<ex_fq_fr<n3,n3>,n3,n3> passed
test_can_prefer<ex_fq_fr<n1,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n1>,n2,false> passed
test_can_prefer<ex_fq_fr<n1,n1>,n3,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,n2,false> passed
test_can_prefer<ex_fq_fr<n1,n2>,n3,true> passed
test_can_prefer<ex_fq_fr<n1,n3>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n3>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n3>,n2,false> passed
test_can_prefer<ex_fq_fr<n1,n3>,n3,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,n2,false> passed
test_can_prefer<ex_fq_fr<n2,n1>,n3,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,n2,false> passed
test_can_prefer<ex_fq_fr<n2,n2>,n3,true> passed
test_can_prefer<ex_fq_fr<n2,n3>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n3>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n3>,n2,false> passed
test_can_prefer<ex_fq_fr<n2,n3>,n3,true> passed
test_can_prefer<ex_fq_fr<n3,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n3,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n3,n1>,n2,false> passed
test_can_prefer<ex_fq_fr<n3,n1>,n3,true> passed
test_can_prefer<ex_fq_fr<n3,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n3,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n3,n2>,n2,false> passed
test_can_prefer<ex_fq_fr<n3,n2>,n3,true> passed
test_can_prefer<ex_fq_fr<n3,n3>,s,false> passed
test_can_prefer<ex_fq_fr<n3,n3>,n1,true> passed
test_can_prefer<ex_fq_fr<n3,n3>,n2,false> passed
test_can_prefer<ex_fq_fr<n3,n3>,n3,true> passed
test_prefer<ex_fq_fr<n1,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n1>,n3,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n3,n1> passed
test_prefer<ex_fq_fr<n1,n3>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n3>,n3,n3> passed
test_prefer<ex_fq_fr<n2,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n2,n1>,n3,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n1,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n3,n2> passed
test_prefer<ex_fq_fr<n2,n3>,n1,n2> passed
test_prefer<ex_fq_fr<n2,n3>,n3,n3> passed
test_prefer<ex_fq_fr<n3,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n3,n1>,n3,n3> passed
test_prefer<ex_fq_fr<n3,n2>,n1,n3> passed
test_prefer<ex_fq_fr<n3,n2>,n3,n3> passed
test_prefer<ex_fq_fr<n3,n3>,n1,n3> passed
test_prefer<ex_fq_fr<n3,n3>,n3,n3> passed
test_vars passed
blocking test suite ends

*** No errors detected.
blocking_adaptation test suite begins
test_can_query<ex_nq_nr,s,true> passed
test_can_query<ex_nq_nr,n1,true> passed
test_can_query<ex_nq_nr,n2,false> passed
test_query<ex_nq_nr,s,n1> passed
test_query<ex_nq_nr,n1,n1> passed
test_constexpr_query<ex_nq_nr,s,n1> passed
test_constexpr_query<ex_nq_nr,n1,n1> passed
test_can_require<ex_nq_nr,s,false> passed
test_can_require<ex_nq_nr,n1,true> passed
test_can_require<ex_nq_nr,n2,true> passed
test_require<ex_nq_nr,n1,n1> passed
test_require<ex_nq_nr,n2,n2> passed
test_can_prefer<ex_nq_nr,s,false> passed
test_can_prefer<ex_nq_nr,n1,true> passed
test_can_prefer<ex_nq_nr,n2,false> passed
test_prefer<ex_nq_nr,n1,n1> passed
test_can_query<ex_cq_nr<s,s,n1>,s,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n2>,s,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n2,true> passed
test_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_cq_nr<s,s,n1>,s,false> passed
test_can_require<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_require<ex_cq_nr<s,s,n2>,s,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,n2,true> passed
test_can_require<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_require<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_require<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n2,true> passed
test_require<ex_cq_nr<s,s,n1>,n1,n1> passed
test_require<ex_cq_nr<s,s,n1>,n2,n2> passed
test_require<ex_cq_nr<s,s,n2>,n2,n2> passed
test_require<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_require<ex_cq_nr<s,n1,n1>,n2,n2> passed
test_require<ex_cq_nr<s,n1,n2>,n2,n2> passed
test_require<ex_cq_nr<s,n2,n1>,n2,n2> passed
test_require<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_require<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_require<ex_cq_nr<n1,s,n1>,n2,n2> passed
test_require<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_prefer<ex_cq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n2,false> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n2,false> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n2,false> passed
test_prefer<ex_cq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_can_query<ex_mq_nr<s,s,n1>,s,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n2>,s,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n2,true> passed
test_query<ex_mq_nr<s,s,n1>,s,n1> passed
test_query<ex_mq_nr<s,s,n1>,n1,n1> passed
test_query<ex_mq_nr<s,s,n1>,n2,n1> passed
test_query<ex_mq_nr<s,s,n2>,s,n2> passed
test_query<ex_mq_nr<s,s,n2>,n1,n2> passed
test_query<ex_mq_nr<s,s,n2>,n2,n2> passed
test_query<ex_mq_nr<s,n1,n1>,s,n1> passed
test_query<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_mq_nr<s,n1,n2>,s,n2> passed
test_query<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_mq_nr<s,n2,n1>,s,n1> passed
test_query<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_mq_nr<s,n2,n2>,s,n2> passed
test_query<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_mq_nr<n1,s,n1>,s,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_mq_nr<n2,s,n2>,s,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_mq_nr<s,s,n1>,s,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_require<ex_mq_nr<s,s,n2>,s,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_require<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n2,true> passed
test_can_require<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n2,true> passed
test_can_require<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_require<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_require<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_require<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n2,true> passed
test_require<ex_mq_nr<s,s,n1>,n2,n2> passed
test_require<ex_mq_nr<s,s,n2>,n2,n2> passed
test_require<ex_mq_nr<s,n1,n1>,n2,n2> passed
test_require<ex_mq_nr<s,n1,n2>,n2,n2> passed
test_require<ex_mq_nr<s,n2,n1>,n2,n2> passed
test_require<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_require<ex_mq_nr<n1,s,n1>,n2,n2> passed
test_require<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_can_prefer<ex_mq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n2,false> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n2,false> passed
test_prefer<ex_mq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_can_query<ex_fq_nr<s,s,n1>,s,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n2>,s,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n2,true> passed
test_query<ex_fq_nr<s,s,n1>,s,n1> passed
test_query<ex_fq_nr<s,s,n1>,n1,n1> passed
test_query<ex_fq_nr<s,s,n1>,n2,n1> passed
test_query<ex_fq_nr<s,s,n2>,s,n2> passed
test_query<ex_fq_nr<s,s,n2>,n1,n2> passed
test_query<ex_fq_nr<s,s,n2>,n2,n2> passed
test_query<ex_fq_nr<s,n1,n1>,s,n1> passed
test_query<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_fq_nr<s,n1,n2>,s,n2> passed
test_query<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_fq_nr<s,n2,n1>,s,n1> passed
test_query<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_fq_nr<s,n2,n2>,s,n2> passed
test_query<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_fq_nr<n1,s,n1>,s,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_fq_nr<n2,s,n2>,s,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_fq_nr<s,s,n1>,s,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_require<ex_fq_nr<s,s,n2>,s,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_require<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n2,true> passed
test_can_require<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n2,true> passed
test_can_require<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_require<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_require<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_require<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n2,true> passed
test_require<ex_fq_nr<s,s,n1>,n2,n2> passed
test_require<ex_fq_nr<s,s,n2>,n2,n2> passed
test_require<ex_fq_nr<s,n1,n1>,n2,n2> passed
test_require<ex_fq_nr<s,n1,n2>,n2,n2> passed
test_require<ex_fq_nr<s,n2,n1>,n2,n2> passed
test_require<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_require<ex_fq_nr<n1,s,n1>,n2,n2> passed
test_require<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_can_prefer<ex_fq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n2,false> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n2,false> passed
test_prefer<ex_fq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_can_query<ex_mq_mr<n1,n1>,s,true> passed
test_can_query<ex_mq_mr<n1,n1>,n1,true> passed
test_can_query<ex_mq_mr<n1,n1>,n2,false> passed
test_can_query<ex_mq_mr<n1,n2>,s,true> passed
test_can_query<ex_mq_mr<n1,n2>,n1,true> passed
test_can_query<ex_mq_mr<n1,n2>,n2,true> passed
test_can_query<ex_mq_mr<n2,n1>,s,true> passed
test_can_query<ex_mq_mr<n2,n1>,n1,true> passed
test_can_query<ex_mq_mr<n2,n1>,n2,true> passed
test_can_query<ex_mq_mr<n2,n2>,s,true> passed
test_can_query<ex_mq_mr<n2,n2>,n1,false> passed
test_can_query<ex_mq_mr<n2,n2>,n2,true> passed
test_query<ex_mq_mr<n1,n1>,s,n1> passed
test_query<ex_mq_mr<n1,n1>,n1,n1> passed
test_query<ex_mq_mr<n1,n2>,s,n1> passed
test_query<ex_mq_mr<n1,n2>,n1,n1> passed
test_query<ex_mq_mr<n2,n1>,s,n2> passed
test_query<ex_mq_mr<n2,n1>,n2,n2> passed
test_query<ex_mq_mr<n2,n2>,s,n2> passed
test_query<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_require<ex_mq_mr<n1,n1>,s,false> passed
test_can_require<ex_mq_mr<n1,n1>,n1,true> passed
test_can_require<ex_mq_mr<n1,n1>,n2,true> passed
test_can_require<ex_mq_mr<n1,n2>,s,false> passed
test_can_require<ex_mq_mr<n1,n2>,n1,true> passed
test_can_require<ex_mq_mr<n1,n2>,n2,true> passed
test_can_require<ex_mq_mr<n2,n1>,s,false> passed
test_can_require<ex_mq_mr<n2,n1>,n1,true> passed
test_can_require<ex_mq_mr<n2,n1>,n2,true> passed
test_can_require<ex_mq_mr<n2,n2>,s,false> passed
test_can_require<ex_mq_mr<n2,n2>,n1,false> passed
test_can_require<ex_mq_mr<n2,n2>,n2,true> passed
test_require<ex_mq_mr<n1,n1>,n1,n1> passed
test_require<ex_mq_mr<n1,n1>,n2,n2> passed
test_require<ex_mq_mr<n1,n2>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n2,n2> passed
test_require<ex_mq_mr<n2,n1>,n1,n1> passed
test_require<ex_mq_mr<n2,n1>,n2,n2> passed
test_require<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_prefer<ex_mq_mr<n1,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n1>,n2,false> passed
test_can_prefer<ex_mq_mr<n1,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,n2,false> passed
test_can_prefer<ex_mq_mr<n2,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,n2,false> passed
test_can_prefer<ex_mq_mr<n2,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,n2,false> passed
test_prefer<ex_mq_mr<n1,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n1,n1> passed
test_prefer<ex_mq_mr<n2,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n2,n2>,n1,n2> passed
test_can_query<ex_fq_fr<n1,n1>,s,true> passed
test_can_query<ex_fq_fr<n1,n1>,n1,true> passed
test_can_query<ex_fq_fr<n1,n1>,n2,false> passed
test_can_query<ex_fq_fr<n1,n2>,s,true> passed
test_can_query<ex_fq_fr<n1,n2>,n1,true> passed
test_can_query<ex_fq_fr<n1,n2>,n2,true> passed
test_can_query<ex_fq_fr<n2,n1>,s,true> passed
test_can_query<ex_fq_fr<n2,n1>,n1,true> passed
test_can_query<ex_fq_fr<n2,n1>,n2,true> passed
test_can_query<ex_fq_fr<n2,n2>,s,true> passed
test_can_query<ex_fq_fr<n2,n2>,n1,false> passed
test_can_query<ex_fq_fr<n2,n2>,n2,true> passed
test_query<ex_fq_fr<n1,n1>,s,n1> passed
test_query<ex_fq_fr<n1,n1>,n1,n1> passed
test_query<ex_fq_fr<n1,n2>,s,n1> passed
test_query<ex_fq_fr<n1,n2>,n1,n1> passed
test_query<ex_fq_fr<n2,n1>,s,n2> passed
test_query<ex_fq_fr<n2,n1>,n2,n2> passed
test_query<ex_fq_fr<n2,n2>,s,n2> passed
test_query<ex_fq_fr<n2,n2>,n2,n2> passed
test_can_require<ex_fq_fr<n1,n1>,s,false> passed
test_can_require<ex_fq_fr<n1,n1>,n1,true> passed
test_can_require<ex_fq_fr<n1,n1>,n2,true> passed
test_can_require<ex_fq_fr<n1,n2>,s,false> passed
test_can_require<ex_fq_fr<n1,n2>,n1,true> passed
test_can_require<ex_fq_fr<n1,n2>,n2,true> passed
test_can_require<ex_fq_fr<n2,n1>,s,false> passed
test_can_require<ex_fq_fr<n2,n1>,n1,true> passed
test_can_require<ex_fq_fr<n2,n1>,n2,true> passed
test_can_require<ex_fq_fr<n2,n2>,s,false> passed
test_can_require<ex_fq_fr<n2,n2>,n1,false> passed
test_can_require<ex_fq_fr<n2,n2>,n2,true> passed
test_require<ex_fq_fr<n1,n1>,n1,n1> passed
test_require<ex_fq_fr<n1,n1>,n2,n2> passed
test_require<ex_fq_fr<n1,n2>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n2,n2> passed
test_require<ex_fq_fr<n2,n1>,n1,n1> passed
test_require<ex_fq_fr<n2,n1>,n2,n2> passed
test_require<ex_fq_fr<n2,n2>,n2,n2> passed
test_can_prefer<ex_fq_fr<n1,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n1>,n2,false> passed
test_can_prefer<ex_fq_fr<n1,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,n2,false> passed
test_can_prefer<ex_fq_fr<n2,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,n2,false> passed
test_can_prefer<ex_fq_fr<n2,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,n2,false> passed
test_prefer<ex_fq_fr<n1,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n1,n1> passed
test_prefer<ex_fq_fr<n2,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n2,n2>,n1,n2> passed
test_vars passed
blocking_adaptation test suite ends

*** No errors detected.
relationship test suite begins
test_can_query<ex_nq_nr,s,true> passed
test_can_query<ex_nq_nr,n1,true> passed
test_can_query<ex_nq_nr,n2,false> passed
test_query<ex_nq_nr,s,n1> passed
test_query<ex_nq_nr,n1,n1> passed
test_constexpr_query<ex_nq_nr,s,n1> passed
test_constexpr_query<ex_nq_nr,n1,n1> passed
test_can_require<ex_nq_nr,s,false> passed
test_can_require<ex_nq_nr,n1,true> passed
test_can_require<ex_nq_nr,n2,false> passed
test_require<ex_nq_nr,n1,n1> passed
test_can_prefer<ex_nq_nr,s,false> passed
test_can_prefer<ex_nq_nr,n1,true> passed
test_can_prefer<ex_nq_nr,n2,true> passed
test_prefer<ex_nq_nr,n1,n1> passed
test_prefer<ex_nq_nr,n2,n1> passed
test_can_query<ex_cq_nr<s,s,n1>,s,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n2>,s,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n2,true> passed
test_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_cq_nr<s,s,n1>,s,false> passed
test_can_require<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,s,n2>,s,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n2,true> passed
test_require<ex_cq_nr<s,s,n1>,n1,n1> passed
test_require<ex_cq_nr<s,s,n2>,n2,n2> passed
test_require<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_require<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_require<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_require<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_prefer<ex_cq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n2,true> passed
test_prefer<ex_cq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_query<ex_mq_nr<s,s,n1>,s,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n2>,s,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n2,true> passed
test_query<ex_mq_nr<s,s,n1>,s,n1> passed
test_query<ex_mq_nr<s,s,n1>,n1,n1> passed
test_query<ex_mq_nr<s,s,n1>,n2,n1> passed
test_query<ex_mq_nr<s,s,n2>,s,n2> passed
test_query<ex_mq_nr<s,s,n2>,n1,n2> passed
test_query<ex_mq_nr<s,s,n2>,n2,n2> passed
test_query<ex_mq_nr<s,n1,n1>,s,n1> passed
test_query<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_mq_nr<s,n1,n2>,s,n2> passed
test_query<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_mq_nr<s,n2,n1>,s,n1> passed
test_query<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_mq_nr<s,n2,n2>,s,n2> passed
test_query<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_mq_nr<n1,s,n1>,s,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_mq_nr<n2,s,n2>,s,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_mq_nr<s,s,n1>,s,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n2>,s,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n2,true> passed
test_prefer<ex_mq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_can_query<ex_fq_nr<s,s,n1>,s,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n2>,s,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n2,true> passed
test_query<ex_fq_nr<s,s,n1>,s,n1> passed
test_query<ex_fq_nr<s,s,n1>,n1,n1> passed
test_query<ex_fq_nr<s,s,n1>,n2,n1> passed
test_query<ex_fq_nr<s,s,n2>,s,n2> passed
test_query<ex_fq_nr<s,s,n2>,n1,n2> passed
test_query<ex_fq_nr<s,s,n2>,n2,n2> passed
test_query<ex_fq_nr<s,n1,n1>,s,n1> passed
test_query<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_fq_nr<s,n1,n2>,s,n2> passed
test_query<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_fq_nr<s,n2,n1>,s,n1> passed
test_query<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_fq_nr<s,n2,n2>,s,n2> passed
test_query<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_fq_nr<n1,s,n1>,s,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_fq_nr<n2,s,n2>,s,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_fq_nr<s,s,n1>,s,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n2>,s,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n2,true> passed
test_prefer<ex_fq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_can_query<ex_mq_mr<n1,n1>,s,true> passed
test_can_query<ex_mq_mr<n1,n1>,n1,true> passed
test_can_query<ex_mq_mr<n1,n1>,n2,false> passed
test_can_query<ex_mq_mr<n1,n2>,s,true> passed
test_can_query<ex_mq_mr<n1,n2>,n1,true> passed
test_can_query<ex_mq_mr<n1,n2>,n2,true> passed
test_can_query<ex_mq_mr<n2,n1>,s,true> passed
test_can_query<ex_mq_mr<n2,n1>,n1,true> passed
test_can_query<ex_mq_mr<n2,n1>,n2,true> passed
test_can_query<ex_mq_mr<n2,n2>,s,true> passed
test_can_query<ex_mq_mr<n2,n2>,n1,false> passed
test_can_query<ex_mq_mr<n2,n2>,n2,true> passed
test_query<ex_mq_mr<n1,n1>,s,n1> passed
test_query<ex_mq_mr<n1,n1>,n1,n1> passed
test_query<ex_mq_mr<n1,n2>,s,n1> passed
test_query<ex_mq_mr<n1,n2>,n1,n1> passed
test_query<ex_mq_mr<n2,n1>,s,n2> passed
test_query<ex_mq_mr<n2,n1>,n2,n2> passed
test_query<ex_mq_mr<n2,n2>,s,n2> passed
test_query<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_require<ex_mq_mr<n1,n1>,s,false> passed
test_can_require<ex_mq_mr<n1,n1>,n1,true> passed
test_can_require<ex_mq_mr<n1,n1>,n2,false> passed
test_can_require<ex_mq_mr<n1,n2>,s,false> passed
test_can_require<ex_mq_mr<n1,n2>,n1,true> passed
test_can_require<ex_mq_mr<n1,n2>,n2,true> passed
test_can_require<ex_mq_mr<n2,n1>,s,false> passed
test_can_require<ex_mq_mr<n2,n1>,n1,true> passed
test_can_require<ex_mq_mr<n2,n1>,n2,true> passed
test_can_require<ex_mq_mr<n2,n2>,s,false> passed
test_can_require<ex_mq_mr<n2,n2>,n1,false> passed
test_can_require<ex_mq_mr<n2,n2>,n2,true> passed
test_require<ex_mq_mr<n1,n1>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n2,n2> passed
test_require<ex_mq_mr<n2,n1>,n1,n1> passed
test_require<ex_mq_mr<n2,n1>,n2,n2> passed
test_require<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_prefer<ex_mq_mr<n1,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n1>,n2,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,n2,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,n2,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,n2,true> passed
test_prefer<ex_mq_mr<n1,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n1>,n2,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n2,n2> passed
test_prefer<ex_mq_mr<n2,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n2,n1>,n2,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n1,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_query<ex_fq_fr<n1,n1>,s,true> passed
test_can_query<ex_fq_fr<n1,n1>,n1,true> passed
test_can_query<ex_fq_fr<n1,n1>,n2,false> passed
test_can_query<ex_fq_fr<n1,n2>,s,true> passed
test_can_query<ex_fq_fr<n1,n2>,n1,true> passed
test_can_query<ex_fq_fr<n1,n2>,n2,true> passed
test_can_query<ex_fq_fr<n2,n1>,s,true> passed
test_can_query<ex_fq_fr<n2,n1>,n1,true> passed
test_can_query<ex_fq_fr<n2,n1>,n2,true> passed
test_can_query<ex_fq_fr<n2,n2>,s,true> passed
test_can_query<ex_fq_fr<n2,n2>,n1,false> passed
test_can_query<ex_fq_fr<n2,n2>,n2,true> passed
test_query<ex_fq_fr<n1,n1>,s,n1> passed
test_query<ex_fq_fr<n1,n1>,n1,n1> passed
test_query<ex_fq_fr<n1,n2>,s,n1> passed
test_query<ex_fq_fr<n1,n2>,n1,n1> passed
test_query<ex_fq_fr<n2,n1>,s,n2> passed
test_query<ex_fq_fr<n2,n1>,n2,n2> passed
test_query<ex_fq_fr<n2,n2>,s,n2> passed
test_query<ex_fq_fr<n2,n2>,n2,n2> passed
test_can_require<ex_fq_fr<n1,n1>,s,false> passed
test_can_require<ex_fq_fr<n1,n1>,n1,true> passed
test_can_require<ex_fq_fr<n1,n1>,n2,false> passed
test_can_require<ex_fq_fr<n1,n2>,s,false> passed
test_can_require<ex_fq_fr<n1,n2>,n1,true> passed
test_can_require<ex_fq_fr<n1,n2>,n2,true> passed
test_can_require<ex_fq_fr<n2,n1>,s,false> passed
test_can_require<ex_fq_fr<n2,n1>,n1,true> passed
test_can_require<ex_fq_fr<n2,n1>,n2,true> passed
test_can_require<ex_fq_fr<n2,n2>,s,false> passed
test_can_require<ex_fq_fr<n2,n2>,n1,false> passed
test_can_require<ex_fq_fr<n2,n2>,n2,true> passed
test_require<ex_fq_fr<n1,n1>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n2,n2> passed
test_require<ex_fq_fr<n2,n1>,n1,n1> passed
test_require<ex_fq_fr<n2,n1>,n2,n2> passed
test_require<ex_fq_fr<n2,n2>,n2,n2> passed
test_can_prefer<ex_fq_fr<n1,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n1>,n2,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,n2,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,n2,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,n2,true> passed
test_prefer<ex_fq_fr<n1,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n1>,n2,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n2,n2> passed
test_prefer<ex_fq_fr<n2,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n2,n1>,n2,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n1,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n2,n2> passed
test_vars passed
relationship test suite ends

*** No errors detected.
outstanding_work test suite begins
test_can_query<ex_nq_nr,s,true> passed
test_can_query<ex_nq_nr,n1,true> passed
test_can_query<ex_nq_nr,n2,false> passed
test_query<ex_nq_nr,s,n1> passed
test_query<ex_nq_nr,n1,n1> passed
test_constexpr_query<ex_nq_nr,s,n1> passed
test_constexpr_query<ex_nq_nr,n1,n1> passed
test_can_require<ex_nq_nr,s,false> passed
test_can_require<ex_nq_nr,n1,true> passed
test_can_require<ex_nq_nr,n2,false> passed
test_require<ex_nq_nr,n1,n1> passed
test_can_prefer<ex_nq_nr,s,false> passed
test_can_prefer<ex_nq_nr,n1,true> passed
test_can_prefer<ex_nq_nr,n2,true> passed
test_prefer<ex_nq_nr,n1,n1> passed
test_prefer<ex_nq_nr,n2,n1> passed
test_can_query<ex_cq_nr<s,s,n1>,s,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n2>,s,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n2,true> passed
test_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_cq_nr<s,s,n1>,s,false> passed
test_can_require<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,s,n2>,s,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n2,true> passed
test_require<ex_cq_nr<s,s,n1>,n1,n1> passed
test_require<ex_cq_nr<s,s,n2>,n2,n2> passed
test_require<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_require<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_require<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_require<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_prefer<ex_cq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n2,true> passed
test_prefer<ex_cq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_can_query<ex_mq_nr<s,s,n1>,s,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n2>,s,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n2,true> passed
test_query<ex_mq_nr<s,s,n1>,s,n1> passed
test_query<ex_mq_nr<s,s,n1>,n1,n1> passed
test_query<ex_mq_nr<s,s,n1>,n2,n1> passed
test_query<ex_mq_nr<s,s,n2>,s,n2> passed
test_query<ex_mq_nr<s,s,n2>,n1,n2> passed
test_query<ex_mq_nr<s,s,n2>,n2,n2> passed
test_query<ex_mq_nr<s,n1,n1>,s,n1> passed
test_query<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_mq_nr<s,n1,n2>,s,n2> passed
test_query<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_mq_nr<s,n2,n1>,s,n1> passed
test_query<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_mq_nr<s,n2,n2>,s,n2> passed
test_query<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_mq_nr<n1,s,n1>,s,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_mq_nr<n2,s,n2>,s,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_mq_nr<s,s,n1>,s,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n2>,s,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n2,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n2,true> passed
test_prefer<ex_mq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_can_query<ex_fq_nr<s,s,n1>,s,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n2>,s,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n2,true> passed
test_query<ex_fq_nr<s,s,n1>,s,n1> passed
test_query<ex_fq_nr<s,s,n1>,n1,n1> passed
test_query<ex_fq_nr<s,s,n1>,n2,n1> passed
test_query<ex_fq_nr<s,s,n2>,s,n2> passed
test_query<ex_fq_nr<s,s,n2>,n1,n2> passed
test_query<ex_fq_nr<s,s,n2>,n2,n2> passed
test_query<ex_fq_nr<s,n1,n1>,s,n1> passed
test_query<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_fq_nr<s,n1,n2>,s,n2> passed
test_query<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_fq_nr<s,n2,n1>,s,n1> passed
test_query<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_fq_nr<s,n2,n2>,s,n2> passed
test_query<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_fq_nr<n1,s,n1>,s,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_fq_nr<n2,s,n2>,s,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_can_require<ex_fq_nr<s,s,n1>,s,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n2>,s,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n2,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n2,true> passed
test_prefer<ex_fq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_can_query<ex_mq_mr<n1,n1>,s,true> passed
test_can_query<ex_mq_mr<n1,n1>,n1,true> passed
test_can_query<ex_mq_mr<n1,n1>,n2,false> passed
test_can_query<ex_mq_mr<n1,n2>,s,true> passed
test_can_query<ex_mq_mr<n1,n2>,n1,true> passed
test_can_query<ex_mq_mr<n1,n2>,n2,true> passed
test_can_query<ex_mq_mr<n2,n1>,s,true> passed
test_can_query<ex_mq_mr<n2,n1>,n1,true> passed
test_can_query<ex_mq_mr<n2,n1>,n2,true> passed
test_can_query<ex_mq_mr<n2,n2>,s,true> passed
test_can_query<ex_mq_mr<n2,n2>,n1,false> passed
test_can_query<ex_mq_mr<n2,n2>,n2,true> passed
test_query<ex_mq_mr<n1,n1>,s,n1> passed
test_query<ex_mq_mr<n1,n1>,n1,n1> passed
test_query<ex_mq_mr<n1,n2>,s,n1> passed
test_query<ex_mq_mr<n1,n2>,n1,n1> passed
test_query<ex_mq_mr<n2,n1>,s,n2> passed
test_query<ex_mq_mr<n2,n1>,n2,n2> passed
test_query<ex_mq_mr<n2,n2>,s,n2> passed
test_query<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_require<ex_mq_mr<n1,n1>,s,false> passed
test_can_require<ex_mq_mr<n1,n1>,n1,true> passed
test_can_require<ex_mq_mr<n1,n1>,n2,false> passed
test_can_require<ex_mq_mr<n1,n2>,s,false> passed
test_can_require<ex_mq_mr<n1,n2>,n1,true> passed
test_can_require<ex_mq_mr<n1,n2>,n2,true> passed
test_can_require<ex_mq_mr<n2,n1>,s,false> passed
test_can_require<ex_mq_mr<n2,n1>,n1,true> passed
test_can_require<ex_mq_mr<n2,n1>,n2,true> passed
test_can_require<ex_mq_mr<n2,n2>,s,false> passed
test_can_require<ex_mq_mr<n2,n2>,n1,false> passed
test_can_require<ex_mq_mr<n2,n2>,n2,true> passed
test_require<ex_mq_mr<n1,n1>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n2,n2> passed
test_require<ex_mq_mr<n2,n1>,n1,n1> passed
test_require<ex_mq_mr<n2,n1>,n2,n2> passed
test_require<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_prefer<ex_mq_mr<n1,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n1>,n2,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,n2,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,n2,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,n2,true> passed
test_prefer<ex_mq_mr<n1,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n1>,n2,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n2,n2> passed
test_prefer<ex_mq_mr<n2,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n2,n1>,n2,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n1,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n2,n2> passed
test_can_query<ex_fq_fr<n1,n1>,s,true> passed
test_can_query<ex_fq_fr<n1,n1>,n1,true> passed
test_can_query<ex_fq_fr<n1,n1>,n2,false> passed
test_can_query<ex_fq_fr<n1,n2>,s,true> passed
test_can_query<ex_fq_fr<n1,n2>,n1,true> passed
test_can_query<ex_fq_fr<n1,n2>,n2,true> passed
test_can_query<ex_fq_fr<n2,n1>,s,true> passed
test_can_query<ex_fq_fr<n2,n1>,n1,true> passed
test_can_query<ex_fq_fr<n2,n1>,n2,true> passed
test_can_query<ex_fq_fr<n2,n2>,s,true> passed
test_can_query<ex_fq_fr<n2,n2>,n1,false> passed
test_can_query<ex_fq_fr<n2,n2>,n2,true> passed
test_query<ex_fq_fr<n1,n1>,s,n1> passed
test_query<ex_fq_fr<n1,n1>,n1,n1> passed
test_query<ex_fq_fr<n1,n2>,s,n1> passed
test_query<ex_fq_fr<n1,n2>,n1,n1> passed
test_query<ex_fq_fr<n2,n1>,s,n2> passed
test_query<ex_fq_fr<n2,n1>,n2,n2> passed
test_query<ex_fq_fr<n2,n2>,s,n2> passed
test_query<ex_fq_fr<n2,n2>,n2,n2> passed
test_can_require<ex_fq_fr<n1,n1>,s,false> passed
test_can_require<ex_fq_fr<n1,n1>,n1,true> passed
test_can_require<ex_fq_fr<n1,n1>,n2,false> passed
test_can_require<ex_fq_fr<n1,n2>,s,false> passed
test_can_require<ex_fq_fr<n1,n2>,n1,true> passed
test_can_require<ex_fq_fr<n1,n2>,n2,true> passed
test_can_require<ex_fq_fr<n2,n1>,s,false> passed
test_can_require<ex_fq_fr<n2,n1>,n1,true> passed
test_can_require<ex_fq_fr<n2,n1>,n2,true> passed
test_can_require<ex_fq_fr<n2,n2>,s,false> passed
test_can_require<ex_fq_fr<n2,n2>,n1,false> passed
test_can_require<ex_fq_fr<n2,n2>,n2,true> passed
test_require<ex_fq_fr<n1,n1>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n2,n2> passed
test_require<ex_fq_fr<n2,n1>,n1,n1> passed
test_require<ex_fq_fr<n2,n1>,n2,n2> passed
test_require<ex_fq_fr<n2,n2>,n2,n2> passed
test_can_prefer<ex_fq_fr<n1,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n1>,n2,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,n2,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,n2,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,n2,true> passed
test_prefer<ex_fq_fr<n1,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n1>,n2,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n2,n2> passed
test_prefer<ex_fq_fr<n2,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n2,n1>,n2,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n1,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n2,n2> passed
test_vars passed
outstanding_work test suite ends

*** No errors detected.
mapping test suite begins
test_can_query<ex_nq_nr,s,true> passed
test_can_query<ex_nq_nr,n1,true> passed
test_can_query<ex_nq_nr,n2,false> passed
test_can_query<ex_nq_nr,n3,false> passed
test_query<ex_nq_nr,s,n1> passed
test_query<ex_nq_nr,n1,n1> passed
test_constexpr_query<ex_nq_nr,s,n1> passed
test_constexpr_query<ex_nq_nr,n1,n1> passed
test_can_require<ex_nq_nr,s,false> passed
test_can_require<ex_nq_nr,n1,true> passed
test_can_require<ex_nq_nr,n2,false> passed
test_can_require<ex_nq_nr,n3,false> passed
test_require<ex_nq_nr,n1,n1> passed
test_can_prefer<ex_nq_nr,s,false> passed
test_can_prefer<ex_nq_nr,n1,true> passed
test_can_prefer<ex_nq_nr,n2,true> passed
test_can_prefer<ex_nq_nr,n3,true> passed
test_prefer<ex_nq_nr,n1,n1> passed
test_prefer<ex_nq_nr,n2,n1> passed
test_prefer<ex_nq_nr,n3,n1> passed
test_can_query<ex_cq_nr<s,s,n1>,s,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n1>,n3,true> passed
test_can_query<ex_cq_nr<s,s,n2>,s,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n2>,n3,true> passed
test_can_query<ex_cq_nr<s,s,n3>,s,true> passed
test_can_query<ex_cq_nr<s,s,n3>,n1,true> passed
test_can_query<ex_cq_nr<s,s,n3>,n2,true> passed
test_can_query<ex_cq_nr<s,s,n3>,n3,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n1>,n3,false> passed
test_can_query<ex_cq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n2>,n3,false> passed
test_can_query<ex_cq_nr<s,n1,n3>,s,true> passed
test_can_query<ex_cq_nr<s,n1,n3>,n1,true> passed
test_can_query<ex_cq_nr<s,n1,n3>,n2,false> passed
test_can_query<ex_cq_nr<s,n1,n3>,n3,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n1>,n3,false> passed
test_can_query<ex_cq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n2>,n3,false> passed
test_can_query<ex_cq_nr<s,n2,n3>,s,true> passed
test_can_query<ex_cq_nr<s,n2,n3>,n1,false> passed
test_can_query<ex_cq_nr<s,n2,n3>,n2,true> passed
test_can_query<ex_cq_nr<s,n2,n3>,n3,false> passed
test_can_query<ex_cq_nr<s,n3,n1>,s,true> passed
test_can_query<ex_cq_nr<s,n3,n1>,n1,false> passed
test_can_query<ex_cq_nr<s,n3,n1>,n2,false> passed
test_can_query<ex_cq_nr<s,n3,n1>,n3,true> passed
test_can_query<ex_cq_nr<s,n3,n2>,s,true> passed
test_can_query<ex_cq_nr<s,n3,n2>,n1,false> passed
test_can_query<ex_cq_nr<s,n3,n2>,n2,false> passed
test_can_query<ex_cq_nr<s,n3,n2>,n3,true> passed
test_can_query<ex_cq_nr<s,n3,n3>,s,true> passed
test_can_query<ex_cq_nr<s,n3,n3>,n1,false> passed
test_can_query<ex_cq_nr<s,n3,n3>,n2,false> passed
test_can_query<ex_cq_nr<s,n3,n3>,n3,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_cq_nr<n1,s,n1>,n3,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n2,true> passed
test_can_query<ex_cq_nr<n2,s,n2>,n3,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,s,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,n1,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,n2,true> passed
test_can_query<ex_cq_nr<n3,s,n3>,n3,true> passed
test_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_query<ex_cq_nr<s,s,n1>,n3,n1> passed
test_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_query<ex_cq_nr<s,s,n2>,n3,n2> passed
test_query<ex_cq_nr<s,s,n3>,s,n3> passed
test_query<ex_cq_nr<s,s,n3>,n1,n3> passed
test_query<ex_cq_nr<s,s,n3>,n2,n3> passed
test_query<ex_cq_nr<s,s,n3>,n3,n3> passed
test_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_cq_nr<s,n1,n3>,s,n3> passed
test_query<ex_cq_nr<s,n1,n3>,n1,n3> passed
test_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_cq_nr<s,n2,n3>,s,n3> passed
test_query<ex_cq_nr<s,n2,n3>,n2,n3> passed
test_query<ex_cq_nr<s,n3,n1>,s,n1> passed
test_query<ex_cq_nr<s,n3,n1>,n3,n1> passed
test_query<ex_cq_nr<s,n3,n2>,s,n2> passed
test_query<ex_cq_nr<s,n3,n2>,n3,n2> passed
test_query<ex_cq_nr<s,n3,n3>,s,n3> passed
test_query<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_cq_nr<n1,s,n1>,n3,n1> passed
test_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_query<ex_cq_nr<n2,s,n2>,n3,n2> passed
test_query<ex_cq_nr<n3,s,n3>,s,n3> passed
test_query<ex_cq_nr<n3,s,n3>,n1,n3> passed
test_query<ex_cq_nr<n3,s,n3>,n2,n3> passed
test_query<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n1>,n3,n1> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n2>,n3,n2> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,n1,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,n2,n3> passed
test_constexpr_query<ex_cq_nr<s,s,n3>,n3,n3> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<s,n1,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,n1,n3>,n1,n3> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<s,n2,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,n2,n3>,n2,n3> passed
test_constexpr_query<ex_cq_nr<s,n3,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<s,n3,n1>,n3,n1> passed
test_constexpr_query<ex_cq_nr<s,n3,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<s,n3,n2>,n3,n2> passed
test_constexpr_query<ex_cq_nr<s,n3,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,s,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_constexpr_query<ex_cq_nr<n1,s,n1>,n3,n1> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,s,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_constexpr_query<ex_cq_nr<n2,s,n2>,n3,n2> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,s,n3> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,n1,n3> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,n2,n3> passed
test_constexpr_query<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_can_require<ex_cq_nr<s,s,n1>,s,false> passed
test_can_require<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,s,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,s,n2>,s,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,s,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,s,n3>,s,false> passed
test_can_require<ex_cq_nr<s,s,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,s,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,s,n3>,n3,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_require<ex_cq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,s,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,n1,n3>,n3,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_require<ex_cq_nr<s,n2,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,s,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,n2,n3>,n3,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,s,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,n1,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,n2,false> passed
test_can_require<ex_cq_nr<s,n3,n1>,n3,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,s,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,n1,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,n2,false> passed
test_can_require<ex_cq_nr<s,n3,n2>,n3,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,s,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,n1,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,n2,false> passed
test_can_require<ex_cq_nr<s,n3,n3>,n3,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_require<ex_cq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_cq_nr<n1,s,n1>,n3,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_cq_nr<n2,s,n2>,n2,true> passed
test_can_require<ex_cq_nr<n2,s,n2>,n3,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,s,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,n1,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,n2,false> passed
test_can_require<ex_cq_nr<n3,s,n3>,n3,true> passed
test_require<ex_cq_nr<s,s,n1>,n1,n1> passed
test_require<ex_cq_nr<s,s,n2>,n2,n2> passed
test_require<ex_cq_nr<s,s,n3>,n3,n3> passed
test_require<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_require<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_require<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_require<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_require<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_require<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_can_prefer<ex_cq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,s,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,s,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,s,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,s,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,s,n3>,n2,true> passed
test_can_prefer<ex_cq_nr<s,s,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n1,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n1,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n1,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n2,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n2,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n2,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,s,false> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n3,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,s,false> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n3,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,s,false> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,n2,true> passed
test_can_prefer<ex_cq_nr<s,n3,n3>,n3,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_cq_nr<n1,s,n1>,n3,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n2,true> passed
test_can_prefer<ex_cq_nr<n2,s,n2>,n3,true> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,s,false> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,n1,true> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,n2,true> passed
test_can_prefer<ex_cq_nr<n3,s,n3>,n3,true> passed
test_prefer<ex_cq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,s,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,s,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,s,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,s,n3>,n2,n3> passed
test_prefer<ex_cq_nr<s,s,n3>,n3,n3> passed
test_prefer<ex_cq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,n1,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,n1,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,n1,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,n1,n3>,n2,n3> passed
test_prefer<ex_cq_nr<s,n1,n3>,n3,n3> passed
test_prefer<ex_cq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,n2,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,n2,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,n2,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,n2,n3>,n2,n3> passed
test_prefer<ex_cq_nr<s,n2,n3>,n3,n3> passed
test_prefer<ex_cq_nr<s,n3,n1>,n1,n1> passed
test_prefer<ex_cq_nr<s,n3,n1>,n2,n1> passed
test_prefer<ex_cq_nr<s,n3,n1>,n3,n1> passed
test_prefer<ex_cq_nr<s,n3,n2>,n1,n2> passed
test_prefer<ex_cq_nr<s,n3,n2>,n2,n2> passed
test_prefer<ex_cq_nr<s,n3,n2>,n3,n2> passed
test_prefer<ex_cq_nr<s,n3,n3>,n1,n3> passed
test_prefer<ex_cq_nr<s,n3,n3>,n2,n3> passed
test_prefer<ex_cq_nr<s,n3,n3>,n3,n3> passed
test_prefer<ex_cq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_cq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_cq_nr<n1,s,n1>,n3,n1> passed
test_prefer<ex_cq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_cq_nr<n2,s,n2>,n2,n2> passed
test_prefer<ex_cq_nr<n2,s,n2>,n3,n2> passed
test_prefer<ex_cq_nr<n3,s,n3>,n1,n3> passed
test_prefer<ex_cq_nr<n3,s,n3>,n2,n3> passed
test_prefer<ex_cq_nr<n3,s,n3>,n3,n3> passed
test_can_query<ex_mq_nr<s,s,n1>,s,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n1>,n3,true> passed
test_can_query<ex_mq_nr<s,s,n2>,s,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n2>,n3,true> passed
test_can_query<ex_mq_nr<s,s,n3>,s,true> passed
test_can_query<ex_mq_nr<s,s,n3>,n1,true> passed
test_can_query<ex_mq_nr<s,s,n3>,n2,true> passed
test_can_query<ex_mq_nr<s,s,n3>,n3,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n1>,n3,false> passed
test_can_query<ex_mq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n2>,n3,false> passed
test_can_query<ex_mq_nr<s,n1,n3>,s,true> passed
test_can_query<ex_mq_nr<s,n1,n3>,n1,true> passed
test_can_query<ex_mq_nr<s,n1,n3>,n2,false> passed
test_can_query<ex_mq_nr<s,n1,n3>,n3,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n1>,n3,false> passed
test_can_query<ex_mq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n2>,n3,false> passed
test_can_query<ex_mq_nr<s,n2,n3>,s,true> passed
test_can_query<ex_mq_nr<s,n2,n3>,n1,false> passed
test_can_query<ex_mq_nr<s,n2,n3>,n2,true> passed
test_can_query<ex_mq_nr<s,n2,n3>,n3,false> passed
test_can_query<ex_mq_nr<s,n3,n1>,s,true> passed
test_can_query<ex_mq_nr<s,n3,n1>,n1,false> passed
test_can_query<ex_mq_nr<s,n3,n1>,n2,false> passed
test_can_query<ex_mq_nr<s,n3,n1>,n3,true> passed
test_can_query<ex_mq_nr<s,n3,n2>,s,true> passed
test_can_query<ex_mq_nr<s,n3,n2>,n1,false> passed
test_can_query<ex_mq_nr<s,n3,n2>,n2,false> passed
test_can_query<ex_mq_nr<s,n3,n2>,n3,true> passed
test_can_query<ex_mq_nr<s,n3,n3>,s,true> passed
test_can_query<ex_mq_nr<s,n3,n3>,n1,false> passed
test_can_query<ex_mq_nr<s,n3,n3>,n2,false> passed
test_can_query<ex_mq_nr<s,n3,n3>,n3,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_mq_nr<n1,s,n1>,n3,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n2,true> passed
test_can_query<ex_mq_nr<n2,s,n2>,n3,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,s,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,n1,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,n2,true> passed
test_can_query<ex_mq_nr<n3,s,n3>,n3,true> passed
test_query<ex_mq_nr<s,s,n1>,s,n1> passed
test_query<ex_mq_nr<s,s,n1>,n1,n1> passed
test_query<ex_mq_nr<s,s,n1>,n2,n1> passed
test_query<ex_mq_nr<s,s,n1>,n3,n1> passed
test_query<ex_mq_nr<s,s,n2>,s,n2> passed
test_query<ex_mq_nr<s,s,n2>,n1,n2> passed
test_query<ex_mq_nr<s,s,n2>,n2,n2> passed
test_query<ex_mq_nr<s,s,n2>,n3,n2> passed
test_query<ex_mq_nr<s,s,n3>,s,n3> passed
test_query<ex_mq_nr<s,s,n3>,n1,n3> passed
test_query<ex_mq_nr<s,s,n3>,n2,n3> passed
test_query<ex_mq_nr<s,s,n3>,n3,n3> passed
test_query<ex_mq_nr<s,n1,n1>,s,n1> passed
test_query<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_mq_nr<s,n1,n2>,s,n2> passed
test_query<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_mq_nr<s,n1,n3>,s,n3> passed
test_query<ex_mq_nr<s,n1,n3>,n1,n3> passed
test_query<ex_mq_nr<s,n2,n1>,s,n1> passed
test_query<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_mq_nr<s,n2,n2>,s,n2> passed
test_query<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_mq_nr<s,n2,n3>,s,n3> passed
test_query<ex_mq_nr<s,n2,n3>,n2,n3> passed
test_query<ex_mq_nr<s,n3,n1>,s,n1> passed
test_query<ex_mq_nr<s,n3,n1>,n3,n1> passed
test_query<ex_mq_nr<s,n3,n2>,s,n2> passed
test_query<ex_mq_nr<s,n3,n2>,n3,n2> passed
test_query<ex_mq_nr<s,n3,n3>,s,n3> passed
test_query<ex_mq_nr<s,n3,n3>,n3,n3> passed
test_query<ex_mq_nr<n1,s,n1>,s,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_mq_nr<n1,s,n1>,n3,n1> passed
test_query<ex_mq_nr<n2,s,n2>,s,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_query<ex_mq_nr<n2,s,n2>,n3,n2> passed
test_query<ex_mq_nr<n3,s,n3>,s,n3> passed
test_query<ex_mq_nr<n3,s,n3>,n1,n3> passed
test_query<ex_mq_nr<n3,s,n3>,n2,n3> passed
test_query<ex_mq_nr<n3,s,n3>,n3,n3> passed
test_can_require<ex_mq_nr<s,s,n1>,s,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,s,n2>,s,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,s,n3>,s,false> passed
test_can_require<ex_mq_nr<s,s,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,s,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,s,n3>,n3,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,s,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,n1,n3>,n3,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,s,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,n2,n3>,n3,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,s,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,n1,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,n2,false> passed
test_can_require<ex_mq_nr<s,n3,n1>,n3,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,s,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,n1,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,n2,false> passed
test_can_require<ex_mq_nr<s,n3,n2>,n3,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,s,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,n1,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,n2,false> passed
test_can_require<ex_mq_nr<s,n3,n3>,n3,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_mq_nr<n1,s,n1>,n3,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n2,false> passed
test_can_require<ex_mq_nr<n2,s,n2>,n3,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,s,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,n1,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,n2,false> passed
test_can_require<ex_mq_nr<n3,s,n3>,n3,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,s,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,s,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,s,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,s,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,s,n3>,n2,true> passed
test_can_prefer<ex_mq_nr<s,s,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n1,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n1,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n1,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n2,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n2,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n2,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,s,false> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n3,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,s,false> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n3,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,s,false> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,n2,true> passed
test_can_prefer<ex_mq_nr<s,n3,n3>,n3,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_mq_nr<n1,s,n1>,n3,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n2,true> passed
test_can_prefer<ex_mq_nr<n2,s,n2>,n3,true> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,s,false> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,n1,true> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,n2,true> passed
test_can_prefer<ex_mq_nr<n3,s,n3>,n3,true> passed
test_prefer<ex_mq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,s,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,s,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,s,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,s,n3>,n2,n3> passed
test_prefer<ex_mq_nr<s,s,n3>,n3,n3> passed
test_prefer<ex_mq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,n1,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,n1,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,n1,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,n1,n3>,n2,n3> passed
test_prefer<ex_mq_nr<s,n1,n3>,n3,n3> passed
test_prefer<ex_mq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,n2,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,n2,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,n2,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,n2,n3>,n2,n3> passed
test_prefer<ex_mq_nr<s,n2,n3>,n3,n3> passed
test_prefer<ex_mq_nr<s,n3,n1>,n1,n1> passed
test_prefer<ex_mq_nr<s,n3,n1>,n2,n1> passed
test_prefer<ex_mq_nr<s,n3,n1>,n3,n1> passed
test_prefer<ex_mq_nr<s,n3,n2>,n1,n2> passed
test_prefer<ex_mq_nr<s,n3,n2>,n2,n2> passed
test_prefer<ex_mq_nr<s,n3,n2>,n3,n2> passed
test_prefer<ex_mq_nr<s,n3,n3>,n1,n3> passed
test_prefer<ex_mq_nr<s,n3,n3>,n2,n3> passed
test_prefer<ex_mq_nr<s,n3,n3>,n3,n3> passed
test_prefer<ex_mq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_mq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_mq_nr<n1,s,n1>,n3,n1> passed
test_prefer<ex_mq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_mq_nr<n2,s,n2>,n2,n2> passed
test_prefer<ex_mq_nr<n2,s,n2>,n3,n2> passed
test_prefer<ex_mq_nr<n3,s,n3>,n1,n3> passed
test_prefer<ex_mq_nr<n3,s,n3>,n2,n3> passed
test_prefer<ex_mq_nr<n3,s,n3>,n3,n3> passed
test_can_query<ex_fq_nr<s,s,n1>,s,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n1>,n3,true> passed
test_can_query<ex_fq_nr<s,s,n2>,s,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n2>,n3,true> passed
test_can_query<ex_fq_nr<s,s,n3>,s,true> passed
test_can_query<ex_fq_nr<s,s,n3>,n1,true> passed
test_can_query<ex_fq_nr<s,s,n3>,n2,true> passed
test_can_query<ex_fq_nr<s,s,n3>,n3,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n1>,n3,false> passed
test_can_query<ex_fq_nr<s,n1,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n2>,n3,false> passed
test_can_query<ex_fq_nr<s,n1,n3>,s,true> passed
test_can_query<ex_fq_nr<s,n1,n3>,n1,true> passed
test_can_query<ex_fq_nr<s,n1,n3>,n2,false> passed
test_can_query<ex_fq_nr<s,n1,n3>,n3,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n1>,n3,false> passed
test_can_query<ex_fq_nr<s,n2,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n2>,n3,false> passed
test_can_query<ex_fq_nr<s,n2,n3>,s,true> passed
test_can_query<ex_fq_nr<s,n2,n3>,n1,false> passed
test_can_query<ex_fq_nr<s,n2,n3>,n2,true> passed
test_can_query<ex_fq_nr<s,n2,n3>,n3,false> passed
test_can_query<ex_fq_nr<s,n3,n1>,s,true> passed
test_can_query<ex_fq_nr<s,n3,n1>,n1,false> passed
test_can_query<ex_fq_nr<s,n3,n1>,n2,false> passed
test_can_query<ex_fq_nr<s,n3,n1>,n3,true> passed
test_can_query<ex_fq_nr<s,n3,n2>,s,true> passed
test_can_query<ex_fq_nr<s,n3,n2>,n1,false> passed
test_can_query<ex_fq_nr<s,n3,n2>,n2,false> passed
test_can_query<ex_fq_nr<s,n3,n2>,n3,true> passed
test_can_query<ex_fq_nr<s,n3,n3>,s,true> passed
test_can_query<ex_fq_nr<s,n3,n3>,n1,false> passed
test_can_query<ex_fq_nr<s,n3,n3>,n2,false> passed
test_can_query<ex_fq_nr<s,n3,n3>,n3,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,s,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_query<ex_fq_nr<n1,s,n1>,n3,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,s,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n2,true> passed
test_can_query<ex_fq_nr<n2,s,n2>,n3,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,s,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,n1,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,n2,true> passed
test_can_query<ex_fq_nr<n3,s,n3>,n3,true> passed
test_query<ex_fq_nr<s,s,n1>,s,n1> passed
test_query<ex_fq_nr<s,s,n1>,n1,n1> passed
test_query<ex_fq_nr<s,s,n1>,n2,n1> passed
test_query<ex_fq_nr<s,s,n1>,n3,n1> passed
test_query<ex_fq_nr<s,s,n2>,s,n2> passed
test_query<ex_fq_nr<s,s,n2>,n1,n2> passed
test_query<ex_fq_nr<s,s,n2>,n2,n2> passed
test_query<ex_fq_nr<s,s,n2>,n3,n2> passed
test_query<ex_fq_nr<s,s,n3>,s,n3> passed
test_query<ex_fq_nr<s,s,n3>,n1,n3> passed
test_query<ex_fq_nr<s,s,n3>,n2,n3> passed
test_query<ex_fq_nr<s,s,n3>,n3,n3> passed
test_query<ex_fq_nr<s,n1,n1>,s,n1> passed
test_query<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_query<ex_fq_nr<s,n1,n2>,s,n2> passed
test_query<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_query<ex_fq_nr<s,n1,n3>,s,n3> passed
test_query<ex_fq_nr<s,n1,n3>,n1,n3> passed
test_query<ex_fq_nr<s,n2,n1>,s,n1> passed
test_query<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_query<ex_fq_nr<s,n2,n2>,s,n2> passed
test_query<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_query<ex_fq_nr<s,n2,n3>,s,n3> passed
test_query<ex_fq_nr<s,n2,n3>,n2,n3> passed
test_query<ex_fq_nr<s,n3,n1>,s,n1> passed
test_query<ex_fq_nr<s,n3,n1>,n3,n1> passed
test_query<ex_fq_nr<s,n3,n2>,s,n2> passed
test_query<ex_fq_nr<s,n3,n2>,n3,n2> passed
test_query<ex_fq_nr<s,n3,n3>,s,n3> passed
test_query<ex_fq_nr<s,n3,n3>,n3,n3> passed
test_query<ex_fq_nr<n1,s,n1>,s,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_query<ex_fq_nr<n1,s,n1>,n3,n1> passed
test_query<ex_fq_nr<n2,s,n2>,s,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_query<ex_fq_nr<n2,s,n2>,n3,n2> passed
test_query<ex_fq_nr<n3,s,n3>,s,n3> passed
test_query<ex_fq_nr<n3,s,n3>,n1,n3> passed
test_query<ex_fq_nr<n3,s,n3>,n2,n3> passed
test_query<ex_fq_nr<n3,s,n3>,n3,n3> passed
test_can_require<ex_fq_nr<s,s,n1>,s,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,s,n2>,s,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,s,n3>,s,false> passed
test_can_require<ex_fq_nr<s,s,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,s,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,s,n3>,n3,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,s,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,n1,n3>,n3,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,s,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,n2,n3>,n3,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,s,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,n1,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,n2,false> passed
test_can_require<ex_fq_nr<s,n3,n1>,n3,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,s,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,n1,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,n2,false> passed
test_can_require<ex_fq_nr<s,n3,n2>,n3,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,s,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,n1,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,n2,false> passed
test_can_require<ex_fq_nr<s,n3,n3>,n3,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n1,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n2,false> passed
test_can_require<ex_fq_nr<n1,s,n1>,n3,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n1,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n2,false> passed
test_can_require<ex_fq_nr<n2,s,n2>,n3,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,s,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,n1,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,n2,false> passed
test_can_require<ex_fq_nr<n3,s,n3>,n3,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,s,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,s,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,s,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,s,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,s,n3>,n2,true> passed
test_can_prefer<ex_fq_nr<s,s,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n1,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n1,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n1,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n2,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n2,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n2,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,s,false> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n3,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,s,false> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n3,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,s,false> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,n2,true> passed
test_can_prefer<ex_fq_nr<s,n3,n3>,n3,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,s,false> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n1,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n2,true> passed
test_can_prefer<ex_fq_nr<n1,s,n1>,n3,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,s,false> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n1,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n2,true> passed
test_can_prefer<ex_fq_nr<n2,s,n2>,n3,true> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,s,false> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,n1,true> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,n2,true> passed
test_can_prefer<ex_fq_nr<n3,s,n3>,n3,true> passed
test_prefer<ex_fq_nr<s,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,s,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,s,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,s,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,s,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,s,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,s,n3>,n2,n3> passed
test_prefer<ex_fq_nr<s,s,n3>,n3,n3> passed
test_prefer<ex_fq_nr<s,n1,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n1,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,n1,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,n1,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n1,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,n1,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,n1,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,n1,n3>,n2,n3> passed
test_prefer<ex_fq_nr<s,n1,n3>,n3,n3> passed
test_prefer<ex_fq_nr<s,n2,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n2,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,n2,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,n2,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n2,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,n2,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,n2,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,n2,n3>,n2,n3> passed
test_prefer<ex_fq_nr<s,n2,n3>,n3,n3> passed
test_prefer<ex_fq_nr<s,n3,n1>,n1,n1> passed
test_prefer<ex_fq_nr<s,n3,n1>,n2,n1> passed
test_prefer<ex_fq_nr<s,n3,n1>,n3,n1> passed
test_prefer<ex_fq_nr<s,n3,n2>,n1,n2> passed
test_prefer<ex_fq_nr<s,n3,n2>,n2,n2> passed
test_prefer<ex_fq_nr<s,n3,n2>,n3,n2> passed
test_prefer<ex_fq_nr<s,n3,n3>,n1,n3> passed
test_prefer<ex_fq_nr<s,n3,n3>,n2,n3> passed
test_prefer<ex_fq_nr<s,n3,n3>,n3,n3> passed
test_prefer<ex_fq_nr<n1,s,n1>,n1,n1> passed
test_prefer<ex_fq_nr<n1,s,n1>,n2,n1> passed
test_prefer<ex_fq_nr<n1,s,n1>,n3,n1> passed
test_prefer<ex_fq_nr<n2,s,n2>,n1,n2> passed
test_prefer<ex_fq_nr<n2,s,n2>,n2,n2> passed
test_prefer<ex_fq_nr<n2,s,n2>,n3,n2> passed
test_prefer<ex_fq_nr<n3,s,n3>,n1,n3> passed
test_prefer<ex_fq_nr<n3,s,n3>,n2,n3> passed
test_prefer<ex_fq_nr<n3,s,n3>,n3,n3> passed
test_can_query<ex_mq_mr<n1,n1>,s,true> passed
test_can_query<ex_mq_mr<n1,n1>,n1,true> passed
test_can_query<ex_mq_mr<n1,n1>,n2,false> passed
test_can_query<ex_mq_mr<n1,n1>,n3,false> passed
test_can_query<ex_mq_mr<n1,n2>,s,true> passed
test_can_query<ex_mq_mr<n1,n2>,n1,true> passed
test_can_query<ex_mq_mr<n1,n2>,n2,true> passed
test_can_query<ex_mq_mr<n1,n2>,n3,false> passed
test_can_query<ex_mq_mr<n1,n3>,s,true> passed
test_can_query<ex_mq_mr<n1,n3>,n1,true> passed
test_can_query<ex_mq_mr<n1,n3>,n2,false> passed
test_can_query<ex_mq_mr<n1,n3>,n3,true> passed
test_can_query<ex_mq_mr<n2,n1>,s,true> passed
test_can_query<ex_mq_mr<n2,n1>,n1,true> passed
test_can_query<ex_mq_mr<n2,n1>,n2,true> passed
test_can_query<ex_mq_mr<n2,n1>,n3,false> passed
test_can_query<ex_mq_mr<n2,n2>,s,true> passed
test_can_query<ex_mq_mr<n2,n2>,n1,false> passed
test_can_query<ex_mq_mr<n2,n2>,n2,true> passed
test_can_query<ex_mq_mr<n2,n2>,n3,false> passed
test_can_query<ex_mq_mr<n2,n3>,s,true> passed
test_can_query<ex_mq_mr<n2,n3>,n1,false> passed
test_can_query<ex_mq_mr<n2,n3>,n2,true> passed
test_can_query<ex_mq_mr<n2,n3>,n3,true> passed
test_can_query<ex_mq_mr<n3,n1>,s,true> passed
test_can_query<ex_mq_mr<n3,n1>,n1,true> passed
test_can_query<ex_mq_mr<n3,n1>,n2,false> passed
test_can_query<ex_mq_mr<n3,n1>,n3,true> passed
test_can_query<ex_mq_mr<n3,n2>,s,true> passed
test_can_query<ex_mq_mr<n3,n2>,n1,false> passed
test_can_query<ex_mq_mr<n3,n2>,n2,true> passed
test_can_query<ex_mq_mr<n3,n2>,n3,true> passed
test_can_query<ex_mq_mr<n3,n3>,s,true> passed
test_can_query<ex_mq_mr<n3,n3>,n1,false> passed
test_can_query<ex_mq_mr<n3,n3>,n2,false> passed
test_can_query<ex_mq_mr<n3,n3>,n3,true> passed
test_query<ex_mq_mr<n1,n1>,s,n1> passed
test_query<ex_mq_mr<n1,n1>,n1,n1> passed
test_query<ex_mq_mr<n1,n2>,s,n1> passed
test_query<ex_mq_mr<n1,n2>,n1,n1> passed
test_query<ex_mq_mr<n1,n3>,s,n1> passed
test_query<ex_mq_mr<n1,n3>,n1,n1> passed
test_query<ex_mq_mr<n2,n1>,s,n2> passed
test_query<ex_mq_mr<n2,n1>,n2,n2> passed
test_query<ex_mq_mr<n2,n2>,s,n2> passed
test_query<ex_mq_mr<n2,n2>,n2,n2> passed
test_query<ex_mq_mr<n2,n3>,s,n2> passed
test_query<ex_mq_mr<n2,n3>,n2,n2> passed
test_query<ex_mq_mr<n3,n1>,s,n3> passed
test_query<ex_mq_mr<n3,n1>,n3,n3> passed
test_query<ex_mq_mr<n3,n2>,s,n3> passed
test_query<ex_mq_mr<n3,n2>,n3,n3> passed
test_query<ex_mq_mr<n3,n3>,s,n3> passed
test_query<ex_mq_mr<n3,n3>,n3,n3> passed
test_can_require<ex_mq_mr<n1,n1>,s,false> passed
test_can_require<ex_mq_mr<n1,n1>,n1,true> passed
test_can_require<ex_mq_mr<n1,n1>,n2,false> passed
test_can_require<ex_mq_mr<n1,n1>,n3,false> passed
test_can_require<ex_mq_mr<n1,n2>,s,false> passed
test_can_require<ex_mq_mr<n1,n2>,n1,true> passed
test_can_require<ex_mq_mr<n1,n2>,n2,true> passed
test_can_require<ex_mq_mr<n1,n2>,n3,false> passed
test_can_require<ex_mq_mr<n1,n3>,s,false> passed
test_can_require<ex_mq_mr<n1,n3>,n1,true> passed
test_can_require<ex_mq_mr<n1,n3>,n2,false> passed
test_can_require<ex_mq_mr<n1,n3>,n3,true> passed
test_can_require<ex_mq_mr<n2,n1>,s,false> passed
test_can_require<ex_mq_mr<n2,n1>,n1,true> passed
test_can_require<ex_mq_mr<n2,n1>,n2,true> passed
test_can_require<ex_mq_mr<n2,n1>,n3,false> passed
test_can_require<ex_mq_mr<n2,n2>,s,false> passed
test_can_require<ex_mq_mr<n2,n2>,n1,false> passed
test_can_require<ex_mq_mr<n2,n2>,n2,true> passed
test_can_require<ex_mq_mr<n2,n2>,n3,false> passed
test_can_require<ex_mq_mr<n2,n3>,s,false> passed
test_can_require<ex_mq_mr<n2,n3>,n1,false> passed
test_can_require<ex_mq_mr<n2,n3>,n2,true> passed
test_can_require<ex_mq_mr<n2,n3>,n3,true> passed
test_can_require<ex_mq_mr<n3,n1>,s,false> passed
test_can_require<ex_mq_mr<n3,n1>,n1,true> passed
test_can_require<ex_mq_mr<n3,n1>,n2,false> passed
test_can_require<ex_mq_mr<n3,n1>,n3,true> passed
test_can_require<ex_mq_mr<n3,n2>,s,false> passed
test_can_require<ex_mq_mr<n3,n2>,n1,false> passed
test_can_require<ex_mq_mr<n3,n2>,n2,true> passed
test_can_require<ex_mq_mr<n3,n2>,n3,true> passed
test_can_require<ex_mq_mr<n3,n3>,s,false> passed
test_can_require<ex_mq_mr<n3,n3>,n1,false> passed
test_can_require<ex_mq_mr<n3,n3>,n2,false> passed
test_can_require<ex_mq_mr<n3,n3>,n3,true> passed
test_require<ex_mq_mr<n1,n1>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n1,n1> passed
test_require<ex_mq_mr<n1,n2>,n2,n2> passed
test_require<ex_mq_mr<n1,n3>,n1,n1> passed
test_require<ex_mq_mr<n1,n3>,n3,n3> passed
test_require<ex_mq_mr<n2,n1>,n1,n1> passed
test_require<ex_mq_mr<n2,n1>,n2,n2> passed
test_require<ex_mq_mr<n2,n2>,n2,n2> passed
test_require<ex_mq_mr<n2,n3>,n2,n2> passed
test_require<ex_mq_mr<n2,n3>,n3,n3> passed
test_require<ex_mq_mr<n3,n1>,n1,n1> passed
test_require<ex_mq_mr<n3,n1>,n3,n3> passed
test_require<ex_mq_mr<n3,n2>,n2,n2> passed
test_require<ex_mq_mr<n3,n2>,n3,n3> passed
test_require<ex_mq_mr<n3,n3>,n3,n3> passed
test_can_prefer<ex_mq_mr<n1,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n1>,n2,true> passed
test_can_prefer<ex_mq_mr<n1,n1>,n3,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,n2,true> passed
test_can_prefer<ex_mq_mr<n1,n2>,n3,true> passed
test_can_prefer<ex_mq_mr<n1,n3>,s,false> passed
test_can_prefer<ex_mq_mr<n1,n3>,n1,true> passed
test_can_prefer<ex_mq_mr<n1,n3>,n2,true> passed
test_can_prefer<ex_mq_mr<n1,n3>,n3,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,n2,true> passed
test_can_prefer<ex_mq_mr<n2,n1>,n3,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,n2,true> passed
test_can_prefer<ex_mq_mr<n2,n2>,n3,true> passed
test_can_prefer<ex_mq_mr<n2,n3>,s,false> passed
test_can_prefer<ex_mq_mr<n2,n3>,n1,true> passed
test_can_prefer<ex_mq_mr<n2,n3>,n2,true> passed
test_can_prefer<ex_mq_mr<n2,n3>,n3,true> passed
test_can_prefer<ex_mq_mr<n3,n1>,s,false> passed
test_can_prefer<ex_mq_mr<n3,n1>,n1,true> passed
test_can_prefer<ex_mq_mr<n3,n1>,n2,true> passed
test_can_prefer<ex_mq_mr<n3,n1>,n3,true> passed
test_can_prefer<ex_mq_mr<n3,n2>,s,false> passed
test_can_prefer<ex_mq_mr<n3,n2>,n1,true> passed
test_can_prefer<ex_mq_mr<n3,n2>,n2,true> passed
test_can_prefer<ex_mq_mr<n3,n2>,n3,true> passed
test_can_prefer<ex_mq_mr<n3,n3>,s,false> passed
test_can_prefer<ex_mq_mr<n3,n3>,n1,true> passed
test_can_prefer<ex_mq_mr<n3,n3>,n2,true> passed
test_can_prefer<ex_mq_mr<n3,n3>,n3,true> passed
test_prefer<ex_mq_mr<n1,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n1>,n2,n1> passed
test_prefer<ex_mq_mr<n1,n1>,n3,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n2>,n2,n2> passed
test_prefer<ex_mq_mr<n1,n2>,n3,n1> passed
test_prefer<ex_mq_mr<n1,n3>,n1,n1> passed
test_prefer<ex_mq_mr<n1,n3>,n2,n1> passed
test_prefer<ex_mq_mr<n1,n3>,n3,n3> passed
test_prefer<ex_mq_mr<n2,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n2,n1>,n2,n2> passed
test_prefer<ex_mq_mr<n2,n1>,n3,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n1,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n2,n2> passed
test_prefer<ex_mq_mr<n2,n2>,n3,n2> passed
test_prefer<ex_mq_mr<n2,n3>,n1,n2> passed
test_prefer<ex_mq_mr<n2,n3>,n2,n2> passed
test_prefer<ex_mq_mr<n2,n3>,n3,n3> passed
test_prefer<ex_mq_mr<n3,n1>,n1,n1> passed
test_prefer<ex_mq_mr<n3,n1>,n2,n3> passed
test_prefer<ex_mq_mr<n3,n1>,n3,n3> passed
test_prefer<ex_mq_mr<n3,n2>,n1,n3> passed
test_prefer<ex_mq_mr<n3,n2>,n2,n2> passed
test_prefer<ex_mq_mr<n3,n2>,n3,n3> passed
test_prefer<ex_mq_mr<n3,n3>,n1,n3> passed
test_prefer<ex_mq_mr<n3,n3>,n2,n3> passed
test_prefer<ex_mq_mr<n3,n3>,n3,n3> passed
test_can_query<ex_fq_fr<n1,n1>,s,true> passed
test_can_query<ex_fq_fr<n1,n1>,n1,true> passed
test_can_query<ex_fq_fr<n1,n1>,n2,false> passed
test_can_query<ex_fq_fr<n1,n1>,n3,false> passed
test_can_query<ex_fq_fr<n1,n2>,s,true> passed
test_can_query<ex_fq_fr<n1,n2>,n1,true> passed
test_can_query<ex_fq_fr<n1,n2>,n2,true> passed
test_can_query<ex_fq_fr<n1,n2>,n3,false> passed
test_can_query<ex_fq_fr<n1,n3>,s,true> passed
test_can_query<ex_fq_fr<n1,n3>,n1,true> passed
test_can_query<ex_fq_fr<n1,n3>,n2,false> passed
test_can_query<ex_fq_fr<n1,n3>,n3,true> passed
test_can_query<ex_fq_fr<n2,n1>,s,true> passed
test_can_query<ex_fq_fr<n2,n1>,n1,true> passed
test_can_query<ex_fq_fr<n2,n1>,n2,true> passed
test_can_query<ex_fq_fr<n2,n1>,n3,false> passed
test_can_query<ex_fq_fr<n2,n2>,s,true> passed
test_can_query<ex_fq_fr<n2,n2>,n1,false> passed
test_can_query<ex_fq_fr<n2,n2>,n2,true> passed
test_can_query<ex_fq_fr<n2,n2>,n3,false> passed
test_can_query<ex_fq_fr<n2,n3>,s,true> passed
test_can_query<ex_fq_fr<n2,n3>,n1,false> passed
test_can_query<ex_fq_fr<n2,n3>,n2,true> passed
test_can_query<ex_fq_fr<n2,n3>,n3,true> passed
test_can_query<ex_fq_fr<n3,n1>,s,true> passed
test_can_query<ex_fq_fr<n3,n1>,n1,true> passed
test_can_query<ex_fq_fr<n3,n1>,n2,false> passed
test_can_query<ex_fq_fr<n3,n1>,n3,true> passed
test_can_query<ex_fq_fr<n3,n2>,s,true> passed
test_can_query<ex_fq_fr<n3,n2>,n1,false> passed
test_can_query<ex_fq_fr<n3,n2>,n2,true> passed
test_can_query<ex_fq_fr<n3,n2>,n3,true> passed
test_can_query<ex_fq_fr<n3,n3>,s,true> passed
test_can_query<ex_fq_fr<n3,n3>,n1,false> passed
test_can_query<ex_fq_fr<n3,n3>,n2,false> passed
test_can_query<ex_fq_fr<n3,n3>,n3,true> passed
test_query<ex_fq_fr<n1,n1>,s,n1> passed
test_query<ex_fq_fr<n1,n1>,n1,n1> passed
test_query<ex_fq_fr<n1,n2>,s,n1> passed
test_query<ex_fq_fr<n1,n2>,n1,n1> passed
test_query<ex_fq_fr<n1,n3>,s,n1> passed
test_query<ex_fq_fr<n1,n3>,n1,n1> passed
test_query<ex_fq_fr<n2,n1>,s,n2> passed
test_query<ex_fq_fr<n2,n1>,n2,n2> passed
test_query<ex_fq_fr<n2,n2>,s,n2> passed
test_query<ex_fq_fr<n2,n2>,n2,n2> passed
test_query<ex_fq_fr<n2,n3>,s,n2> passed
test_query<ex_fq_fr<n2,n3>,n2,n2> passed
test_query<ex_fq_fr<n3,n1>,s,n3> passed
test_query<ex_fq_fr<n3,n1>,n3,n3> passed
test_query<ex_fq_fr<n3,n2>,s,n3> passed
test_query<ex_fq_fr<n3,n2>,n3,n3> passed
test_query<ex_fq_fr<n3,n3>,s,n3> passed
test_query<ex_fq_fr<n3,n3>,n3,n3> passed
test_can_require<ex_fq_fr<n1,n1>,s,false> passed
test_can_require<ex_fq_fr<n1,n1>,n1,true> passed
test_can_require<ex_fq_fr<n1,n1>,n2,false> passed
test_can_require<ex_fq_fr<n1,n1>,n3,false> passed
test_can_require<ex_fq_fr<n1,n2>,s,false> passed
test_can_require<ex_fq_fr<n1,n2>,n1,true> passed
test_can_require<ex_fq_fr<n1,n2>,n2,true> passed
test_can_require<ex_fq_fr<n1,n2>,n3,false> passed
test_can_require<ex_fq_fr<n1,n3>,s,false> passed
test_can_require<ex_fq_fr<n1,n3>,n1,true> passed
test_can_require<ex_fq_fr<n1,n3>,n2,false> passed
test_can_require<ex_fq_fr<n1,n3>,n3,true> passed
test_can_require<ex_fq_fr<n2,n1>,s,false> passed
test_can_require<ex_fq_fr<n2,n1>,n1,true> passed
test_can_require<ex_fq_fr<n2,n1>,n2,true> passed
test_can_require<ex_fq_fr<n2,n1>,n3,false> passed
test_can_require<ex_fq_fr<n2,n2>,s,false> passed
test_can_require<ex_fq_fr<n2,n2>,n1,false> passed
test_can_require<ex_fq_fr<n2,n2>,n2,true> passed
test_can_require<ex_fq_fr<n2,n2>,n3,false> passed
test_can_require<ex_fq_fr<n2,n3>,s,false> passed
test_can_require<ex_fq_fr<n2,n3>,n1,false> passed
test_can_require<ex_fq_fr<n2,n3>,n2,true> passed
test_can_require<ex_fq_fr<n2,n3>,n3,true> passed
test_can_require<ex_fq_fr<n3,n1>,s,false> passed
test_can_require<ex_fq_fr<n3,n1>,n1,true> passed
test_can_require<ex_fq_fr<n3,n1>,n2,false> passed
test_can_require<ex_fq_fr<n3,n1>,n3,true> passed
test_can_require<ex_fq_fr<n3,n2>,s,false> passed
test_can_require<ex_fq_fr<n3,n2>,n1,false> passed
test_can_require<ex_fq_fr<n3,n2>,n2,true> passed
test_can_require<ex_fq_fr<n3,n2>,n3,true> passed
test_can_require<ex_fq_fr<n3,n3>,s,false> passed
test_can_require<ex_fq_fr<n3,n3>,n1,false> passed
test_can_require<ex_fq_fr<n3,n3>,n2,false> passed
test_can_require<ex_fq_fr<n3,n3>,n3,true> passed
test_require<ex_fq_fr<n1,n1>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n1,n1> passed
test_require<ex_fq_fr<n1,n2>,n2,n2> passed
test_require<ex_fq_fr<n1,n3>,n1,n1> passed
test_require<ex_fq_fr<n1,n3>,n3,n3> passed
test_require<ex_fq_fr<n2,n1>,n1,n1> passed
test_require<ex_fq_fr<n2,n1>,n2,n2> passed
test_require<ex_fq_fr<n2,n2>,n2,n2> passed
test_require<ex_fq_fr<n2,n3>,n2,n2> passed
test_require<ex_fq_fr<n2,n3>,n3,n3> passed
test_require<ex_fq_fr<n3,n1>,n1,n1> passed
test_require<ex_fq_fr<n3,n1>,n3,n3> passed
test_require<ex_fq_fr<n3,n2>,n2,n2> passed
test_require<ex_fq_fr<n3,n2>,n3,n3> passed
test_require<ex_fq_fr<n3,n3>,n3,n3> passed
test_can_prefer<ex_fq_fr<n1,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n1>,n2,true> passed
test_can_prefer<ex_fq_fr<n1,n1>,n3,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,n2,true> passed
test_can_prefer<ex_fq_fr<n1,n2>,n3,true> passed
test_can_prefer<ex_fq_fr<n1,n3>,s,false> passed
test_can_prefer<ex_fq_fr<n1,n3>,n1,true> passed
test_can_prefer<ex_fq_fr<n1,n3>,n2,true> passed
test_can_prefer<ex_fq_fr<n1,n3>,n3,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,n2,true> passed
test_can_prefer<ex_fq_fr<n2,n1>,n3,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,n2,true> passed
test_can_prefer<ex_fq_fr<n2,n2>,n3,true> passed
test_can_prefer<ex_fq_fr<n2,n3>,s,false> passed
test_can_prefer<ex_fq_fr<n2,n3>,n1,true> passed
test_can_prefer<ex_fq_fr<n2,n3>,n2,true> passed
test_can_prefer<ex_fq_fr<n2,n3>,n3,true> passed
test_can_prefer<ex_fq_fr<n3,n1>,s,false> passed
test_can_prefer<ex_fq_fr<n3,n1>,n1,true> passed
test_can_prefer<ex_fq_fr<n3,n1>,n2,true> passed
test_can_prefer<ex_fq_fr<n3,n1>,n3,true> passed
test_can_prefer<ex_fq_fr<n3,n2>,s,false> passed
test_can_prefer<ex_fq_fr<n3,n2>,n1,true> passed
test_can_prefer<ex_fq_fr<n3,n2>,n2,true> passed
test_can_prefer<ex_fq_fr<n3,n2>,n3,true> passed
test_can_prefer<ex_fq_fr<n3,n3>,s,false> passed
test_can_prefer<ex_fq_fr<n3,n3>,n1,true> passed
test_can_prefer<ex_fq_fr<n3,n3>,n2,true> passed
test_can_prefer<ex_fq_fr<n3,n3>,n3,true> passed
test_prefer<ex_fq_fr<n1,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n1>,n2,n1> passed
test_prefer<ex_fq_fr<n1,n1>,n3,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n2>,n2,n2> passed
test_prefer<ex_fq_fr<n1,n2>,n3,n1> passed
test_prefer<ex_fq_fr<n1,n3>,n1,n1> passed
test_prefer<ex_fq_fr<n1,n3>,n2,n1> passed
test_prefer<ex_fq_fr<n1,n3>,n3,n3> passed
test_prefer<ex_fq_fr<n2,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n2,n1>,n2,n2> passed
test_prefer<ex_fq_fr<n2,n1>,n3,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n1,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n2,n2> passed
test_prefer<ex_fq_fr<n2,n2>,n3,n2> passed
test_prefer<ex_fq_fr<n2,n3>,n1,n2> passed
test_prefer<ex_fq_fr<n2,n3>,n2,n2> passed
test_prefer<ex_fq_fr<n2,n3>,n3,n3> passed
test_prefer<ex_fq_fr<n3,n1>,n1,n1> passed
test_prefer<ex_fq_fr<n3,n1>,n2,n3> passed
test_prefer<ex_fq_fr<n3,n1>,n3,n3> passed
test_prefer<ex_fq_fr<n3,n2>,n1,n3> passed
test_prefer<ex_fq_fr<n3,n2>,n2,n2> passed
test_prefer<ex_fq_fr<n3,n2>,n3,n3> passed
test_prefer<ex_fq_fr<n3,n3>,n1,n3> passed
test_prefer<ex_fq_fr<n3,n3>,n2,n3> passed
test_prefer<ex_fq_fr<n3,n3>,n3,n3> passed
test_vars passed
mapping test suite ends

*** No errors detected.
prefer_only test suite begins
prefer_only_executor_query_test passed
prefer_only_executor_execute_test passed
prefer_only test suite ends

*** No errors detected.
experimental/deferred test suite begins
null_test passed
experimental/deferred test suite ends

*** No errors detected.
this_coro test suite begins
null_test passed
this_coro test suite ends

*** No errors detected.
streambuf test suite begins
streambuf_test passed
streambuf test suite ends

*** No errors detected.
writable_pipe test suite begins
writable_pipe_compile::test passed
writable_pipe test suite ends

*** No errors detected.
is_read_buffered test suite begins
is_read_buffered_test passed
is_read_buffered test suite ends

*** No errors detected.
static_thread_pool test suite begins
null_test passed
static_thread_pool test suite ends

*** No errors detected.
detached test suite begins
null_test passed
detached test suite ends

*** No errors detected.
buffered_write_stream test suite begins
test_compile passed
test_sync_operations passed
test_async_operations passed
buffered_write_stream test suite ends

*** No errors detected.
basic_datagram_socket test suite begins
null_test passed
basic_datagram_socket test suite ends

*** No errors detected.
basic_stream_file test suite begins
null_test passed
basic_stream_file test suite ends

*** No errors detected.
connect test suite begins
test_connect_range passed
test_connect_range_ec passed
test_connect_range_cond passed
test_connect_range_cond_ec passed
test_connect_iter passed
test_connect_iter_ec passed
test_connect_iter_cond passed
test_connect_iter_cond_ec passed
test_async_connect_range passed
test_async_connect_range_cond passed
test_async_connect_iter passed
test_async_connect_iter_cond passed
connect test suite ends

*** No errors detected.
basic_stream_socket test suite begins
null_test passed
basic_stream_socket test suite ends

*** No errors detected.
random_access_file test suite begins
random_access_file_compile::test passed
random_access_file test suite ends

*** No errors detected.
associator test suite begins
null_test passed
associator test suite ends

*** No errors detected.
Usage: udp_client <ip> <port1> <nports> <bufsize> {spin|block}
Usage: tcp_client <ip> <port> <nconns> <bufsize> {spin|block}
Usage: tcp_server <port> <nconns> <bufsize> {spin|block}
Usage: udp_server <port1> <nports> <bufsize> {spin|block}
socket_base test suite begins
socket_base_compile::test passed
socket_base_runtime::test passed
socket_base test suite ends

*** No errors detected.
basic_random_access_file test suite begins
null_test passed
basic_random_access_file test suite ends

*** No errors detected.
signal_set_base test suite begins
null_test passed
signal_set_base test suite ends

*** No errors detected.
basic_overlapped_handle test suite begins
null_test passed
basic_overlapped_handle test suite ends

*** No errors detected.
basic_random_access_handle test suite begins
null_test passed
basic_random_access_handle test suite ends

*** No errors detected.
windows/random_access_handle test suite begins
windows_random_access_handle_compile::test passed
windows/random_access_handle test suite ends

*** No errors detected.
windows/object_handle test suite begins
windows_object_handle_compile::test passed
windows/object_handle test suite ends

*** No errors detected.
basic_object_handle test suite begins
null_test passed
basic_object_handle test suite ends

*** No errors detected.
windows/overlapped_handle test suite begins
null_test passed
windows/overlapped_handle test suite ends

*** No errors detected.
windows/stream_handle test suite begins
windows_stream_handle_compile::test passed
windows/stream_handle test suite ends

*** No errors detected.
windows/overlapped_ptr test suite begins
windows_overlapped_ptr_compile::test passed
windows/overlapped_ptr test suite ends

*** No errors detected.
basic_stream_handle test suite begins
null_test passed
basic_stream_handle test suite ends

*** No errors detected.
compose test suite begins
compose_0_completion_args_test passed
compose_1_completion_arg_test passed
compose_default_cancellation_test passed
compose_partial_cancellation_test passed
compose_total_cancellation_test passed
compose test suite ends

*** No errors detected.
error test suite begins
error_test passed
error test suite ends

*** No errors detected.
serial_port test suite begins
serial_port_compile::test passed
serial_port test suite ends

*** No errors detected.
dispatch test suite begins
null_test passed
dispatch test suite ends

*** No errors detected.
steady_timer test suite begins
null_test passed
steady_timer test suite ends

*** No errors detected.
defer test suite begins
null_test passed
defer test suite ends

*** No errors detected.
write_at test suite begins
test_3_arg_const_buffer_write_at passed
test_3_arg_mutable_buffer_write_at passed
test_3_arg_vector_buffers_write_at passed
test_4_arg_nothrow_const_buffer_write_at passed
test_4_arg_nothrow_mutable_buffer_write_at passed
test_4_arg_nothrow_vector_buffers_write_at passed
test_4_arg_const_buffer_write_at passed
test_4_arg_mutable_buffer_write_at passed
test_4_arg_vector_buffers_write_at passed
test_5_arg_const_buffer_write_at passed
test_5_arg_mutable_buffer_write_at passed
test_5_arg_vector_buffers_write_at passed
test_4_arg_const_buffer_async_write_at passed
test_4_arg_mutable_buffer_async_write_at passed
test_4_arg_boost_array_buffers_async_write_at passed
test_4_arg_std_array_buffers_async_write_at passed
test_4_arg_vector_buffers_async_write_at passed
test_4_arg_streambuf_async_write_at passed
test_5_arg_const_buffer_async_write_at passed
test_5_arg_mutable_buffer_async_write_at passed
test_5_arg_boost_array_buffers_async_write_at passed
test_5_arg_std_array_buffers_async_write_at passed
test_5_arg_vector_buffers_async_write_at passed
test_5_arg_streambuf_async_write_at passed
write_at test suite ends

*** No errors detected.
posix/basic_stream_descriptor test suite begins
null_test passed
posix/basic_stream_descriptor test suite ends

*** No errors detected.
posix/descriptor test suite begins
null_test passed
posix/descriptor test suite ends

*** No errors detected.
posix/basic_descriptor test suite begins
null_test passed
posix/basic_descriptor test suite ends

*** No errors detected.
posix/stream_descriptor test suite begins
posix_stream_descriptor_compile::test passed
posix/stream_descriptor test suite ends

*** No errors detected.
posix/descriptor_base test suite begins
null_test passed
posix/descriptor_base test suite ends

*** No errors detected.
executor_work_guard test suite begins
null_test passed
executor_work_guard test suite ends

*** No errors detected.
is_write_buffered test suite begins
is_write_buffered_test passed
is_write_buffered test suite ends

*** No errors detected.
basic_deadline_timer test suite begins
null_test passed
basic_deadline_timer test suite ends

*** No errors detected.
co_spawn test suite begins
null_test passed
co_spawn test suite ends

*** No errors detected.
any_io_executor test suite begins
any_io_executor_construction_test passed
any_io_executor_nothrow_construction_test passed
any_io_executor_assignment_test passed
any_io_executor_swap_test passed
any_io_executor_query_test passed
any_io_executor_execute_test passed
any_io_executor test suite ends

*** No errors detected.
post test suite begins
null_test passed
post test suite ends

*** No errors detected.
read test suite begins
test_2_arg_zero_buffers_read passed
test_2_arg_mutable_buffer_read passed
test_2_arg_vector_buffers_read passed
test_2_arg_dynamic_string_read passed
test_2_arg_streambuf_read passed
test_3_arg_nothrow_zero_buffers_read passed
test_3_arg_nothrow_mutable_buffer_read passed
test_3_arg_nothrow_vector_buffers_read passed
test_3_arg_nothrow_dynamic_string_read passed
test_3_arg_nothrow_streambuf_read passed
test_3_arg_mutable_buffer_read passed
test_3_arg_vector_buffers_read passed
test_3_arg_dynamic_string_read passed
test_3_arg_streambuf_read passed
test_4_arg_mutable_buffer_read passed
test_4_arg_vector_buffers_read passed
test_4_arg_dynamic_string_read passed
test_4_arg_streambuf_read passed
test_3_arg_mutable_buffer_async_read passed
test_3_arg_boost_array_buffers_async_read passed
test_3_arg_std_array_buffers_async_read passed
test_3_arg_vector_buffers_async_read passed
test_3_arg_dynamic_string_async_read passed
test_3_arg_streambuf_async_read passed
test_4_arg_mutable_buffer_async_read passed
test_4_arg_vector_buffers_async_read passed
test_4_arg_boost_array_buffers_async_read passed
test_4_arg_std_array_buffers_async_read passed
test_4_arg_dynamic_string_async_read passed
test_4_arg_streambuf_async_read passed
read test suite ends

*** No errors detected.
compose test suite begins
compose_0_completion_args_test passed
compose_1_completion_arg_test passed
compose_default_cancellation_test passed
compose_partial_cancellation_test passed
compose_total_cancellation_test passed
compose test suite ends

*** No errors detected.
consign test suite begins
consign_test passed
consign test suite ends

*** No errors detected.
as_tuple test suite begins
as_tuple_test passed
as_tuple_constness_test passed
partial_as_tuple_test passed
as_tuple test suite ends

*** No errors detected.
co_composed test suite begins
null_test passed
co_composed test suite ends

*** No errors detected.
awaitable test suite begins
null_test passed
awaitable test suite ends

*** No errors detected.
coroutine test suite begins
yield_break_test passed
return_test passed
exception_test passed
fall_off_end_test passed
coroutine test suite ends

*** No errors detected.
generic/raw_protocol test suite begins
generic_raw_protocol_socket_compile::test passed
generic/raw_protocol test suite ends

*** No errors detected.
generic/basic_endpoint test suite begins
null_test passed
generic/basic_endpoint test suite ends

*** No errors detected.
generic/seq_packet_protocol test suite begins
generic_seq_packet_protocol_socket_compile::test passed
generic/seq_packet_protocol test suite ends

*** No errors detected.
generic/stream_protocol test suite begins
generic_stream_protocol_socket_compile::test passed
generic/stream_protocol test suite ends

*** No errors detected.
generic/datagram_protocol test suite begins
generic_datagram_protocol_socket_compile::test passed
generic/datagram_protocol test suite ends

*** No errors detected.
buffer test suite begins
buffer_compile::test passed
buffer_copy_runtime::test passed
buffer_sequence::test passed
buffer_literals::test passed
buffer test suite ends

*** No errors detected.
cancel_after test suite begins
cancel_after_function_object_test passed
cancel_after_timer_function_object_test passed
cancel_after_completion_token_v1_test passed
cancel_after_timer_completion_token_v1_test passed
cancel_after_completion_token_v2_test passed
cancel_after_timer_completion_token_v2_test passed
partial_cancel_after_test passed
partial_cancel_after_timer_test passed
cancel_after test suite ends

*** No errors detected.
registered_buffer test suite begins
registered_buffer_compile::test passed
registered_buffer test suite ends

*** No errors detected.
ssl/stream test suite begins
ssl_stream_compile::test passed
ssl/stream test suite ends

*** No errors detected.
ssl/rfc2818_verification test suite begins
null_test passed
ssl/rfc2818_verification test suite ends

*** No errors detected.
ssl/context test suite begins
null_test passed
ssl/context test suite ends

*** No errors detected.
ssl/stream_base test suite begins
null_test passed
ssl/stream_base test suite ends

*** No errors detected.
ssl/host_name_verification test suite begins
null_test passed
ssl/host_name_verification test suite ends

*** No errors detected.
ssl/error test suite begins
null_test passed
ssl/error test suite ends

*** No errors detected.
ssl/context_base test suite begins
null_test passed
ssl/context_base test suite ends

*** No errors detected.
associated_executor test suite begins
null_test passed
associated_executor test suite ends

*** No errors detected.
io_context test suite begins
io_context_test passed
io_context_service_test passed
io_context_executor_query_test passed
io_context_executor_execute_test passed
io_context test suite ends

*** No errors detected.
buffer_registration test suite begins
null_test passed
buffer_registration test suite ends

*** No errors detected.
stream_file test suite begins
stream_file_compile::test passed
stream_file test suite ends

*** No errors detected.
bind_cancellation_slot test suite begins
bind_cancellation_slot_to_function_object_test passed
bind_cancellation_slot_to_completion_token_v1_test passed
bind_cancellation_slot_to_completion_token_v2_test passed
partial_bind_cancellation_slot passed
bind_cancellation_slot test suite ends

*** No errors detected.
basic_seq_packet_socket test suite begins
null_test passed
basic_seq_packet_socket test suite ends

*** No errors detected.
read_at test suite begins
test_3_arg_mutable_buffer_read_at passed
test_3_arg_vector_buffers_read_at passed
test_3_arg_streambuf_read_at passed
test_4_arg_nothrow_mutable_buffer_read_at passed
test_4_arg_nothrow_vector_buffers_read_at passed
test_4_arg_nothrow_streambuf_read_at passed
test_4_arg_mutable_buffer_read_at passed
test_4_arg_vector_buffers_read_at passed
test_4_arg_streambuf_read_at passed
test_5_arg_mutable_buffer_read_at passed
test_5_arg_vector_buffers_read_at passed
test_5_arg_streambuf_read_at passed
test_4_arg_mutable_buffer_async_read_at passed
test_4_arg_boost_array_buffers_async_read_at passed
test_4_arg_std_array_buffers_async_read_at passed
test_4_arg_vector_buffers_async_read_at passed
test_4_arg_streambuf_async_read_at passed
test_5_arg_mutable_buffer_async_read_at passed
test_5_arg_boost_array_buffers_async_read_at passed
test_5_arg_std_array_buffers_async_read_at passed
test_5_arg_vector_buffers_async_read_at passed
test_5_arg_streambuf_async_read_at passed
read_at test suite ends

*** No errors detected.
any_completion_handler test suite begins
any_completion_handler_construction_test passed
any_completion_handler_assignment_test passed
any_completion_handler_associator_test passed
any_completion_handler_invocation_test passed
any_completion_handler test suite ends

*** No errors detected.
cancellation_type test suite begins
null_test passed
cancellation_type test suite ends

*** No errors detected.
system_executor test suite begins
system_executor_query_test passed
system_executor_execute_test passed
system_executor test suite ends

*** No errors detected.
```

