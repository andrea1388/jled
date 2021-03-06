# JLed unit tests Makefile
# run `make coverage` to run all test and calculate coverage
CFLAGS=-std=c++11 -c -Wall -I. -I../src --coverage -fno-inline \
	   -fno-inline-small-functions -fno-default-inline -O0 -g -fmax-errors=5
LDFLAGS=-fprofile-arcs -ftest-coverage 

TEST_JLED_SOURCES=Arduino.cpp test_jled.cpp test_mock.cpp 
TEST_JLED_OBJECTS=$(TEST_JLED_SOURCES:.cpp=.o)

TEST_ESP32_SOURCES=Arduino.cpp test_esp32_analog_writer.cpp ../src/esp32_analog_writer.cpp
TEST_ESP32_OBJECTS=$(TEST_ESP32_SOURCES:.cpp=.o)

TEST_ESP8266_SOURCES=Arduino.cpp test_esp8266_analog_writer.cpp 
TEST_ESP8266_OBJECTS=$(TEST_ESP8266_SOURCES:.cpp=.o)

all: test_jled test_esp32_analog_writer test_esp8266_analog_writer

test_jled: $(TEST_JLED_OBJECTS)
	$(CXX) $(LDFLAGS) $(TEST_JLED_OBJECTS) -o $@

test_esp32_analog_writer: CFLAGS += -DESP32
test_esp32_analog_writer: $(TEST_ESP32_OBJECTS)
	$(CXX) $(LDFLAGS) $(TEST_ESP32_OBJECTS) -o $@

test_esp8266_analog_writer: $(TEST_ESP8266_OBJECTS)
	$(CXX) $(LDFLAGS) $(TEST_ESP8266_OBJECTS) -o $@

coverage: test
	lcov --config-file=.lcovrc --directory ../src --directory .. --capture --output-file coverage.info --no-external
	lcov --config-file=.lcovrc --list coverage.info
	mkdir -p report
	genhtml --branch-coverage coverage.info -o report

test: all
	./test_jled
	./test_esp32_analog_writer
	./test_esp8266_analog_writer

.cpp.o:
	$(CXX) $(CFLAGS) $< -o $@

clean:
	rm -f coverage.info *.{gcov,gcda,gcno,o} ../src/*.{gcov,gcda,gcno,o} 

clobber: clean
	rm -f test_jled test_esp32_analog_writer test_esp8266_analog_writer

