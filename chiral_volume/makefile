# Makefile'as skirtas programos testavimui
# Testavimas: programos išvestis yra lygynama su 
# etaloniniais pavyzdžiais naudojant *nix diff programa

SHELL := /bin/bash

INPUT_DIR = inputs
OUTPUT_DIR = outputs
TEST_DIR = tests

TEST_FILES = $(wildcard ${TEST_DIR}/*.sh)
OUTP_FILES = ${TEST_FILES:${TEST_DIR}/%.sh=${OUTPUT_DIR}/%.out}
DIFF_FILES = ${TEST_FILES:${TEST_DIR}/%.sh=${OUTPUT_DIR}/%.diff}

.PHONY: all clean distclean test

all: test

test: ${DIFF_FILES}

${OUTPUT_DIR}/%.diff: ${OUTPUT_DIR}/%.out ${TEST_DIR}/%.sh
	@printf "%-25s: " $*
	@$(word 2, $^) 2>&1 \
	| diff <(less -n +2 $<) <(less -n +2 -) > $@; \
	if [ $$? -eq 0 ]; then \
		echo OK; \
	else \
		echo FAILED:; \
		cat $@; \
	fi

clean:
	rm -f ${DIFF_FILES}

distclean: clean

