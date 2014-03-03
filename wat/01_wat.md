!SLIDE
![WAT](./wat.png "wat")

!SLIDE bullets incremental

* The Three laws of TDD
* Terminologie

!SLIDE
# Three Laws

> You are not allowed to write any production code unless it is to make a failing unit test pass.

!SLIDE
# Three Laws
> You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.
!SLIDE
# Three Laws
> You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

!SLIDE
# Terminologie
## Behaviour Test
* Test de buitenkant van je applicatie
* Ook wel Acceptance Test, Integration Test, Feature

!SLIDE
# Behaviour Test
> Its core idea is to replace confusing and developer-centric terminology (tests, suites, assertions etc) with ubiquitous language that all participating stakeholders (including non-technical staff, and, possibly, clients) can understand.

!SLIDE code

    @@@ Cucumber
    Feature: Search

      So that I can find campings
      As a user
      I want to search and filter campings

      @javascript
      Scenario: Search in title
        Given 1 Campings
        And a camping named "Bij Ons"
        When I visit the map page
        And I fill in search with "ons"
        And I click "Search"
        Then I should see only the camping "Bij Ons"

!SLIDE
# Terminologie
## Functional Test
* Black Box testing van je controllers
* Uitgekleed

!SLIDE code
    @@@ Ruby
    describe CampingsController do
      describe "GET show" do
        before do
          @camping = FactoryGirl.create(:camping)
          get :show, :id => @camping.id
        end
        it { should assign_to(:camping) }
        it { should assign_to(:title).with(@camping.name) }
      end
    end

!SLIDE
# Terminologie
## Unit Test
* Black box testing van models en objecten
* Beschrijft alle models, en andere "Dingen"

!SLIDE code
    @@@ Ruby
    describe "#website" do
      it { should allow_mass_assignment_of(:website) }
      it { should allow_value(nil).for(:website) }

      it 'should ensure website has a length of at most 255' do
        camping = Camping.new(:website => "x" * 256)
        camping.valid?
        camping.errors[:website].first.should match /is too long/
      end
      it 'should prepend http to urls without it' do
        camping = Camping.new(:website => "example.com")
        camping.valid?
        camping.website.should eq "http://example.com"
      end
      %w{example.com http://example.com https://example.com}.each do |valid_value|
        it { should allow_value(valid_value).for(:website) }
      end
    end

