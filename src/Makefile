CXX = g++
CXXFLAGS = -Wall -Werror -Wextra -std=c++17
LFLAGS = -lgtest

.PHONY: clean all test rebuild gcov_report

HEADERS = s21_containersplus.hpp s21_containers.hpp

HPP_FILES = $(wildcard */*/*.hpp)
TPP_FILES = $(wildcard */*/*.tpp)
TEST_SOURCES = $(wildcard tests/*.cpp)
TEST_OBJECTS = $(TEST_SOURCES:.cpp=.o)

tests/%.o: tests/%.cpp
	$(CXX) $(CXXFLAGS) -c $< -o $@

all: test

test: $(TEST_OBJECTS) $(HEADERS)
	$(CXX) $(TEST_OBJECTS) $(LFLAGS) -o test
	./test

gcov_report: clean $(TEST_SOURCES) $(HEADERS)
	$(CXX) $(CXXFLAGS) $(TEST_SOURCES) --coverage $(LFLAGS) -o test
	./test
	lcov -c -d . -o coverage.info --no-external
	lcov --remove coverage.info $(CURDIR)/tests/* --output-file coverage.info
	genhtml coverage.info --output-directory gcov_report
	open gcov_report/index.html

clean:
	rm -rf tests/*.o test *.o *.gcno *.gcda coverage.info gcov_report/
