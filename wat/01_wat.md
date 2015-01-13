!SLIDE center
# Wat
![WAT](./wat.png "wat")

!SLIDE bullets incremental
# Terminologie
* Integration
* Units
* TDD
* BDD
* The Three laws of TDD

!SLIDE bullets incremental
# Integration
* "It must be a rooster"
* "It must have an eye"
* "It must be 30mm wide, 90mm deep and 80mm high"

!SLIDE center
![integration](duplo.jpg)

!SLIDE bullets incremental
# Integration
* Test het gedrag van je site. Aan de buitenkant
* Test veranderingen aan de buitenkant bij interactie.


!SLIDE bullets incremental
# Units
* "It must be green"
* "It must have four knobs"
* "It must have one rounded edge"
* "It must be 30mm wide, 45mm deep and 20mm high"

!SLIDE center
![unit](duplo_unit_B.jpg)

!SLIDE bullets incremental
# Units and Integration
* Units kunnen veranderen
* Behaviour blijft hetzelfde

!SLIDE center
![different unit](duplo_integration_swap_units.jpg)

!SLIDE bullets incremental
# Voorbeelden
## Pseudocode

!SLIDE center
# Integration

!SLIDE code
    @@@ PHP
    class PublishComment extends PHPUnit_Framework_TestCase {
      // Test that a comment gets published immediately
      public function CommentIsPublished() {
        // Given: a story
        $story = $this->create_a_story();

        // When: we are on the story page
        $page = $this->visit($story->url);

        // And: we place a comment
        $page->fill_in("comment_form",
          array("body" => "I am comment")
        );
        $page->click_button("Place Comment");

        // Then we should see it on the page
        $page = $this->visit($story->url);
        $this->assertContains(
          'I am comment', 
          $page->find("#comments .body")->content()
        );
      }
    }

!SLIDE center
# Unit

!SLIDE code
    @@@ PHP
    class CommentStateMachine extends PHPUnit_Framework_TestCase {
      // It forces the published state on a comment-ish
      public function publishForcesPublishedOnComment() {
        $comment = $this->mock("Comment")
          ->allow("set_published");

        $comment->expects("set_published");

        $subject = new CommentStateMachine($comment);
        $subject->publish();
      }
      public function publishCannotPublishPublishedComment() {}
      public function publishReturnsTrueOnSuccess() {}
    }

!SLIDE center
# Other Units

!SLIDE code
    @@@ PHP
    class Comment extends PHPUnit_Framework_TestCase {
      function set_published_sets_published() { }
    }

    class CommentsController extends PHPUnit_Framework {
      # POST stories/1/comments
      function comment_is_created_with_params() { }
      function state_machine_is_created_with_comment() { }
      function calls_publish_on_state_machine() { }
      function redirects_to_comments_with_message() { }
    }

    class StoriesController extends PHPUnit_Framework {
      # GET stories/1
      #...
      function published_comment_is_included_in_comments() { }
      function unpublished_comment_is_omitted_from_comments() { }
      function passes_comments_to_comment_list_template() { }
    }


!SLIDE center
# Implementation Example

!SLIDE code
    @@@ PHP
    class CommentsController extends Controller {
      function action_create() {
        $comment = new Comment($this->request_params());
        $state_machine = new CommentStateMachine($comment);
        $state_machine->publish();
        $this->redirect_to('comments', "Comment Created!");
      }
    }



!SLIDE bullets incremental
# Omarm verandering
* Units kunnen herschreven worden.
* Maar aan de buitenkant blijft het hetzelfde werken. 
* Dat weet je "zeker", als je integrationtest groen is.
* (Voor alles wat je met die integrationtests test)

!SLIDE bullets incremental
# TDD: Test Driven development
* Schrijf eerst de tests
* En dan pas de code voor die test

!SLIDE bullets incremental
# BDD: Behaviour Driven development
* Variatie op TDD
* Schrijf eerst de gewenste uitkomst
* Test eerst de integratie (het gedrag)

!SLIDE
# Three Laws
> You are not allowed to write any production code unless it is to make a failing unit test pass.

!SLIDE
# Three Laws
> You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.

!SLIDE
# Three Laws
> You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

