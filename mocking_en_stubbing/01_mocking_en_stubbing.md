!SLIDE center
# Mocking and Stubbing
![indifferent](indifferent.jpg)

!SLIDE bullets
# Precies de juiste calls testen

* Units zijn losse dingen.
* Integratie voegt deze samen.

!SLIDE center

!SLIDE code

    @@@php
    function find_initialize_self_with_attributes_from_db() {
      $this->mock_any_instance_of(Person)
        ->expect_call("db_select")
        ->with_arguments("persons", array("id" => 1))
        ->and_return(array("name" => "I am person #1"))

      $subject = Person::find(1);
      $this->assertEquals('I am person #1', $subject->name);
    }

!SLIDE code

    @@@php
    class Model
      public function db_select() {
        #... code to connect to
        # and fetch from database
      }
    }

    class Person extends Model
      public static function find($id) {
        $person = new self();
        $person->set_attributes(
          $person->db_select("persons", array("id" => $id)
        );
        return $person;
      }
      private function set_attributes($attributes) {
        foreach($attributes as $name => $value) {
          $this->set_attribute($name, $value);
        }
      }
    }

