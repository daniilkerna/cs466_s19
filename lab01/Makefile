#
# project target
#
TARGET=blinky

#
# Defines the part type that this project uses.
#
PART=TM4C123GH6PM

#
# The base directory for TivaWare.
#
LABROOT=..
TIVAROOT=../../TivaDriver


# Echo full command lines.. Comment out for terse
VERBOSE=1

# Include Debugging flags and disable some optimization
DEBUG=1

SIZE=arm-none-eabi-size

#
# Support the flash util

ifeq ($(OS),Windows_NT)
	#Windows stuff
	FLASHOPTS=--verify
	FLASHOPTS+=--reset
	FLASH=${TIVAROOT}/lmflash
else
	#Linux stuff
	FLASHOPTS=-v
	FLASH=lm4flash
endif


#
# Include the common make definitions.
#
include ${LABROOT}/makedefs

#
# Where to find header files that do not live in the source directory.
#
IPATH+=.
IPATH+=${TIVAROOT}

#
# The default rule, which causes the blinky example to be built.
#
all: ${COMPILER}
all: ${COMPILER}/${TARGET}.axf

#
# The rule to clean out all the build products.
#
clean:
	@rm -rf ${COMPILER} ${wildcard *~}

#
# The rule to create the target directory.
#
${COMPILER}:
	@mkdir -p ${COMPILER}

#
# Rules for building the blinky example.
#
${COMPILER}/${TARGET}.axf: ${COMPILER}/${TARGET}.o
${COMPILER}/${TARGET}.axf: ${COMPILER}/startup_${COMPILER}.o
${COMPILER}/${TARGET}.axf: ${TARGET}.ld
SCATTERgcc_blinky=${TARGET}.ld
ENTRY_${TARGET}=ResetISR

#
# Include the automatically generated dependency files.
#
ifneq (${MAKECMDGOALS},clean)
-include ${wildcard ${COMPILER}/*.d} __dummy__
endif



#
# A rule to flash and restart the program
#
flash: ${COMPILER}/blinky.axf
	${SIZE} ${COMPILER}/${TARGET}.axf
	${FLASH} ${FLASHOPTS} ${COMPILER}/blinky.bin
    
    
