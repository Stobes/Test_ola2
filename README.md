# Test_ola2

# Assignment #2

## 1. Reflections

  ### 1.1 Computer Mouse
  - Checking if all the buttons (both main and extra) are working as intented
  - Checking if the scrollwheel works
  - Checking how well the mouse performs on different surfaces (tracking)
  - Checking how many times your can click the mouse before it breaks
  - Checking how comfortable the mouse is
  - Checking if the material of the mouse is durable
      
  ### 1.2 Catastrophic Failure
  In the coastal town of Lumsås in 1982, a fateful missile launch incident occurred due to a software glitch. This event serves as a reminder of the vital role software systems play in our modern world and the potential repercussions of software errors. The Danish Navy's frigate "Peder Skram" was preparing for a NATO exercise at sea. Inexplicably, during a routine missile test, a software malfunction triggered the accidental launch of a 600-kilogram Harpoon missile. The missile's erratic trajectory spared lives but left behind a trail of destruction among unoccupied holiday homes. This incident remains a testament to the need for rigorous software testing and the safeguarding of critical systems against unforeseen software errors.

  Given that this incident was due to a glitch, a simulation test with safety overrides could have been employed as a preventive measure. Prior to any live missile test, a comprehensive simulation scenario could have been created. This scenario should mimic the conditions of a missile launch, including all relevant parameters, coordinates, and inputs.

  A simulation test, in short, is designed to assess how one would react to situations encountered while working and how one would solve problems.
  

## 2. Two Katas

  ### 2.1 String Utility
  ```
class StringUtils:
    @staticmethod
    def reverse(input_str):
        return input_str[::-1]

    @staticmethod
    def capitalize(input_str):
        return input_str.upper()

    @staticmethod
    def lowercase(input_str):
        return input_str.lower()

def test_reverse():
    # Given a string
    string = "aBc"

    # When the string is reversed
    result = StringUtils.reverse(string)

    # Then the result should be the reversed string
    assert result == "cBa"

def test_capitalize():
    # Given a string
    string = "aBc"

    # When the string is capitalized
    result = StringUtils.capitalize(string)

    # Then the result should be the capitalized string
    assert result == "ABC"

def test_lowercase():
    # Given a string
    string = "aBc"

    # When the string is lowercased
    result = StringUtils.lowercase(string)

    # Then the result should be the lowercased string
    assert result == "abc"

# Run the tests
if __name__ == "__main__":
    test_reverse()
    test_capitalize()
    test_lowercase()

    print("All tests passed!")

  ```
  ### 2.2 Bowling Game Kata
  ```
  class BowlingGame:

    def __init__(self):
        self.rolls = [0] * 21
        self.current_roll = 0

    def roll_ball(self, pins):
        self.rolls[self.current_roll] = pins
        self.current_roll += 1

    def calculate_score(self):
        score = 0
        frame_index = 0
        for frame in range(10):
            if self.is_strike(frame_index):
                score += 10 + self.strike_bonus(frame_index)
                frame_index += 1
            elif self.is_spare(frame_index):
                score += 10 + self.spare_bonus(frame_index)
                frame_index += 2
            else:
                score += self.sum_of_balls_in_frame(frame_index)
                frame_index += 2
        return score

    def is_strike(self, frame_index):
        return self.rolls[frame_index] == 10

    def sum_of_balls_in_frame(self, frame_index):
        return self.rolls[frame_index] + self.rolls[frame_index + 1]

    def spare_bonus(self, frame_index):
        return self.rolls[frame_index + 2]

    def strike_bonus(self, frame_index):
        return self.rolls[frame_index + 1] + self.rolls[frame_index + 2]

    def is_spare(self, frame_index):
        return self.rolls[frame_index] + self.rolls[frame_index + 1] == 10


import unittest
from BowlingGame import BowlingGame

class BowlingGameTest(unittest.TestCase):

    def setUp(self):
        self.game = BowlingGame()

    def roll_many(self, n, pins):
        for i in range(n):
            self.game.roll_ball(pins)

    def test_gutter_game(self):
        self.roll_many(20, 0)
        self.assertEqual(0, self.game.calculate_score())

    def test_all_ones(self):
        self.roll_many(20, 1)
        self.assertEqual(20, self.game.calculate_score())

    def test_one_spare(self):
        self.roll_spare()
        self.game.roll_ball(3)
        self.roll_many(17, 0)
        self.assertEqual(16, self.game.calculate_score())

    def test_one_strike(self):
        self.roll_strike()
        self.game.roll_ball(3)
        self.game.roll_ball(4)
        self.roll_many(16, 0)
        self.assertEqual(24, self.game.calculate_score())

    def test_perfect_game(self):
        self.roll_many(12, 10)
        self.assertEqual(300, self.game.calculate_score())

    def roll_strike(self):
        self.game.roll_ball(10)

    def roll_spare(self):
        self.game.roll_ball(5)
        self.game.roll_ball(5)

if __name__ == '__main__':
    unittest.main()
  ```


## 3. Investigation of Tools

  ### 3.1 JUnit 5

  #### @Tag
  Allows you to categorize your test method/classes with a userdefined tag.  
  Useful for selectively running tests based on their categories/tag.
  #### @Disabled
  Makes a test method/class disabled, meaning it won't be executed.
  Useful when you tempoarily skip a test that may be failing/not yet implemented.
  #### @RepeatedTest
  Is used to repeat the execution of a test method x number of times.
  Useful for testing senarios that need to be repeated x amount of times, to ensure stability or even verify random behaviour.
  #### @BeforeEach, @AfterEach
  Both annotations marks methods that are run before and after each test method.
  Useful for initializing resources before each test and then clean them up afterwards.
  #### @BeforeAll, @AfterAll
  Both annotations marks methods that are run once before and after all test methods in a test class.
  Useful for setting up expensive resources that can be shared across multiple methods - such as initializing a database conenction.
  #### @DisplayName
  Allows your to provide a custom name for a test method/class, which is displayed in test reports.
  Useful for providing descriptive names to your test, making it easier to understand the purpose of each test case.
  #### @Nested
  Enables the creation of nested test class with a test class.
  Useful for making a better and organized test code, by grouping related tests together.
  #### @assumeFalse, @assumeTrue
  Allows you to conditionally skip tests based on certain assumptions.
  Useful for controlling test execution, based on assumptions, making tests more flexible to different enviorments.

  ### 3.2 Mocking Frameworks

  For this assignment, I will be comparing 'unittest.mock' and 'pytest-mock'.

  #### Similarities:
  Both provide tools for creating and using mock objects to simulate the behaviour of real world objects and functions during testing.
  They allow you to configure the behaviour of mock objects, such as defining return values, side effects and assertions on method calls.
  
  #### Differences:
  'unittest.mock' is part of the Python standard library and is integrated with the built-in unittest framework.
  'pytest-mock' is a Pytest plugin specifically designed to enhance mocking capabilities within Pytest. It is not part of the Python standard library and requires installation as an external plugin.
  'pytest-mock' is known for its more concise and expressive syntax for mocking and asserting expectations, making test code more readable.
  'unittest.mock' is a general-purpose mocking framework suitable for various testing scenarios, including unit testing, integration testing, and system testing, whereas 'pytest-mock' is specifically designed for projects using the Pytest testing framework.

  #### Preference:
  I prefer Pytest because it offers clear and readable test syntax, making it easy to write and understand. Additionally, it follows Python conventions and allows for easy customization, which I find neat.
