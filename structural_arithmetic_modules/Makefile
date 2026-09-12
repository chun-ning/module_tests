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

.DEFAULT_GOAL := test

.PHONY: test adder_test adder_carry_save adder_ripple_carry FORCE

# Run both implementations; each adder target can also be run individually.
test adder_test: adder_ripple_carry adder_carry_save

adder_carry_save: $(RTL_DIR)/adder_carry_save.v $(TEST_DIR)/adder_carry_save_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s adder_carry_save_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/adder_carry_save_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

adder_ripple_carry: $(RTL_DIR)/adder_ripple_carry.v $(TEST_DIR)/adder_ripple_carry_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s adder_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/adder_ripple_carry_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

FORCE:
