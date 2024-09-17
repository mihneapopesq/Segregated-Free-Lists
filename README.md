# Segregated-Free-Lists

### Description:
The purpose of the code is to simulate the behavior of Segregated Free Lists. It is based on a vector where each entry stores the starting address of a doubly linked list containing free memory blocks of the same size, with their sizes being powers of 2.

### Commands:
The program can execute commands such as: INIT_HEAP, MALLOC, FREE, READ, WRITE, DUMP_MEMORY, and DESTROY_HEAP.

INIT_HEAP <heap_start_address> <num_lists> <num_bytes_per_list> <recovery_type>:
This command creates a number of lists that contain contiguous starting addresses within the range [heap_base, heap_base + heap_size). In INIT_HEAP, each list corresponds to a block with a size equal to a power of 2.

MALLOC <num_bytes>:
Allocates a memory block of the specified size by searching through the segregated lists to find an appropriate block size. The algorithm calculates the required memory block size, rounding it up to the nearest power of 2. Once the block is found, it is removed from the segregated free lists and marked as allocated.

If the requested block is smaller than the available blocks in the list, fragmentation occurs.

During fragmentation, it checks if the requested number of bytes exceeds the maximum available size. After allocation, the data structures representing free blocks are updated by removing the allocated block from the free list and adding a new free block, post-fragmentation.

The operations in MALLOC have a complexity of O(n).

FREE <address>:
The FREE function releases a previously allocated memory block and reintroduces it into the corresponding list.

The algorithm identifies the memory block to free, checks if it can be merged with other free blocks, and if so, combines them into a larger block and updates the list. If the blocks cannot be combined, the block is simply reinserted into the appropriate list.

The operations in FREE have a complexity of O(n) and O(1).

READ <address> <num_bytes>:
This function relies on check_valid_address to ensure the requested read address is valid, meaning the address and number of bytes fall within an allocated block. It does this by traversing the linked list of memory blocks, with a complexity of O(n).

Once the read request is confirmed valid, it traverses each byte starting from the address and displays it, with a complexity of O(num bytes).

If the requested address is invalid, indicated by the variable ok being 0, the function handles the error by outputting "Segmentation fault (core dumped)" and dumping memory before ending the program.

WRITE <address> <data> <num_bytes>:
The function det_parameters extracts the text enclosed in quotes for the data to be written. Similar to READ, the check_valid_access function checks if the data size and location are valid for writing. If the address is invalid, the function handles the error and dumps the memory just like in READ.

The actual data writing uses memcpy. The write location is calculated by adjusting the address to obtain a relative address within the memory block.

DUMP_MEMORY:
Displays information about the current state of the heap, including allocated and free blocks, by traversing the segregated list vector.

The complexity is O(n).

DESTROY_HEAP:
Releases all resources allocated for the heap by traversing each segregated list and freeing the associated nodes and memory blocks. It also frees the segregated list vector and other heap-related data structures.

The complexity is O(elements_per_list).

Comments on the assignment:
It was an interesting task that taught me a new concept, Segregated Free Lists. Through this assignment, I deepened my understanding of lists as well as other data structures.
