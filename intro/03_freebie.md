!SLIDE center
# Wedstrijdje
![Real-World Solutions for Developing High-Quality PHP Frameworks and
Applications](cover.jpg)

!SLIDE bullets incremental
# Wedstrijdje #

* Begin met testen in je (nieuw te bouwen) plugin of thema.
* Met onderstaande tests of variatie daarvan, die **passen**.
* Tweet naar **@savviihq**
* Questions and help **@berkes**

!SLIDE code

    @@@ PHP
    class SanityTest extends PHPUnit_Framework_TestCase {
      public function YayMyTestsAreWiredUp() {
        $this->assertContains(
          'W00t. Tests are running!', 
          $this->page('/myplugin')
        );
      }
    }

!SLIDE code

    @@@ Cucumber
    Feature: Sanity

      As a visitor
      I want to see a simple text on a page
      So that I know I have my test running and wired up

      Scenario: Visit my pluginpage
        Given I am not logged in
        When I visit "/myplugin"
        Then I should see the text "w00t. Tests are running!"

