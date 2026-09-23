# Directories
PROJECT_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))
RTL_DIR = $(PROJECT_DIR)adder
MULTIPLIER_DIR = $(PROJECT_DIR)multiplier
DIVIDER_DIR = $(PROJECT_DIR)divider
TEST_DIR = $(PROJECT_DIR)test
BUILD_DIR = $(PROJECT_DIR)test/build
WAVE_DIR = $(PROJECT_DIR)test/waves

# Verilog compiler and simulator
IVERILOG = iverilog
VVP = vvp
GTKWAVE = gtkwave

.DEFAULT_GOAL := test

.PHONY: test adder_test multiplier_test divider_test comparator_test comparator adder_carry_save adder_ripple_carry adder_carry_skip multiplier_shift_add divider_restoring FORCE

# Run all tests; each implementation can also be run individually.
test: adder_test multiplier_test divider_test comparator_test
adder_test: adder_ripple_carry adder_carry_save adder_carry_skip
multiplier_test: multiplier_shift_add
divider_test: divider_restoring
comparator_test: comparator

comparator: $(PROJECT_DIR)comparator.v $(TEST_DIR)/comparator_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s comparator_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/comparator_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

adder_carry_skip: $(RTL_DIR)/adder_carry_skip.v $(TEST_DIR)/adder_carry_skip_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s adder_carry_skip_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/adder_carry_skip_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

adder_carry_save: $(RTL_DIR)/adder_carry_save.v $(TEST_DIR)/adder_carry_save_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s adder_carry_save_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/adder_carry_save_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

adder_ripple_carry: $(RTL_DIR)/adder_ripple_carry.v $(TEST_DIR)/adder_ripple_carry_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s adder_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/adder_ripple_carry_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

multiplier_shift_add: $(MULTIPLIER_DIR)/multiplier_shift_add.v $(TEST_DIR)/multiplier_shift_add_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s multiplier_shift_add_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/multiplier_shift_add_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

divider_restoring: $(DIVIDER_DIR)/divider_restoring.v $(TEST_DIR)/divider_restoring_test.v FORCE
	mkdir -p $(BUILD_DIR) $(WAVE_DIR)
	$(IVERILOG) -g2012 -s divider_restoring_test -o $(BUILD_DIR)/$@ $(TEST_DIR)/divider_restoring_test.v $<
	cd $(PROJECT_DIR) && $(VVP) $(BUILD_DIR)/$@

FORCE:
