!SLIDE center
![goal](goal.jpg)

!SLIDE center
# Effort curve
![Efficiency](TDD_efficiency.png)

!SLIDE bullets incremental
# LinkDump
* Behat [behat.org](http://behat.org) Feature Tests
* PHPUnit [phpunit.de](http://phpunit.de) Defacto Standaard Unit Testing
* AspectMock [Codeception/AspectMock](https://github.com/Codeception/AspectMock) Mocking Library
* Codeception [codeception.com](http://codeception.com/) Voor als je van Overkill houd.

!SLIDE bullets incremental
# Opmerkingen
* Je hebt geen testframework nodig om te testen. Tests zijn ook gewoon
  code.
* Je hebt geen twee testframeworks nodig om te testen. Integratietests
  zijn ook gewoon code (maar wel met veel curl gegoochel).

!SLIDE code
    @@@PHP
    require "state_machines/comment_state_machine.php"

    class CommentMock {
      var $message_memo = array("set_published" => "not called");

      public function set_published() {
        $message_memo["set_published"] = "called";
      }
    }

    $comment = new CommentMock();
    $comment_state_machine = new CommentStateMachine($comment);
    $comment_state_machine->publish();
    if ($comment->message_memo["set_published"] != "called") {
      throw new Exception('Expected set_published to be called!')
    }


!SLIDE bullets incremental
# Opmerkingen
* Globals zijn klote. Ook in de implementatie. Schrijf Wrappers.

!slide code
    @@@php
    class myseoform extends phpunit_framework_testcase {
      function submitcallssetoptionwith {
        $wordpress = $this->mock(wordpress)
          ->expects("set_option")
          ->with("seo_meta_description", "needs moah seo");

        $subject = myseoform($mock_wordpress);
        $subject->fields(array("meta_description", "needs more seo"));
        $subject->submit();
      }
    }

!SLIDE code
    @@@PHP
    class MySeoForm extends Form {
      function initialize($wordpress) {
        $this->wordpress = $wordpress;
      }

      function submit() {
        foreach($fields as $name => $value) {
          $wordpress->set_option(
            $this->prefix_option($name),
            $value);
        }
      }

      private function prefix_option($option) {
        "seo_" . $option;
      }
    }

!SLIDE code

    @@@PHP
    class WordPress {
      def set_option($name, $value) {
        if(get_option($name)) {
          update_option($name);
        } else {
          add_option($name, $value);
        }
      }
    }
