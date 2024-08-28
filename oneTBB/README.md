# 软件包 : oneTBB

# 测试环境 

### OS : openEuler 2309 

### Arch : RISC-V

### Machine : Qemu-Virt

# 测试流程

1. 拉取  oneTBB 源码 

   ```shell
   git clone https://github.com/oneapi-src/oneTBB.git
   ```

2. 安装依赖

   ```shell
   sudo yum install gcc g++ cmake make 
   ```

3. 在 riscv 机器上编译

   ```shell
   mkdir build && cd build
   cmake -DCMAKE_INSTALL_PREFIX=/tmp/my_installed_onetbb  ..
   ```

4. 编译

   ```shell
   make
   ```

5. 测试

   ```shell
   make test
   ```

# 测试结果

### 编译 : 通过

### 测试 : 通过

```shell
Running tests...
Test project /root/oneTBB/build
        Start   1: test_tick_count
  1/137 Test   #1: test_tick_count ..........................   Passed    0.33 sec
        Start   2: test_allocators
  2/137 Test   #2: test_allocators ..........................   Passed    0.14 sec
        Start   3: test_arena_priorities
  3/137 Test   #3: test_arena_priorities ....................   Passed    0.32 sec
        Start   4: test_dynamic_link
  4/137 Test   #4: test_dynamic_link ........................   Passed    0.11 sec
        Start   5: test_collaborative_call_once
  5/137 Test   #5: test_collaborative_call_once .............   Passed   16.32 sec
        Start   6: test_concurrent_lru_cache
  6/137 Test   #6: test_concurrent_lru_cache ................   Passed    0.11 sec
        Start   7: test_concurrent_unordered_map
  7/137 Test   #7: test_concurrent_unordered_map ............   Passed    7.50 sec
        Start   8: test_concurrent_unordered_set
  8/137 Test   #8: test_concurrent_unordered_set ............   Passed    8.40 sec
        Start   9: test_concurrent_map
  9/137 Test   #9: test_concurrent_map ......................   Passed    3.05 sec
        Start  10: test_concurrent_set
 10/137 Test  #10: test_concurrent_set ......................   Passed    4.61 sec
        Start  11: test_concurrent_priority_queue
 11/137 Test  #11: test_concurrent_priority_queue ...........   Passed    0.87 sec
        Start  12: test_partitioner
 12/137 Test  #12: test_partitioner .........................   Passed    1.53 sec
        Start  13: test_parallel_for
 13/137 Test  #13: test_parallel_for ........................   Passed    2.57 sec
        Start  14: test_parallel_for_each
 14/137 Test  #14: test_parallel_for_each ...................   Passed    0.88 sec
        Start  15: test_parallel_reduce
 15/137 Test  #15: test_parallel_reduce .....................   Passed    9.49 sec
        Start  16: test_parallel_sort
 16/137 Test  #16: test_parallel_sort .......................   Passed   44.99 sec
        Start  17: test_parallel_invoke
 17/137 Test  #17: test_parallel_invoke .....................   Passed    0.92 sec
        Start  18: test_parallel_scan
 18/137 Test  #18: test_parallel_scan .......................   Passed   21.92 sec
        Start  19: test_parallel_pipeline
 19/137 Test  #19: test_parallel_pipeline ...................   Passed   34.89 sec
        Start  20: test_eh_algorithms
 20/137 Test  #20: test_eh_algorithms .......................   Passed   12.82 sec
        Start  21: test_blocked_range
 21/137 Test  #21: test_blocked_range .......................   Passed    0.11 sec
        Start  22: test_concurrent_vector
 22/137 Test  #22: test_concurrent_vector ...................   Passed    1.51 sec
        Start  23: test_task_group
 23/137 Test  #23: test_task_group ..........................   Passed    8.44 sec
        Start  24: test_concurrent_hash_map
 24/137 Test  #24: test_concurrent_hash_map .................   Passed    0.79 sec
        Start  25: test_task_arena
 25/137 Test  #25: test_task_arena ..........................   Passed   60.14 sec
        Start  26: test_enumerable_thread_specific
 26/137 Test  #26: test_enumerable_thread_specific ..........   Passed    1.90 sec
        Start  27: test_concurrent_queue
 27/137 Test  #27: test_concurrent_queue ....................   Passed    6.82 sec
        Start  28: test_resumable_tasks
 28/137 Test  #28: test_resumable_tasks .....................   Passed  121.09 sec
        Start  29: test_mutex
 29/137 Test  #29: test_mutex ...............................   Passed    7.24 sec
        Start  30: test_function_node
 30/137 Test  #30: test_function_node .......................   Passed   14.71 sec
        Start  31: test_multifunction_node
 31/137 Test  #31: test_multifunction_node ..................   Passed   15.75 sec
        Start  32: test_broadcast_node
 32/137 Test  #32: test_broadcast_node ......................   Passed    0.63 sec
        Start  33: test_buffer_node
 33/137 Test  #33: test_buffer_node .........................   Passed    0.46 sec
        Start  34: test_composite_node
 34/137 Test  #34: test_composite_node ......................   Passed   19.23 sec
        Start  35: test_continue_node
 35/137 Test  #35: test_continue_node .......................   Passed   11.42 sec
        Start  36: test_eh_flow_graph
 36/137 Test  #36: test_eh_flow_graph .......................   Passed    3.39 sec
        Start  37: test_flow_graph
 37/137 Test  #37: test_flow_graph ..........................   Passed    0.90 sec
        Start  38: test_flow_graph_priorities
 38/137 Test  #38: test_flow_graph_priorities ...............   Passed    2.69 sec
        Start  39: test_flow_graph_whitebox
 39/137 Test  #39: test_flow_graph_whitebox .................   Passed    0.34 sec
        Start  40: test_indexer_node
 40/137 Test  #40: test_indexer_node ........................   Passed    2.02 sec
        Start  41: test_join_node
 41/137 Test  #41: test_join_node ...........................   Passed    5.60 sec
        Start  42: test_join_node_key_matching
 42/137 Test  #42: test_join_node_key_matching ..............   Passed    0.66 sec
        Start  43: test_join_node_key_matching_n_args
 43/137 Test  #43: test_join_node_key_matching_n_args .......   Passed    2.66 sec
        Start  44: test_join_node_msg_key_matching
 44/137 Test  #44: test_join_node_msg_key_matching ..........   Passed    0.56 sec
        Start  45: test_join_node_msg_key_matching_n_args
 45/137 Test  #45: test_join_node_msg_key_matching_n_args ...   Passed    3.31 sec
        Start  46: test_join_node_preview
 46/137 Test  #46: test_join_node_preview ...................   Passed    0.25 sec
        Start  47: test_limiter_node
 47/137 Test  #47: test_limiter_node ........................   Passed    2.30 sec
        Start  48: test_priority_queue_node
 48/137 Test  #48: test_priority_queue_node .................   Passed    0.31 sec
        Start  49: test_queue_node
 49/137 Test  #49: test_queue_node ..........................   Passed    0.90 sec
        Start  50: test_sequencer_node
 50/137 Test  #50: test_sequencer_node ......................   Passed    0.39 sec
        Start  51: test_split_node
 51/137 Test  #51: test_split_node ..........................   Passed    1.16 sec
        Start  52: test_tagged_msg
 52/137 Test  #52: test_tagged_msg ..........................   Passed    0.13 sec
        Start  53: test_overwrite_node
 53/137 Test  #53: test_overwrite_node ......................   Passed   40.85 sec
        Start  54: test_write_once_node
 54/137 Test  #54: test_write_once_node .....................   Passed   40.01 sec
        Start  55: test_async_node
 55/137 Test  #55: test_async_node ..........................   Passed    7.40 sec
        Start  56: test_input_node
 56/137 Test  #56: test_input_node ..........................   Passed    0.27 sec
        Start  57: test_profiling
 57/137 Test  #57: test_profiling ...........................   Passed    0.15 sec
        Start  58: test_concurrent_queue_whitebox
 58/137 Test  #58: test_concurrent_queue_whitebox ...........   Passed    2.75 sec
        Start  59: test_intrusive_list
 59/137 Test  #59: test_intrusive_list ......................   Passed    7.18 sec
        Start  60: test_semaphore
 60/137 Test  #60: test_semaphore ...........................   Passed    4.48 sec
        Start  61: test_environment_whitebox
 61/137 Test  #61: test_environment_whitebox ................   Passed    0.30 sec
        Start  62: test_hw_concurrency
 62/137 Test  #62: test_hw_concurrency ......................   Passed    0.13 sec
        Start  63: test_eh_thread
 63/137 Test  #63: test_eh_thread ...........................   Passed    0.13 sec
        Start  64: test_global_control
 64/137 Test  #64: test_global_control ......................   Passed    3.67 sec
        Start  65: test_task
 65/137 Test  #65: test_task ................................   Passed   25.93 sec
        Start  66: test_concurrent_monitor
 66/137 Test  #66: test_concurrent_monitor ..................   Passed    3.46 sec
        Start  67: test_scheduler_mix
 67/137 Test  #67: test_scheduler_mix .......................   Passed   18.34 sec
        Start  68: test_handle_perror
 68/137 Test  #68: test_handle_perror .......................   Passed    0.16 sec
        Start  69: test_arena_constraints
 69/137 Test  #69: test_arena_constraints ...................   Passed    0.39 sec
        Start  70: test_tbb_fork
 70/137 Test  #70: test_tbb_fork ............................   Passed    8.53 sec
        Start  71: test_tbb_header
 71/137 Test  #71: test_tbb_header ..........................   Passed    0.13 sec
        Start  72: test_openmp
 72/137 Test  #72: test_openmp ..............................   Passed    0.29 sec
        Start  73: conformance_tick_count
 73/137 Test  #73: conformance_tick_count ...................   Passed    0.11 sec
        Start  74: conformance_allocators
 74/137 Test  #74: conformance_allocators ...................   Passed   32.98 sec
        Start  75: conformance_mutex
 75/137 Test  #75: conformance_mutex ........................   Passed    3.96 sec
        Start  76: conformance_task_group
 76/137 Test  #76: conformance_task_group ...................   Passed    0.23 sec
        Start  77: conformance_task_group_context
 77/137 Test  #77: conformance_task_group_context ...........   Passed    0.12 sec
        Start  78: conformance_task_arena
 78/137 Test  #78: conformance_task_arena ...................   Passed    0.19 sec
        Start  79: conformance_collaborative_call_once
 79/137 Test  #79: conformance_collaborative_call_once ......   Passed    0.18 sec
        Start  80: conformance_concurrent_lru_cache
 80/137 Test  #80: conformance_concurrent_lru_cache .........   Passed    0.11 sec
        Start  81: conformance_concurrent_unordered_map
 81/137 Test  #81: conformance_concurrent_unordered_map .....   Passed    0.95 sec
        Start  82: conformance_concurrent_unordered_set
 82/137 Test  #82: conformance_concurrent_unordered_set .....   Passed    1.01 sec
        Start  83: conformance_concurrent_map
 83/137 Test  #83: conformance_concurrent_map ...............   Passed    1.10 sec
        Start  84: conformance_concurrent_set
 84/137 Test  #84: conformance_concurrent_set ...............   Passed    0.98 sec
        Start  85: conformance_concurrent_priority_queue
 85/137 Test  #85: conformance_concurrent_priority_queue ....   Passed    1.09 sec
        Start  86: conformance_parallel_for
 86/137 Test  #86: conformance_parallel_for .................   Passed   11.34 sec
        Start  87: conformance_parallel_for_each
 87/137 Test  #87: conformance_parallel_for_each ............   Passed    0.69 sec
        Start  88: conformance_parallel_reduce
 88/137 Test  #88: conformance_parallel_reduce ..............   Passed    2.59 sec
        Start  89: conformance_parallel_scan
 89/137 Test  #89: conformance_parallel_scan ................   Passed    0.21 sec
        Start  90: conformance_parallel_sort
 90/137 Test  #90: conformance_parallel_sort ................   Passed    0.45 sec
        Start  91: conformance_parallel_pipeline
 91/137 Test  #91: conformance_parallel_pipeline ............   Passed    3.53 sec
        Start  92: conformance_parallel_invoke
 92/137 Test  #92: conformance_parallel_invoke ..............   Passed    2.94 sec
        Start  93: conformance_blocked_range
 93/137 Test  #93: conformance_blocked_range ................   Passed    1.43 sec
        Start  94: conformance_blocked_range2d
 94/137 Test  #94: conformance_blocked_range2d ..............   Passed   10.68 sec
        Start  95: conformance_blocked_range3d
 95/137 Test  #95: conformance_blocked_range3d ..............   Passed    3.65 sec
        Start  96: conformance_blocked_rangeNd
 96/137 Test  #96: conformance_blocked_rangeNd ..............   Passed    4.23 sec
        Start  97: conformance_concurrent_vector
 97/137 Test  #97: conformance_concurrent_vector ............   Passed   15.00 sec
        Start  98: conformance_global_control
 98/137 Test  #98: conformance_global_control ...............   Passed    1.33 sec
        Start  99: conformance_concurrent_hash_map
 99/137 Test  #99: conformance_concurrent_hash_map ..........   Passed    6.74 sec
        Start 100: conformance_enumerable_thread_specific
100/137 Test #100: conformance_enumerable_thread_specific ...   Passed   10.44 sec
        Start 101: conformance_combinable
101/137 Test #101: conformance_combinable ...................   Passed    8.45 sec
        Start 102: conformance_concurrent_queue
102/137 Test #102: conformance_concurrent_queue .............   Passed    9.61 sec
        Start 103: conformance_resumable_tasks
103/137 Test #103: conformance_resumable_tasks ..............   Passed    0.18 sec
        Start 104: conformance_version
104/137 Test #104: conformance_version ......................   Passed    0.12 sec
        Start 105: conformance_function_node
105/137 Test #105: conformance_function_node ................   Passed    0.24 sec
        Start 106: conformance_multifunction_node
106/137 Test #106: conformance_multifunction_node ...........   Passed    0.23 sec
        Start 107: conformance_input_node
107/137 Test #107: conformance_input_node ...................   Passed    1.28 sec
        Start 108: conformance_continue_node
108/137 Test #108: conformance_continue_node ................   Passed    0.17 sec
        Start 109: conformance_async_node
109/137 Test #109: conformance_async_node ...................   Passed    0.23 sec
        Start 110: conformance_overwrite_node
110/137 Test #110: conformance_overwrite_node ...............   Passed    0.17 sec
        Start 111: conformance_write_once_node
111/137 Test #111: conformance_write_once_node ..............   Passed    0.17 sec
        Start 112: conformance_buffer_node
112/137 Test #112: conformance_buffer_node ..................   Passed    0.16 sec
        Start 113: conformance_queue_node
113/137 Test #113: conformance_queue_node ...................   Passed    0.16 sec
        Start 114: conformance_priority_queue_node
114/137 Test #114: conformance_priority_queue_node ..........   Passed    0.17 sec
        Start 115: conformance_sequencer_node
115/137 Test #115: conformance_sequencer_node ...............   Passed    0.18 sec
        Start 116: conformance_limiter_node
116/137 Test #116: conformance_limiter_node .................   Passed    0.17 sec
        Start 117: conformance_broadcast_node
117/137 Test #117: conformance_broadcast_node ...............   Passed    0.15 sec
        Start 118: conformance_composite_node
118/137 Test #118: conformance_composite_node ...............   Passed    0.17 sec
        Start 119: conformance_indexer_node
119/137 Test #119: conformance_indexer_node .................   Passed    0.16 sec
        Start 120: conformance_split_node
120/137 Test #120: conformance_split_node ...................   Passed    0.17 sec
        Start 121: conformance_join_node
121/137 Test #121: conformance_join_node ....................   Passed    0.22 sec
        Start 122: conformance_graph
122/137 Test #122: conformance_graph ........................   Passed    0.22 sec
        Start 123: conformance_arena_constraints
123/137 Test #123: conformance_arena_constraints ............   Passed    0.12 sec
        Start 124: test_scalable_allocator
124/137 Test #124: test_scalable_allocator ..................   Passed   18.93 sec
        Start 125: test_malloc_pools
125/137 Test #125: test_malloc_pools ........................   Passed   29.16 sec
        Start 126: test_malloc_init_shutdown
126/137 Test #126: test_malloc_init_shutdown ................   Passed    0.12 sec
        Start 127: test_malloc_regression
127/137 Test #127: test_malloc_regression ...................   Passed    0.75 sec
        Start 128: test_malloc_shutdown_hang
128/137 Test #128: test_malloc_shutdown_hang ................   Passed    7.73 sec
        Start 129: test_malloc_compliance
129/137 Test #129: test_malloc_compliance ...................   Passed   34.68 sec
        Start 130: test_malloc_used_by_lib
130/137 Test #130: test_malloc_used_by_lib ..................   Passed    0.18 sec
        Start 131: test_malloc_lib_unload
131/137 Test #131: test_malloc_lib_unload ...................   Passed    0.14 sec
        Start 132: test_malloc_pure_c
132/137 Test #132: test_malloc_pure_c .......................   Passed    0.23 sec
        Start 133: test_malloc_whitebox
133/137 Test #133: test_malloc_whitebox .....................   Passed   36.97 sec
        Start 134: test_malloc_atexit
134/137 Test #134: test_malloc_atexit .......................   Passed    0.18 sec
        Start 135: test_malloc_overload
135/137 Test #135: test_malloc_overload .....................   Passed    0.51 sec
        Start 136: test_malloc_overload_disable
136/137 Test #136: test_malloc_overload_disable .............   Passed    0.11 sec
        Start 137: test_malloc_new_handler
137/137 Test #137: test_malloc_new_handler ..................   Passed    0.26 sec
100% tests passed, 0 tests failed out of 137
```

