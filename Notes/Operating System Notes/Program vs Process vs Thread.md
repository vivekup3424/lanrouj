1. Program is an executable containing a set of instructions
	1. Stored in disk
2. Process is the program that is currently running in system, hence its loaded in RAM
	1. Each process has its own data section, code section, program counter, stack and heap
3. Threads 
	1. every process can have independent sections which can be executed concurrently
	2. each of these can be loaded in a light weight process called threads
	3. to make these threads lightweight we will share the common data section, code section (which would containing common global variables)
	>[!Example]
	>If an images to be converted from Jpeg to png
	>use threads here convert many sections of images independently
	