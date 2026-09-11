# Directories
PROJECT_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))
RTL_DIR = $(PROJECT_DIR)adder
TEST_DIR = $(PROJECT_DIR)test
BUILD_DIR = $(PROJECT_DIR)test/build
WAVE_DIR = $(PROJECT_DIR)test/waves

# Verilog compiler and simulator
IVERILOG = iverilog
VVP = vvp
GTKWAVE = gtkwave

.PHONY: test adder_test FORCE
test adder_test: adder_ripple_carry

# Example: make adder_carry_save selects $(RTL_DIR)/adder_carry_save.v.
# Each adder must expose module top with the same ports and N parameter.
adder_%: $(RTL_DIR)/adder_%.v $(TEST_DIR)/adder_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s adder_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/adder_test.v $<
	$(VVP) $(BUILD_DIR)/$@

FORCE:
